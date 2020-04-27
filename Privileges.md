SmokeDetector operates a privilege system. That is, before you are able to use a number of commands (most notably the feedback commands), you must be added to a list of privileged users in SmokeDetector's code. 

Please review this page before getting in touch with someone with a request; once you know what you need, see [whom to ping.](https://charcoal-se.org/pings/)

For broader background, please also review the [training section.](https://charcoal-se.org/training/)

For guidance on reviewing possible spam posts, please review [Feedback Guidance.](https://charcoal-se.org/smokey/Feedback-Guidance)

## Getting reviewer privileges with SmokeDetector
In theory, anyone can be added to the privilege list. In practice, this doesn't always work out, so *as a general guideline*, we look for a few things to indicate how qualified you are.

- **Reputation**  
  A higher reputation score indicates a higher level of participation on the sites, which is strongly correlated with moderation ability. We're looking for enough rep to indicate that you've been around a little while: generally, 300 on one site will suffice.

- **Participation**  
  We can also simply look through your various accounts on the network. SmokeDetector scans posts for spam network-wide, so the more sites you have accounts on, the better it is for everyone — more accounts means you can flag spam on more sites. We may also look at how active you've been on various sites (and on their meta sites) to determine how able you are to moderate content effectively. Again, we're not looking for a massive or exceptional record, just enough to show that you know what you're doing.

- **Referral**  
  If your request for privileges is supported by a regular of one of the [chat rooms](Chat-Rooms) that SmokeDetector posts reports to, we'll look more favourably upon it — we tend to trust people who are already part of the system to make sound judgements. Additionally, if you've been around in one of the rooms for a while and have made yourself known, you've got a good chance. However, notice that some rooms have policies of their own for whom to grant SmokeDetector privileges to (in particular, SOCVR and SOBotics require approval from a room owner) -- check your chat room's policies as well.

These are all general guidelines, rather than hard limits. Really, we're just checking to make sure that you're a sane person who won't abuse the system. We understand that there are cases of users who have little apparent activity who can be excellent at moderation; we're also aware that the converse is true. Take note of what's mentioned here, but also remember that requests are judged on a case-by-case basis.

#### For Moderators
If you're a Stack Exchange network moderator, **you're automatically privileged** with SmokeDetector in [Charcoal HQ](http://chat.stackexchange.com/rooms/11540/charcoal-hq) (and in [SOCVR](http://chat.stackoverflow.com/rooms/41570/so-close-vote-reviewers) if you are a Stack Overflow moderator). You don't need to be added to the explicit privilege lists, as your diamond also gives you privileges with SmokeDetector. We assume that moderators are, on the whole, pretty good at moderation.

Moderators can also see additional information on their [site dashboard](https://metasmoke.erwaysoftware.com/sites/dash) in relation to spammers and autoflagging participants.

<sup>Diamond-based privileges apply to any room you have a diamond in. This means, in effect, they extend across one entire chat server (two if you're an SO or MSE mod; three if you're an SO _and_ MSE mod - looking at you, ChrisF). Diamond privileges _do not inherit_ like normal privileges do - if your privileges in CHQ are based on your diamond, they will not inherit to Tavern on the Meta.</sup>

## Privilege Levels

There are multiple privilege levels on SmokeDetector and metasmoke, each giving you access to different commands, tools, etc. There isn't any exact threshold that you have to meet in order to be eligible for many of these privileges; rather the admins will grant them to you at their own discretion. If you think that you should have some of these privileges but you don't, please contact [an admin](https://charcoal-se.org/people#admins).

This is not a strict hierarchy; if you have special needs, you might need a specific privilege.
This exposition roughly outlines a typical progression from newcomer to trusted project admin.
(Obviously, most users never want or need to become project administrators.)

(SD) refers to privileges set in the code of SmokeDetector in [`users.yml`](https://github.com/Charcoal-SE/SmokeDetector/blob/master/users.yml) and [`rooms.yml`](https://github.com/Charcoal-SE/SmokeDetector/blob/master/rooms.yml), (MS) refers to privileges set from within metasmoke (the admin would then add you using the form on [this page](https://metasmoke.erwaysoftware.com/admin/permissions)), and (GH) refers to privileges set on GitHub.

### SmokeDetector privileges (SD)
The process for acquiring these privileges is listed above. Depending on where you get privileges, your privileges may apply to one or to multiple rooms: if you acquire them in SOCVR, your privileges will apply only to SOCVR; if you acquire them in Charcoal HQ, you will also be automatically privileged in Charcoal Test and Tavern on the Meta.

This privilege level allows you to:
* Give feedback via chat
* Use the privileged commands listed [here](./Commands#privileged-commands).
* Add comments to posts from chat (simply reply to any SD report)
* Stop autoflagging in the event of an emergency using `!!/stopflagging`. After this, autoflagging can only be re-enabled by an admin.

Technically, this privilege is granted in the Smoke Detector source code
by adding the user's numeric account ID to the `privileged_users` list for the room in question.  When this is in place, the `!!/amiprivileged` chat command
will cause Smoke Detector to reply "✓ You are a privileged user".

* Requirements: You have a user account on Stack Overflow / Stack Exchange
  with enough reputation to use the chat rooms where you want to interact with Smokey
* Requirements (SOCVR, SOBotics): Room owner approval for this change
* Recommended: metasmoke account
* Recommended: Enough exposure to Smoke Detector to broadly understand
  what these privileges mean
* Admin instructions:
  * Add user to `users.yml` if not already present
  * Add user to `rooms.yml` in the appropriate section(s)

### Flagger (MS)
Everyone who signs up to metasmoke gets this privilege by default
(unless that's turned off, which it sometimes is, e.g. in response to troll attacks).
* Allows you to set up your account so that it will be used for autoflagging

You can sign up for a metasmoke account without being a Stack Overflow / Stack Exchange user;
though most users will come from one of those systems,
and want their metasmoke account to be linked to their Stack Exchange network user account.
Sign up for a metasmoke account through this link:
https://metasmoke.erwaysoftware.com/users/sign_up

You don't need a metasmoke to interact with Smoke Detector,
and you don't need to interact with Smoke Detector in order for metasmoke to be useful.
Typically, new users sign up for one or the other,
and then sign up for the other within at most a few days.

* Requirements: You have created a metasmoke account
* Recommended: You are a registered user on Stack Overflow or Stack Exchange,
  and link your metasmoke account to your Stack Exchange network account
* Admin instructions: Click Flagger in metasmoke user screen if requested
  (i.e. the user account was created at a time when this was not automatically granted)

### Reviewer (MS)
Everyone who has SmokeDetector privileges is eligible to get the reviewer role.
However, this process is not automatic, so you will need to ask an admin to grant it to you.

This allows you to:
* Review posts from the [metasmoke review queue](https://metasmoke.erwaysoftware.com/review)
* Use applications which require the write API (e.g. userscripts such as FIRE and FDSC)
* Associate your chat feedback with your metasmoke account when [you connect your SE account](https://metasmoke.erwaysoftware.com/authentication/status) (this should be done when you sign up, older users may need to do this manually)
* Overwrite and invalidate your own feedback
* Use the [autoflagging conditions sandbox](https://metasmoke.erwaysoftware.com/flagging/conditions/sandbox)
* Add comments to posts from metasmoke

As already mentioned, this privilege is yours for the asking.
* Requireds: have a metasmoke account (see above)
* Required: ask an admin to add this privilege
* Admin instructions: Click Reviewer in metasmoke user screen

### Blacklist manager a.k.a. code admin or blacklister (MS)
For new users, watching and blacklisting causes a pull request on GitHub to be creatred.
Once you gain experience and confidence, we trust you to manipulate the watchlists and blacklists
without this review step.
* Can `!!/watch` and `!!/blacklist` without approval. Please make sure that you read the [blacklisting guidelines](https://charcoal-se.org/smokey/Guidance-for-Blacklisting-and-Watching) before using these commands.
* Can approve other users' watches and blacklists on GitHub. Simply use the [`!!/approve <PR number>`](https://github.com/Charcoal-SE/SmokeDetector/wiki/Commands#user-content-detection-blacklists-and-watchlist) command from chat and Smokey will handle the rest. You should also be able to approve such watch and blacklist PRs, but not other PRs, by adding a comment on the auto-generated PR containing the text `!!/approve`, and metasmoke will handle the rest. However, merging PRs with such comments is not working at this time.
* Can failover standby instances from the [status](https://metasmoke.erwaysoftware.com/status) page. Normally metasmoke handles this automatically if an instance goes down for more than 3 minutes, but you can use this if Smokey isn't working properly. Make sure that you follow the [troubleshooting guidelines](https://charcoal-se.org/pings/#dead) first.

* Required: a GitHub account we can add to our organization
  (strictly speaking optional if you _only_ want the failover privilege).
* Required: enough experience with the blacklists (typically through GitHub PRs)
  that we can be confident that you have the required competence
* Admin instructions:
  * In metasmoke, tick Blacklist Manager on the user's account
  * If the user is not already a member of the
    [Charcoal-SE GitHub organization](https://github.com/Charcoal-SE),
    they will need to be invited to join Charcoal-SE and accept the invitation.
    (Probably invite to OAP at the same time; see next item)
  * Add the user's GitHub account to the
    [Other Awesome People (OAPs) team on GitHub][1]
    (only visible to Charcoal-SE members)
  * Add the user's GitHub account to the [`.pullapprove.yml`][2] file.
    Once they've been added to the `.pullapprove.yml` file,
    you need to press the 'sync everything' button on
    [this PullApprove page](https://pullapprove.com/Charcoal-SE/SmokeDetector/settings/)
    (near the bottom of the page).
    After clicking on PullApprove's 'sync everything' button,
    the error that shows at the top of the PullApprove page should go away.
  * After all that is done, or at least the after the Blacklist Manager role is granted on MS,
    the user (or someone) will need to run `!!/amicodeprivileged`
    to have SD update its cached list of Blacklisters

 [1]: https://github.com/orgs/Charcoal-SE/teams/oaps/members
 [2]:; https://github.com/Charcoal-SE/SmokeDetector/blob/master/.pullapprove.yml

### Core (MS)
Given to people who have contributed to Charcoal in a significant way.
This signals that you are a core member of our team.

Benefits include:
* Increased autoflagging frequency (see [this][3] page for details)
* Access to the [SQL](https://metasmoke.erwaysoftware.com/data/sql)
  and [JavaScript](https://metasmoke.erwaysoftware.com/data) data explorers
* Ability to download [database dumps](https://metasmoke.erwaysoftware.com/dumps)*
* Can create [new announcements](https://metasmoke.erwaysoftware.com/announcements/new)
  (please don't use this if you don't know what you're doing)
* Can edit domain records, and add/edit domain tags
* Can create abuse reports & contacts and change their statuses

<sup>* Although downloading database dumps is restricted to core users, you're welcome to distribute them onwards to other people who ask for them too.</sup>

[3]: https://charcoal-se.org/smokey/Set-Up-Autoflagging#i-opted-in-but-i-dont-see-any-flags

### GitHub push privileges a.k.a. proper code admin (GH)

These people have collaborator access on GitHub. 

* Can push code directly to GitHub, manage PRs and issues,
  and add people to the SmokeDetector privilege list.
* ***ALWAYS PUSH TO MASTER, NEVER DEPLOY!***
* Generally it's fine to directly push minor changes
  (e.g. privilege, blacklist, watchlist, regex, and spam check changes, bug fixes)
  to master without any reviews;
  it is recommended that you make a PR and ask for reviews on any major changes
  (e.g. refactoring, changed functionality, new commands, new rules)

One of [the project's owners on GitHub][4] will add you as a collaborator
to the correct repository by assigning you to
[the appropriate team on our GH organisation][5].
Note: if you're already part of the GH organisation, the team maintainer can also add you.

 [4]: https://github.com/orgs/Charcoal-SE/people?utf8=%E2%9C%93&query=%20role%3Aowner
 [5]: https://github.com/orgs/Charcoal-SE/teams

### SmokeDetector Runner (MS)

Note that you can still run a SmokeDetector instance without this privilege;
however its functionality will be limited without it.

* Has a copy of the credentials for the SmokeDetector account on SE and GH
* Has the ability to [generate](https://metasmoke.erwaysoftware.com/smoke_detector/mine)
  metasmoke integration tokens, required in order for Smokey to integrate with MS
  (e.g. feedbacks, privilege checks, autoflagging, etc)

### Admin (MS)

These people get access to lots of administrative tools.
They are able to see most data that is usually only visible to its owner,
and perform system-level administration and maintenance tasks.
All admins are also subscribed to the `smokey@charcoal-se.org` mailing list
- any email sent to that address will reach the admins.

They can:

* Manage privileges for all users
* See posts which have been flagged for admin attention
* Create API keys, edit them, and revoke write tokens, on the behalf of the application author
* Invalidate other people's feedback
* Manually expire announcements
* View, edit, enable/disable and delete other users' autoflagging conditions
* Invalidate autoflagging API tokens in the event of an emergency
* Edit global autoflagging settings (e.g. enabled/disabled, min accuracy and post count,
  dry run, and max flags - note that the latter is also hard-coded for extra security)
* Edit metasmoke site settings
* Edit and delete abuse reports & contacts
* Edit and delete comments
* Destroy domain records and domain tags
* De-authorize a rogue SmokeDetector instance
* Kill all SmokeDetector instances
* Remove 'skip' reviews
* Manage Spam Wave settings

### MS Developer (MS)

Only available to our benevolent dictators Art, thesecretmaster, Undo, and Thomas Ward.
Only Undo can grant this privilege level, by editing the database directly from the console.

* Can see production logs
* Can deploy metasmoke
* Can refresh the site list cache
* Can refresh the per-post feedback cache
* Can destroy metasmoke post records
* Can destroy metasmoke users
* Can send messages down metasmoke's websockets for testing and development purposes
* Has access to a user details page and associated tooling
  (including refreshing chat IDs and mod sites, and sending password reset emails manually)
