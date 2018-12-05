> This document covers how to create a new spam check, which essentially turns out to be a guide on `findspam.py`.

## 1. The `B(are|ear)` Necessities
The *very first* thing you need to do before creating a new spam check is test if it's actually necessary.

- What is your proposed check designed to catch?
- Is it something that's caught by existing checks? This includes regex-based pattern checks, blacklists, and check methods. Use the various `!!/test` commands to check this.
- Is it something *we want to catch*? Remember that Smokey is designed to catch spam and/or abuse — anything else (low quality posts, not-an-answers, etc) is out of scope. There are plenty more moderation bots around the network that might want that kind of check, though.

## 2. Write a Check
...preferably addressed to me, with plenty of money involved. (Ha! Spelling jokes!)

If you've determined that a new check is necessary, now you need to actually write it. The preferred way of doing this is a regex — these are (usually) simpler and easier to maintain than the alternatives. Writing a regex check is pretty easy: just write the regex. You can use regex-checking websites like [regex101](http://regex101.com) to check if you've written it right — doing this is encouraged, because regex is not an easy language to speak.

The alternative, which should only be used if a regex doesn't do the job, is to write a check method. This is done by writing a new method in `findspam.py`, which takes two parameters: `s` and `site`. `s` is a string of stuff that you need to check (like the title, username, or post body), and `site` is the site that the post is on. Give your method a descriptive name, so that its purpose can be judged at a glance.

Your method should return a pair of values. The first is a boolean, indicating whether or not you think the post is spam. The second is a string, the `why` data for the post. It should be a short descriptive text that describes why you think it's spam, e.g. *Contains keyword \*male-enhancement\**. See the text box under the reasons list of [a metasmoke record](https://m.erwaysoftware.com/post/130809) for an example.

Here's an example check method. This method will say that any `s` longer than 3 characters is spam.

```py
def ridiculous_spam_check(s, site):
    if len(s) > 3:
        return True, "Length is greater than 3 characters"
    else:
        return False, ""
```

If you need to combine multiple pieces of information from a post (e.g [Username similar to website](https://github.com/Charcoal-SE/SmokeDetector/blob/5374e226dabb574a974bdebd826d8c9a9921fc93/findspam.py#L607), where you need both the post body and the username), see section 4 below.

## 3. Endless Lists
Checks are our ammunition against spam; now you need a gun to fire it from. In our case, it's a GLoCK — a Giant List of Checks and Keywords.

Read the code of the existing checks in [`findspam.py`](https://github.com/Charcoal-SE/SmokeDetector/blob/master/findspam.py), there are two kinds of them:

- RegEx-based checks are created and registered into the GLoCK with a call to `create_rule`:

  ```py
  create_rule("bad keyword in post", r"male\W?enhancement", max_rep=5, max_score=1)
  ```

- Functional checks are created by using `create_rule` as a decorator ([PEP 318](https://www.python.org/dev/peps/pep-0318/)):

  ```py
  @create_rule("spam answer", question=False)
  def ridiculous_check(s, site):
      return True, "All answers are spam"
  ```

  This way, the function `ridiculous_check` is wrapped into a `Rule` object and registered to the GLoCK.

#### Master Rule Creator

The prototype of the master Rule Creator™ function is

> **create_post**(reason, regex=None, **kwargs)

Accepted keyword arguments are:

- `title`, `username`, `body`, `body_summary`: These are the different parts of a post. Set them to *True* if your check should be performed against these aspects
- `all` and `sites`: `all` defines whether the check should apply on all sites, and `sites` define exception sites. If `all=True`, then posts *not* from a site in `sites` will be checked (whitelisted). If `all=False`, then only posts on `sites` will be checked.
- `max_rep`, `max_score`: Upper limits of owner reputation and post score. Generally, if the owner has more reputation or the post has a high score, it's unlikely that it will be spam.
- `question`, `answer`: Whether the check is designed for questions and answers. For example, you probably want to specify `answer=False` for a "bad question" check. Note that they're in the singular form.
- `stripcodeblocks`: Whether code blocks `like this` should be stripped before running the check.
- `whole_post`: See below
- `disabled`: Just a neat way to create a rule without putting it into production 😃.

The default values for those options are:

```py
create_rule(reason,
    all=True,
    sites=[],
    title=True,
    body=True,
    username=False,
    body_summary=False,
    max_rep=1,
    max_score=0,
    question=True,
    answer=True,
    stripcodeblocks=False,
    whole_post=False,
    disabled=False
)
```

Implementation details: `create_rule` takes an optional `regex` argument. If it's provided, then it creates a regular expression check. If no regex is provided, it returns a decorator that can be used to decorate a function-based check. This is how it works in two ways.

## 4. Other neat things

#### Partial reason

If a check is designed to check multiple aspects of a post individually, you may want separate reasons for the aspects checked. For example, *bad keyword in title*, *bad keyword in body* and *bad keyword in username* are three reasons.

To keep things minimal, you can use a pair of curly brackets in the reason, which will be replaced by one of `title`, `body` and `username`, if the corresponding part of the post is caught as spam. So you can write this as a reason:

```python
create_rule("bad keyword in {}", "male\W?enhancement")
```

Note: We're currently using `str.replace()` to insert the post aspect instead of using `.format()`, so only bare braces are supported.

#### `whole_post` check

If you need multiple pieces of information from a post, instead of checking title, body and username separately, you can define a method like this ([example](https://github.com/Charcoal-SE/SmokeDetector/blob/5374e226dabb574a974bdebd826d8c9a9921fc93/findspam.py#L607)):

```python
@create_rule("this is a reason", whole_post=True)
def another_ridiculous_check(post):
    if post.user_name in post.body and post.user_name in post.title:
        return False, True, False "Username in both title and body"
    return False, False, False, ""
```

The method should take one `post` object. You can find its available properties starting from [here](https://github.com/Charcoal-SE/SmokeDetector/blob/5374e226dabb574a974bdebd826d8c9a9921fc93/classes/_Post.py#L180). Then you can perform the check with the information provided in the object.

The return value is also a bit different from a standard check. A `whole_post` check should return 4 values, the format of which would be

```python
return title_is_spam, username_is_spam, body_is_spam, why
```

The first three boolean values indicate whether you think the title, the username or the post body is spam. The last value is `why` data, which is identical to the `why` data mentioned above.

When defining the entry for your check, you need to add `whole_post=True` to the rule creator, so that the check dispatcher can provide the post object to your method, instead of `s, site`.