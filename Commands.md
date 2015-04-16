This wiki page contains a list of commands and their explanation.

# Commands for everyone

These command can be executed by everyone.

 - `!!/alive` - Replies a random message taken from a list so you can see that SmokeDetector is still running.
 - `!!/status` - Shows the UTC date when SmokeDetector started running.
 - `!!/rev` - Shows the running Git revision.
 - `!!/help` - Shows a small help message about SmokeDetector.
 - `!!/apiquota` - Shows the remaining API quota of SmokeDetector.
 - `!!/queuestatus` - Shows the queue status of BodyFetcher.
 - `!!/so2015` - Displays information about the [2015 Stack Overflow Election](http://stackoverflow.com/election/6).
 - `!!/blame` - Only active in [The Tavern](http://chat.meta.stackexchange.com/rooms/89/tavern-on-the-meta), chooses randomly from a list of people who have talked recently in the room.
 - `!!/lick` - better version of `!!/alive`
 - `!!/wut` another better version of `!!/alive`

# Privileged commands

These commands require privileges.

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
 - `!!/block <N>` - Blocks SmokeDetector for *N* seconds; no alerts will be posted.
 - `!!/unblock` - Unblock SmokeDetector manually.

# Privileged commands as reply

These commands require privileges, and have to be posted as a reply to a message of SmokeDetector.

 - `tp` or `true` - Marks a reported post as true positive.
 - `tpu` or `trueu` - Marks a reported post as true positive and adds the poster to the blacklist.
 - `fp` or `false` - Marks a reported post as false positive.
 - `fpu` or `falseu` - Marks a reported post as false positive and adds the poster to the whitelist.
 - `ignore` - Makes SmokeDetector ignore a reported post.
 - `delete`, `remove` or `gone` - Deleted a message of SmokeDetector.