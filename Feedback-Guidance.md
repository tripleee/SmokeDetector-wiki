Some aspects of feedback to SmokeDetector have historically caused confusion. This page is intended to address some of those confusions.

## Generic Guidance
In very general terms, the litmus test for whether you should use [`k`](Commands#silent-mode-and-aliases) or [`f`](Commands#silent-mode-and-aliases) is this:

> If SmokeDetector was implemented as a system-level block, would we want to catch this type of activity?

If the answer to that question is *yes*, you should mark the post `k`. Otherwise, a `f` or `n` response may be more appropriate.

If it's not obvious which type of feedback was appropriate for a post, it may be easier to refrain from giving feedback until you can discuss it with others in Charcoal HQ and work out what the correct response is. You can also [leave a comment on the metasmoke record](https://charcoal-se.org/smokey/Comments) to help others looking at the record work out what's already been thought of. Please don't comment on the post itself on Stack Exchange unless you're a regular of the site.

There are a few types of activity we have specific feedback guidelines for, as outlined below.

## Disclosed affiliation
It's fine to promote your own product or service on Stack Exchange, *as long as*:

- you're not doing it excessively
- you disclose your affiliation
- you only do so where relevant

If all of those conditions are true, then self-promotion is not spam and therefore `f` and not `k` (unless it doesn't answer the question, in which case it's `n`). If any of them are false, self-promotion is `k`.

## Self-vandalism
Self-vandalism is where a user vandalises their own post by replacing all its useful content with something like "xxxxxxxxxxxxxxxxxxxxxxxx", or "deleted deleted deleted". For self-vandalism, use [`tp-`](Commands#privileged-commands-as-reply) (or one of its aliases, such as `v`, `vand` or `vandalism`). At a system level, we'd want to catch and block people doing this, but it's not worth blacklisting the user because it's usually a one-time incident. Most users, when warned, don't do it again.

## Posts containing only garbage
For posts containing no understandable content (e.g. "dfajiojaifojadiofjadhiga"), these should be given `tp` or `tpu` feedback, because we would want a system-level block of this content.

However, if you choose to raise a flag, you want to be a bit more nuanced in which flag you use. [Shog9's answer on MSE](https://meta.stackexchange.com/a/234035) indicates that, in the vast majority of cases, almost any flag works, but that he's partial to "rude or abusive", as those flags get the post deleted faster. For users with more than a very small amount of reputation, you [should stay away from red-flags (spam or R/A)](https://chat.stackoverflow.com/transcript/41570?m=26705146) ([MSE](https://meta.stackexchange.com/a/58035)). Give those users the benefit of doubt and raise an NAA flag. In addition, be aware that which flags are acceptable for this type of content are different on *some* individual sites. On some sites, flags other than "rude or abusive" and NAA may be declined (e.g. some sites will decline spam flags on this type of content: [physics](https://physics.meta.stackexchange.com/q/10875)).

## Foreign-language posts on English sites (or vice versa)
Treat these as you would an English post. If it's spam, offensive, etc., then mark it as `k`; otherwise use `f` or `n`. Particularly, answers in the wrong language for the target site are NAA, so `n`. Being in the wrong language for the site *alone* doesn't make a post `k`-able.

## Plagiarism
Plagiarism — copying without attribution from another source such as someone else's answer or another website — is not always easy to spot. If you do spot it in an answer, then mark it as `k` — you may wish to explain to other users in the chatroom why you've done that, to avoid arguments about what the feedback should be.

If you get to a post before it's deleted, an easy way to spot plagiarism is to check the other posts on the same page for similar content.

However, while plagiarism should be marked as `k`, the `!!/report` command shouldn't be used to report plagiarism — catching plagiarism is a bonus if we do, but we're not aiming to catch it.

## Repairable offensive posts
Some people think that *f\*cking* is a synonym for *very*, and so they use it to provide emphasis when writing their post. These posts usually can be salvaged by editing out the inappropriate language and leaving a comment. Therefore the appropriate feedback is `f` as we [don't want a system-level block preventing these kind of posts](https://github.com/Charcoal-SE/SmokeDetector/issues/995#issuecomment-319727732).

However, if a post is edited by the author in a way which is mostly offensive, then the appropriate feedback is `tp-` as we would've wanted that edit to be blocked by the system.

## NAA feedback
NAA feedback has sometimes been a little confusing. Using `n` as your feedback should, in general, be done if:

- the post is not spam, abusive, offensive etc. (use `k`)
- you would flag the post as Not An Answer on the site itself

### Bad questions

The NAA feedback is disabled on questions, as questions are, in fact, not answers. But what if the question is VLQ, off-topic, too broad, or otherwise considered 'bad' by SE's quality standards? Often, it's not entirely clear whether the `tp-` or `fp-` feedbacks are appropriate. 

In these cases, it's recommended that you pick the feedback type that feels most appropriate (if you're still unsure, err on the side of caution and choose `f`). Then, leave a comment on the post indicating what is wrong with it, and why you chose that feedback.