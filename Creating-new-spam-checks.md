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

Scroll to the `rules` array, which is [somewhere around line 1150 in `findspam.py`](https://github.com/Charcoal-SE/SmokeDetector/blob/master/findspam.py#L1146). This structure describes all the checks that SmokeDetector runs, and how to apply them. (N.B.: It's not actually JSON, don't make that mistake — it's Python dicts.)

You need to add a new entry to this array that describes your check. The general format of this dictionary is:

```py
{
    'regex': r"Include your regex here if it's a regex-based check",
    'method': method_name,  # Pass the name of your method here if it's a method-based check,
    # You should include only one of above, not both

    'all': True,            # True if you want to scan all sites in the network, False otherwise,
    'sites': [],            # If `all` is true, these sites are excluded; otherwise, they are the only sites to get scanned
    'reason': "Name of the reason you're categorising these posts as (bad keyword, link at end of body, etc)",
    'title': False,         # True if you want to scan post titles, False otherwise
    'body': True,           # True if you want to scan post bodies, False otherwise
    'username': False,      # True if you want to scan owner usernames, False otherwise
    'body_summary': False,  # True if you want to scan body summaries, for a preemptive check
    'stripcodeblocks': False,  # True if you want code removed before getting passed to your check
    'max_rep': 20,          # Posts from users above this reputation will not be scanned
    'max_score': 1,         # Posts scoring above this value will not be scanned

    'questions': True,      # False if questions shouldn't be checked, optional
    'answers': True,        # False if answers shouldn't be checked, optional
}
```

You should only include *either* `regex` or `method` — checks should not be both at the same time.

## 4. Other neat things

#### Partial reason

If a check is designed to check multiple aspects of a post individually, you may want separate reasons for the aspects checked. For example, *bad keyword in title*, *bad keyword in body* and *bad keyword in username* are three reasons.

To keep things minimal, you can use a pair of curly brackets in the reason, which will be replaced by one of `title`, `body` and `username`, if the corresponding part of the post is caught as spam. So you can write this as a reason:

```python
    'title': True, 'body': True, 'body_summary': True, 'username': True,
    'reason': 'bad keyword in {}' 
```

Note: We're currently using `str.replace()` to insert the post aspect instead of using `.format()`, so only bare braces are supported.

#### `whole_post` check

If you need multiple pieces of information from a post, instead of checking title, body and username separately, you can define a method like this ([example](https://github.com/Charcoal-SE/SmokeDetector/blob/5374e226dabb574a974bdebd826d8c9a9921fc93/findspam.py#L607)):

```python
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

Then, when defining the entry for your check, you need to add `'whole_post': True` to the dict, so that the check dispatcher can provide the post object to your method, instead of `s, site`.