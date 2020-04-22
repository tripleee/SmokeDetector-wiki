This wiki page contains a list of commands and their explanation.

## Commands for everyone

These commands can be executed by everyone.

- `!!/alive` or `!!/live` — Replies a random message taken from a list so you can see that SmokeDetector is still running. 
- `!!/status` — Shows the UTC date when SmokeDetector started running.
- `!!/ms-status` — Shows the status of metasmoke. If SmokeDetector is unable to communicate with metasmoke, then SmokeDetector will assume that metasmoke is down and continue processing posts and reporting them into chat without attempting to communicate with metasmoke.
- `!!/ms-up` — Instructs SmokeDetector that metasmoke is up. SmokeDetector will attempt to communicate with metasmoke. This is the normal, default state.
- `!!/ms-down` — Instructs SmokeDetector that metasmoke is down. SmokeDetector will not attempt to communicate with metasmoke.
- `!!/rev` or `!!/ver` — Shows the running Git revision.
- `!!/help`, `!!/info`, `!!/commands` — Shows a small help message about SmokeDetector.
- `!!/apiquota` — Shows the remaining API quota of SmokeDetector.
- `!!/queuestatus` — Shows the queue status of BodyFetcher.
- `!!/blame` — Chooses randomly from a list of people who have talked recently in the room.
- `!!/lick`, `!!/wut`, `!!/coffee`, `!!/tea`, and `!!/brownie` — better versions of `!!/alive`, aka 'fun' commands.
- `!!/location` — Replies with the current location, as set in the `config` file.
- `!!/test site=<site_domain> <string>` — Runs `<string>` against the filter as if it appeared in a question title, body, or username. To test specifically, use `!!/test-a` for answer, `!!/test-q` for question body, `!!/test-t` for title, or `!!/test-u` for username. Note that the site is optional. If site is present, the command will use filters for that site.
- `!!/isblu`, `!!/iswlu` — Checks if a user is blacklisted/whitelisted. Two formats are accepted: `<profile_URL>` or `<user_ID> <site_name>`
- `!!/whoami` — Replies with the bot's user id for that site
- `!!/whois admin` — Replies with a list of admins (and who's currently in the room).
- `!!/whois blacklister` — Replies with a list of blacklisters (and who's currently in the room). Aliases for `blacklister` include: `blacklist_manger`, `blacklisters`, `code_admin`, and `codeadmins`.
- `!!/amiprivileged` — Lets you know if you are in the list of privileged users
- `!!/amicodeprivileged` — Lets you know whether or not you have code privileges (i.e. you can blacklist without approval)
- `!!/notify <chatroom_ID_number> <site_domain>` — Tells SmokeDetector to ping you, in the given chatroom, when a post is reported on the given site.  
  Example:  `!!/notify- 89 parenting.stackexchange.com`  
  Note: Please use the squelch suffix (`-`) and avoid spamming the chat room with too many requests. See [this chat message](http://chat.meta.stackexchange.com/transcript/message/4157790#4157790) and the surrounding context.  
  Note 2: The list of who to notify is maintained separately by each SmokeDetector instance. This means that if the active instance is switched to a different one, you will need to run a `!!/notify-` command again, if you haven't previously done so for the newly active SmokeDetector instance.
- `!!/unnotify <chatroom_ID_number> <site_domain>` — Cancels the previously set notification.  Also, accepts the silent mode suffix&nbsp;(`-`).
- `!!/unnotify-all` - Removes all notifications.
- `!!/willbenotified <chatroom_ID_number> <site_domain>` — Reports whether you will be pinged, in the given room, about spam on the given site.
- `!!/allnotificationsites <chatroom_ID_number>` — Shows all sites that you will be pinged for in the given room.
- `!!/scan <post URL 1> [<post URL 2> [...<post URL 5>]] ["custom scan reason"]` — Directs SmokeDetector to scan a post. This is useful when you're not sure if a post is spam and don't want to report it. Smokey will go through all the usual processes of scanning a post and report it if it's spam, and will tell you that it's not spam otherwise. If you're sure it's spam but it isn't being caught, use `!!/report` instead. A custom scan reason may be supplied. If you include a custom reason, it's required to be enclosed in double quotation marks (e.g. `"custom scan reason"`).

## Commands as reply for everyone

- `why` — Shows the reason that SmokeDetector caught a post.  
  Note that `why` data is only kept for the last 50 reports. If you need to see older data, it can be found in the post record on Metasmoke.
- `autoflagged` — Returns if the post was autoflagged or not, and if so, what users were used.

## Privileged commands

These commands require [privileges](https://charcoal-se.org/smokey/Privileges#smokedetector-privileges-sd). Note that some commands may be disabled in some rooms. You may talk to others to understand why.
<!-- These were not in any order. Recommend most-used/useful up top. -->

- `!!/report <post URL 1> [<post URL 2> [...<post URL 5>]] ["custom reason"]` — Makes SmokeDetector scan and report a specific post/multiple specific posts in Charcoal HQ and other applicable rooms. Recommended over `!!/scan` if you're sure the post is spam. The originator of each post will be added to the blacklist if the post wouldn't have been caught otherwise. Maximum 5 posts at a time. An optional custom reason may be supplied so others are clearer why you're reporting it. Additionally, the post will be added to the database on Metasmoke, just like all other reported posts. If you include a custom reason, it is required to be enclosed in double quotation marks.
- `!!/report-force <post URL 1> [<post URL 2> [...<post URL 5>]] ["custom reason"]` — Same as `!!/report`, but causes SmokeDetector to ignore the active instance's record of the post being recently reported.
- `!!/scan-force <post URL 1> [<post URL 2> [...<post URL 5>]] ["custom reason"]` — Forces SmokeDetector to scan a post (see `!!/scan` above). The post will be reported if detected as spam, even if the the post was recently reported. This is useful to back-fill metasmoke with reports it missed due to being down, or SmokeDetector just thinking metasmoke was down (e.g metasmoke being up was not automatically detected and a `!!/ms-up` command wasn't issued). Note that for back-filling metasmoke, the scan will be on the current version of the post and, of course, can't scan posts that have been deleted.
- `!!/allspam <user URL>` — To be used if a spammer has many posts so you don't have to use `!!/report`. This command posts a message about the user in all applicable rooms.  Note that this command does NOT auto-TPU anything, for various reasons. Both individual site and network-wide user profiles are supported. It has an alias, `!!/reportuser <user URL>`.
- `!!/feedback <post_URL> <feedback_type>` - Takes a valid SE post URL as input, and manually sends the given feedback to metasmoke. Note that this won't blacklist/whitelist users automatically.
- `!!/reboot` — Reboots SmokeDetector.
- `!!/stappit` — Stops all SmokeDetector instances.
- `!!/stappit <string>` — Stops all SmokeDetector instances where `string` is included in the location (e.g. `!!/stappit undo` would stop `Undo/EC2` and `Undo/DO`, but not `teward/aroura`
- `!!/standby <string>` - Places that instance into standby mode. *The one that has been [active](https://metasmoke.erwaysoftware.com/status) the most over the last while is the one we will normally prefer stays running. The reason for that is that there is some state information which is specific to each instance (e.g. user-blacklist; notify list; recently reported post list; user-whitelist; etc). We generally want to keep the instance active which has the larger amount of recent information.*
- `!!/standby-except <string>` <string> - Places all other instances into standby mode, use if multiple instances are running.
- `!!/pull` — Pulls new revisions from GitHub.
- `!!/pull-sync-force` — For use when other methods of resolving git issues fail, particularly resolving "HEAD isn't at tip of origin's master branch". After a `git fetch --force`, this command performs `git branch --create-reflog -f master -t origin/master`, which replaces the SmokeDetector instance's local master branch with what's on origin/master. It also does the same thing for the deploy branch. This command shouldn't be needed on a regular basis, as git operations have been made more robust (e.g. using `git reset --hard origin/master` elsewhere). Use `!!/pull-sync-force` if you really need to. It is recommended that you `!!/reboot` after executing this command in order to start using the current version of the files.
- `!!/pull-sync-hard` — For use when other methods of resolving git issues fail. Uses a series of `git` commands to `--force` both the master and deploy branches to be on the same commit as origin/master and origin/deploy (normally, origin is set to [Charcoal-SE/SmokeDetector on GitHub](https://github.com/Charcoal-SE/SmokeDetector)). An alias, `!!/pull-sync-hard-reboot`, will automatically reboot the SmokeDetector instance after syncing both branches to the origin. If you don't have it automatically reboot, it's recommended that you `!!/reboot` after executing this command in order to start using the current version of the files.
- `!!/master` — When SmokeDetector enters reverted mode, use this command to go back to the `deploy` branch.
- `!!/gitstatus` — Shows which git branch the SD instance is on and if it is behind origin/deploy.
- `!!/errorlogs <N>` — Shows lines of the error logs for the last *N* exceptions. (You can also use `!!/errorlog`, `!!/errlog` or `!!/errlogs`)
- `!!/block <N>` — Blocks SmokeDetector globally for *N* seconds; no alerts will be posted. Example: `!!/block 600` blocks globally for 10 minutes.
- `!!/block <N> <room_id>` — Blocks SmokeDetector in the specific room for *N* seconds; no alerts will be posted there. Example: `!!/block 3600 89` blocks alerts in the Tavern for one hour.
- `!!/unblock` — Unblock SmokeDetector manually, resetting global block only.
- `!!/unblock <room_id>` — Unblock SmokeDetector manually in the specific room.
- `!!/invite <room_id> <roles separated by commas...>` - Temporarily invites SmokeDetector to the given room on the current site. Roles are the same as in `rooms.yml`.
- `!!/stopflagging` - An emergency measure to immediately disable all autoflagging. Once disabled, autoflagging can only be re-enabled by an Admin.

### Blacklists, watchlists, and the user-whitelist
#### User-blacklist and user-whitelist
The user-blacklist and user-whitelist are maintained *per SmokeDetector instance*. The SmokeDetector instances do not share these lists between themselves. Thus, if the SmokeDetector instance is switched, the new instance will only have a record of the entries on these lists which were added/removed while that instance was active.
##### User-blacklist
The user-blacklist is a dynamic list of users which will have any post of theirs reported by SmokeDetector anytime one of their posts is scanned. Users are primarily added to the user-blacklist when someone gives <code>tp<b>u</b></code> feedback to a post the user has authored. Users are automatically removed from the user-blacklist when `fp` feedback is given for a post they have authored. Users can also be explicitly added or removed with the following commands:
- `!!/addblu <profile_URL>` or `!!/addblu <user_ID> <site_name>` — Adds a user to the user-blacklist (this means that any post by this user will be reported when scanned).
- `!!/rmblu <profile_URL>` or `!!/rmblu <user_ID> <site_name>` — Removes a user from the user-blacklist.

##### User-whitelist
The user-whitelist is a list of users for which posts will not be reported if the *only detections* of the post are on the user's username. If there are other detections triggered, then the post will be reported with the username detections included. Users are added to the list if their post receives <code>fp<b>u</b></code> feedback. Users can also be explicitly added or removed with the following commands:
- `!!/addwlu <profile_URL>` or `!!/addwlu <user_ID> <site_name>` — Adds a user to the user-whitelist. For posts by this user, if the only detections triggered for the post are on the username, then those detections alone will not cause the post to be reported.
- `!!/rmwlu <profile_URL>` or `!!/rmwlu <user_ID> <site_name>` — Removes a user from the user-whitelist.

#### Detection blacklists and watchlists
For all `!!/blacklist-*` and `!!/watch*` commands: If you are a [blacklister](https://charcoal-se.org/smokey/Privileges#code-admin-aka-blacklister-ms) on metasmoke, your change will apply immediately, after brief checks by SmokeDetector or once CI passes, depending on the circumstances. If you are not a blacklister: A) a [pull request](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests) (PR) will be created for your additions to the lists, so the changes can be reviewed. B) you will not be allowed to execute `!!/unwatch` or `!!/unblacklist` commands. You will need to ping a blacklister to perform those commands, or manually submit a PR that performs the change.

All commands which add entries to one of these lists run the new entry through a variety of checks. If some checks are not passed, then a chat reply message is posted detailing what didn't pass. All such commands have a `-force` variant (i.e. append `-force` to the command; e.g. `!!/watch-force`), which will bypass these checks, except checks for actual duplicate entries, which are considered a hard error. You should not be in the habit of directly running the `-force` variant of the commands. Run the non `-force` version first to see what SmokeDetector says. If you have verified that you still want to add the entry, despite the issues SmokeDetector mentioned, then you can then edit your chat message to add `-force`, or post a new chat message with `-force`. Even very experienced users rarely go directly to using the `-force` version without running the command as a non- `-force` version first.

##### Non `-number` blacklists and watchlist
The non `-number` blacklists and watchlist are lists of regular expressions (regexes) which are used to test some or all of post bodies, post titles, and usernames for matching text. See the description of the command for adding entries to each list for a statement as to what the entries on that list are tested against.

Because these lists are regular expressions, make sure regex special characters are escaped (in particular, `.` characters should be escaped as `\.`) when not used as the special character. The regular expression variant that SmokeDetector uses is the [`regex` package](https://pypi.org/project/regex/). 

When adding to the blacklists, any entry in the watchlists which exactly matches what you're adding to the blacklist will be automatically removed from the watchlists. In other words, adding to the blacklist is assumed to be moving an entry from the watchlist to the blacklists, if it already existed on a watchlist.

The regexes for the keyword-blacklist and watchlist have `\b` prepended and appended to them prior to testing against post bodies, titles, and usernames. For both of those lists, the `i` and `s` flags are set (case insensitive and `.` matches anything). The other lists do not bookend the regexes with `\b` and only have the case insensitive flag, `i`, set. Note: the actual bookending begins the overall regex with `(?:^|\b|(?w:\b))` and ends it with `(?:\b|(?w:\b)|$)`. The documentation for the [`regex` package](https://pypi.org/project/regex/) briefly describes what the `w` (word) flag in the bookending does. [See "Unicode line separators" in the linked regex package documentation.]

- `!!/blacklist` — **This command has been deactivated.** Use one of the four specialized blacklist commands instead, which are shown below. If run, this command will post a help message in chat.
- `!!/blacklist-keyword <regex>` — Adds a regular expression pattern to the [list of bad keywords](https://github.com/Charcoal-SE/SmokeDetector/blob/master/bad_keywords.txt). Prior to being used, all regexes on this list automatically have `\b` added to the start and end of the regex. Regular expressions on this list are tested against post bodies, post titles, and usernames.
- `!!/blacklist-username <regex>` — Adds a regular expression pattern to the [username blacklist](https://github.com/Charcoal-SE/SmokeDetector/blob/master/blacklisted_usernames.txt).  Regexes on this list do *not* have `\b` added to the start and end of the regex. These regexes are tested only against usernames.
- `!!/blacklist-website <regex>` — Adds a regular expression pattern to the [website blacklist](https://github.com/Charcoal-SE/SmokeDetector/blob/master/blacklisted_websites.txt). Make sure regex special characters are escaped (in particular, `.` characters should be escaped as `\.`; e.g. `!!/blacklist-website example\.com`). Regexes on this list do *not* have `\b` added to the start and end of the regex. Regular expressions on this list are tested against post bodies, post titles, and usernames.
- `!!/watch <regex>` - Adds a regular expression pattern to the [watchlist](https://github.com/Charcoal-SE/SmokeDetector/blob/master/watched_keywords.txt) which is similar to the list of bad keywords (see `!!/blacklist-keyword` above), but with less strict criteria for what you can list.  The intent is that you can set up SmokeDetector to watch for something and be alerted when it actually happens.  Typical phrases to watch include domain names and phrases which occur in spam, but which have not been seen by metasmoke enough to actually blacklist (yet) or which don't meet the high spam-detection-accuracy criteria required of blacklisted items. The long version of this command is `!!/watch-keyword <regex>`. Prior to being used by SmokeDetector to test posts, all regexes on this list automatically have `\b` added to the start and end of the regex. Regular expressions on this list are tested against post bodies, post titles, and usernames.

##### `-number` blacklists and watchlist
The `-number` blacklist and watchlist are lists of numbers that are tested against post bodies, post titles, and usernames as text both verbatim and "normalized" (with everything but numbers removed).

- `!!/watch-number <number text>` - Adds a number to the [watched number list](https://github.com/Charcoal-SE/SmokeDetector/blob/master/watched_numbers.txt). The text may contain non-number characters and is tested verbatim against potential spam. In addition, it's tested "normalized", which is with both the watched number text and the post reduced to numbers.
- `!!/blacklist-number <number text>` — Adds a number to the [number blacklist](https://github.com/Charcoal-SE/SmokeDetector/blob/master/blacklisted_numbers.txt). The text may contain non-number characters and is tested verbatim against potential spam. In addition, it's tested "normalized", which is with both the blacklisted number text and the post reduced to numbers.

##### Commands applicable to both `-number` and non- `-number` blacklists and watchlists (excluding the user-blacklist and user-whitelist described above)

- `!!/unwatch <regex>` or `!!/unwatch <number text>` - Removes a previously-added regular expression from the watchlist and/or a number from the number watchlist. Only blacklisters can use this command; it will only accept an exact match to a regular expression in the watchlist and/or an exact match to a number in the number watchlist.
- `!!/unblacklist <regex>` or `!!/unblacklist <number text>` - Similar to `unwatch`, removes a previously-added regular expression from the blacklists and/or a number from the number blacklist. Only blacklisters can use this command. It will only accept an exact match to a regular expression in the blacklists and/or an exact match to a number in the number blacklist.
- `!!/approve <PR number>` - Only blacklisters can use this command. It allows you to approve without leaving the chat a pull request which was automatically created for watches/blacklists by non-blacklisters users.
- `!!/bisect <text>` - Test the text against all of the blacklist and watchlist entries and report which entries match.

## Privileged commands as reply

These commands require privileges and have to be posted as a reply to a message of SmokeDetector.

User-friendly syntax:

- use `spam` or `rude` or `abusive` or `offensive` for posts that should be flagged as such (equivalent to `tpu-`; see below)
- use `v`, `vand` or `vandalism` for posts that have been vandalised and the vandalism edit should be rolled back (equivalent to `tp-`)
- use `notspam` if the post should not be flagged (equivalent to `fp-`)

Complete list:

- `tp` or `true` — Marks a reported post as true positive.
- `tpu` or `trueu` — Marks a reported post as true positive and adds the poster to the blacklist.
- `fp` or `false` — Marks a reported post as false positive. Additionally removes the user from the blacklist, if that was the reason that the post was reported.
- `fpu` or `falseu` — Marks a reported post as false positive and adds the poster to the whitelist.
- `naa` — If the reported post is an answer, this command records it as NAA (Not an answer) in metasmoke.
- `ignore` — Makes SmokeDetector ignore a reported post.
- `delete`, `del`, `remove` or `gone` — Deletes a message of SmokeDetector. This has been disabled in CHQ for reports due to the reasons [listed below](#a-note-on-message-deletion). But if you really need to delete a report, use `sd delete-force`.
- `postgone` — Edits out the post link of a SmokeDetector report. If in CHQ, this should be used sparingly. 

## Silent mode and aliases

If you don't want SmokeDetector to reply when executing a command add a `-` sign at the end, for example, `fp-`. This is a good practice to cut down on chatroom clutter.  Note that SmokeDetector will always report any errors, even if the `-` is present. The hyphen can be placed after the command itself or after its parameter. The following commands support silent mode: replying to spam reports, managing black- and white-list, and managing chat notifications.

Also, some frequently used commands have one-letter aliases or convenient words that can be used instead:

|   Command | Alias of |
|----------:|----------|
|         f | fp-      |
|   notspam | fp-      |
|         k | tpu-     |
|      spam | tpu-     |
|      rude | tpu-     |
|     abuse | tpu-     |
|   abusive | tpu-     |
| offensive | tpu-     |
|         v | tp-      |
| vandalism | tp-      |
|         n | naa-     |

## A note on message deletion
Messages by SmokeDetector can be deleted within 2 minutes after they were posted by using the `del`, `remove`, or `gone` commands. After 2 minutes are up, SmokeDetector cannot delete its own messages in response to those commands, so any deletion after that window must be done by a moderator.

Messages will also be deleted in *Tavern on the Meta* and *SO Close Vote Reviewers*, or *Raiders of the Lost Downboat* if the relevant post is deleted or marked as false positive before the 2-minute window is up.

**Please note** that the usage of deletion commands is discouraged in Charcoal HQ. Generally, messages in CHQ are kept as a record of all reported posts for multiple reasons:

* While we *do* have metasmoke which acts as a mirror of all posts, it does go offline occasionally
* Some userscripts which run in chat (e.g. FIRE) use information from the chat reports to fetch the correct data from the API. 
* It allows for a second opinion on reports, even if one person has marked it as a false positive
* Seeing spam and abusive posts is an occupational hazard in CHQ; we aren't worried if the report contains something NSFW.

The `delete-force` command can be used if a report *really* needs to be deleted in Charcoal HQ.

## Shortcut commands

You can now use a shortcut to post a reply to one, two or three messages
at the same time, in this shape:

    sd cmd1
    sd cmd1 cmd2
    sd cmd1 cmd2 cmd3
    sd cmd1 cmd2 cmd3 cmd4
    sd cmd1 cmd2 cmd3 cmd4 cmd5

cmd1 will be invoked in the most recent message, cmd2 on the message
before that and cmd3 on the message before that, and so on.

It's also possible to skip a message. Replace a command with a `-` to skip a
message. For example, `sd - delete` skips the most recent message and
deletes the message before that one.

Smokey will reply to your shortcut command unless all commands have quiet
mode (like tp-) or just don't reply by default (like delete).

A few examples:

- `sd - delete` keeps the most recent message and deletes the one before that.
- `sd tp fp delete` marks the most recent message as tp, the one before that as fp, and deletes the one before that.

You can also put a digit in front of a command so that the command will apply as many times as the digit. A few examples:

- `sd 2tpu` = `sd tpu tpu`
- `sd 2tpu 3fpu` = `sd tpu tpu fpu fpu fpu`
- `sd 2- fp` = `sd - - fp`
