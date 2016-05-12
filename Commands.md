This wiki page contains a list of commands and their explanation.

# Commands for everyone

These commands can be executed by everyone.

 - `!!/alive` - Replies a random message taken from a list so you can see that SmokeDetector is still running.
 - `!!/status` - Shows the UTC date when SmokeDetector started running.
 - `!!/rev` or `!!/ver` - Shows the running Git revision.
 - `!!/help` - Shows a small help message about SmokeDetector.
 - `!!/apiquota` - Shows the remaining API quota of SmokeDetector.
 - `!!/queuestatus` - Shows the queue status of BodyFetcher.
 - `!!/blame` - Chooses randomly from a list of people who have talked recently in the room.
 - `!!/lick`, `!!/wut`, `!!/coffee`, `!!/tea`, and `!!/brownie` - better versions of `!!/alive`.
 - `!!/location` - Replies with the current location, as set in the `config` file
 - `!!/test <string>` - Runs `<string>` against the filter as if it appeared in a question body.
 - `!!/whoami` - Replies with the bot's user id for that site
 - `!!/amiprivileged` - Lets you know if you are in the list of privileged users

# Commands as reply for everyone

- `why` - Shows the reason that SmokeDetector caught a post.  
  Note that `why` data is only kept for the last 50 reports.

# Privileged commands

These commands require privileges.
<!-- These were not in any order. Recommend most-used/useful up top. -->

 - `!!/report <post URL 1> [<post URL 2> [...]]` - Makes SmokeDetector report a specific post/multiple specific posts in Charcoal HQ and Tavern on the Meta. The originator of each post will be added to the blacklist. Maximally 5 at a time.
 - `!!/allspam <user URL>` - To be used if a spammer has many posts so you don't have to use `!!/report`. This command posts a message about the user in all applicable rooms.  Note that this command does NOT auto-TPU anything, for various reasons. It has an alias, `!!/reportuser <user URL>`
 - `!!/addwlu <profile_URL>` or `!!/addwlu <user_ID> <site_name>` - Adds a user to the whitelist (this means that if the username for that user matches one of the regexes, this will be ignored).
 - `!!/rmwlu <profile_URL>` or `!!/rmwlu <user_ID> <site_name>` - Removes a user from the whitelist.
 - `!!/addblu` (same syntax as `!!/addwlu`) - Adds a user to the blacklist (this means that any post of this user will be reported).
 - `!!/rmblu` (same syntax as `!!/rmwlu`) - Removes a user from the blacklist.
 - `!!/clearbl` - Removes all users from the blacklist.
 - `!!/reboot` - Reboots SmokeDetector.
 - `!!/stappit` - Stops SmokeDetector.
 - `!!/pull` - Pulls new revisions from GitHub.
 - `!!/master` - When SmokeDetector enters reverted mode, use this command to go back to the `master` branch.
 - `!!/errorlogs <N>` - Shows the last *N* lines of the error logs.
 - `!!/block <N>` - Blocks SmokeDetector globally for *N* seconds; no alerts will be posted. Example: `!!/block 600` blocks globally for 10 minutes.
 - `!!/block <N> <room_id>` - Blocks SmokeDetector in the specific room for *N* seconds; no alerts will be posted there. Example: `!!/block 3600 89` blocks alerts in the Tavern for one hour.
 - `!!/unblock` - Unblock SmokeDetector manually, resetting global block only.
 - `!!/unblock <room_id>` - Unblock SmokeDetector manually in the specific room.
 - `!!/notify <chatroom_ID_number> <site_domain>` - Tells SmokeDetector to ping you, in the given chatroom, when a post is reported on the given site.  
  Example:  `!!/notify 89 parenting.stackexchange.com-`  
  Note: Please use the squelch suffix (`-`) and avoid spamming the chat room with too many requests. See [this chat message](http://chat.meta.stackexchange.com/transcript/message/4157790#4157790) and the surrounding context.
 - `!!/unnotify <chatroom_ID_number> <site_domain>` - Cancels the previously set notification.  Also accepts the silent mode suffix&nbsp;(`-`).
 - `!!/willibenotified <chatroom_ID_number> <site_domain>` - Reports whether you will be pinged, in the given room, about spam on the given site.
 - `!!/allnotificationsites <chatroom_ID_number>` - Shows all sites that you will be pinged for in the given room.


# Privileged commands as reply

These commands require privileges, and have to be posted as a reply to a message of SmokeDetector.

User-friendly syntax: 

- use `spam` or `rude` or `abusive` or `offensive` for posts that should be flagged as such 
- use `notspam` if the post should not be flagged

These commands are equivalent to `tpu-` and `fp-`, respectively: see below.

Complete list:

 - `tp` or `true` - Marks a reported post as true positive.
 - `tpu` or `trueu` - Marks a reported post as true positive and adds the poster to the blacklist.
 - `fp` or `false` - Marks a reported post as false positive.
 - `fpu` or `falseu` - Marks a reported post as false positive and adds the poster to the whitelist.
 - `naa` - If the reported post is an answer, this command records it as NAA (Not an answer) in metasmoke.
 - `ignore` - Makes SmokeDetector ignore a reported post.
 - `delete`, `del`, `remove` or `gone` - Deletes a message of SmokeDetector.
 - `postgone` - Edits out the post link of a SmokeDetector report.

# Silent mode and aliases

If you don't want SmokeDetector to reply when executing a command, add a `-` sign at the end, for example `fp-`. This is a good practice to cut down on chatroom clutter.  Note that SmokeDetector will always report any errors, even if the `-` is present.

Also, some frequently used commands have one-letter aliases:

 - `f` is the same as `fp-`
 - `k` is the same as `tpu-`
 - `n` is the same as `naa-`

Finally 

# Shortcut commands

You can now use a shortcut to post a reply to one, two or three messages
at the same time, in this shape:

    sd cmd1
    sd cmd1 cmd2
    sd cmd1 cmd2 cmd3
    sd cmd1 cmd2 cmd3 cmd4
    sd cmd1 cmd2 cmd3 cmd4 cmd5

cmd1 will be invoked in the most recent message, cmd2 on the message
before that and cmd3 on the message before that, and so on.

It's also possible to skip a message. Replace a command by a - to skip a
message. For example, `sd - delete` skips the most recent message and
deletes the message before that one.

Smokey will reply to your shortcut command, unless all commands have quiet
mode (like tp-) or just don't reply by default (like delete).

A few examples:

- `sd - delete` keeps the most recent message and deletes the one before that.
- `sd tp fp delete` marks the most recent message as tp, the one before that as fp, and deletes the one before that.

You can also put a digit in front of a command so the command will apply as many times as the digit. A few examples:

- `sd 2tpu` == `sd tpu tpu`
- `sd 2tpu 3fpu` == `sd tpu tpu fpu fpu fpu`
- `sd 2- fp` == `sd - - fp`