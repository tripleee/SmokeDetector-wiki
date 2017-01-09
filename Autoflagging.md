# State of the Project

Caution: At this point in time, this page is an ad-hoc summary of work in progress. Autoflagging is preliminarily enabled right now, only casting a single spam flag per eligible post, to be expanded in the future (Stack Exchange permitting)

We are looking into automating flags from Smokey.  Basically, it will look as if though Smokey clicks "flag" -> "spam" as soon as Smoke Detector reports a post (Not all reported posts are eligible, see the Spam score section for details.).

We are working out the details of the system. Technically, the flagging is done by Metasmoke (the back end component) using credentials of a user who signed up to allow the system to cast flags on their behalf (currently only the core developers, @Undo and @ArtofCode).

To participate in the development of this feature, please show up in [the Charcoal HQ chat room](http://chat.stackexchange.com/rooms/11540/charcoal-hq) and wait for a good moment to bring up your topic (afternoon UTC seems to be a fairly busy time in the room).

The main dashboard (status, statistics, etc) is at https://metasmoke.erwaysoftware.com/flagging

# Technical details and spam score

Every time a post is reported, it triggers a variety of different reasons for being reported (such as bad keyword, blacklisted website, etc). Each of these reasons contributes to the post's spam score. The formula that determines how much score each reason contributes is as follows:

`[Numer of True Positives caught by reason] / [Total posts caught by the reason] * 100`

In our current preliminary testing, the threshold that was set for posts to be flagged automatically is at 280. In our database of over 50.000 records, this score threshold has a predictive accuracy of 99,98% (meaning of all posts hitting 280 score caught by smokey, 99,98% were true positives).
