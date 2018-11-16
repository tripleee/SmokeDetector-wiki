<!--
	EDITORS PLEASE NOTE:
	This page is intended as a quick "WTF is this?" reference for network moderators who've just come across an automatic
	"other" flag from Smokey about a deleted potential FP. Bear this in mind when editing - the audience here is _not_
	Charcoal members, and a majority of the audience will have little to no familiarity with Charcoal systems or nuances.
-->

> **Bug!**
>
> The initial implementation of this system had a bug in it that would cast a moderator flag when 0 spam flags were cast on the post. Whoops! If you see any of these, handle as you see fit. The bug is now fixed, so you shouldn't see any more.
{: .alert.link}

If you're reading this page, you've probably just found an automatic flag cast by SmokeDetector that says something about a post having had Charcoal members flag it as spam but then decided it wasn't. This page is an explanation of what that's about.

## What are these flags?
These flags are mostly informational for you. There is very little visibility into posts that have been deleted by the community for moderators, including cases where posts were deleted with spam flags. This can lead to some undesirable situations, where posts are unnecessarily marked as spam or, in the worst cases, users are penalized, if the flaggers got it wrong. The automatic "other" flags that SmokeDetector casts are there to alert you to cases of posts that were deleted, and had some spam flags on them, but might not have been spam. These cases need a moderator (that's you!) to look at them and make sure the spam flags were appropriate.

## When are they cast?
Rarely. These flags are cast when all of the following are true:

 - SmokeDetector reported the post as being potentially spam.  
 - Charcoal members (people looking at the report) manually cast at least one spam flag on the post.  
 - The post was later classified as not being spam - either as a false positive or just not an answer (NAA).  
 - The post was later deleted.

In terms of frequency, we see these cases about once every 10 days or so, network-wide. Many small sites on the SE network will never see one of these flags; even the large sites are unlikely to get more than one or two a month. This makes these flags much rarer than most Community auto-flags.

## What do you need to do?
Take a look at the post that was flagged. If there are spam flags on it that weren't retracted, check the post was actually spam - if it was, all is well. If it _wasn't_, you may want to dispute (via post mod menu > "clear spam/offensive flags") or decline the spam flags. If the post shouldn't have been deleted _at all_, now is also your opportunity to undelete it.

If you feel like it, we'd also appreciate you letting us know in [Charcoal HQ](https://chat.stackexchange.com/rooms/11540) that the spam flags were inappropriate. This lets us keep track of where we're getting it wrong, and helps us to make improvements to our systems and policies for the future.

## What if you don't want these flags?
That's cool. Have a discussion with your local mod team, and reach agreement on whether or not you want these flags. If you decide you don't, ping Undo and/or ArtOfCode in [Charcoal HQ](https://chat.stackexchange.com/rooms/11540), and we'll flip them off for your site.