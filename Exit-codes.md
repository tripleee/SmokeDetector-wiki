SmokeDetector is usually run via `nocrash.py`, which takes care of recovering when the bot crashes. It also handles various minor exceptional tasks between restarts based on the exit code returned from the program. These exit codes are documented here.

Only exit codes that have some special action attached to them are in this document. Unused exit codes incur a 5-second sleep followed by a restart - if you want to define a new exit code for some other purpose, you'll need to add it to `nocrash.py`.

Exit code | Action
----------|--------
 3        | `!!/pull` - runs `git checkout deploy`, `git pull`, and `git submodule update`, in that order. Does nothing on Windows.
 4        | Crash code - increments a crash counter, and enters reverted mode if the crash count is too high (i.e. the commit is bad).
 5        | Straight reboot - resets the restart count, and reboots Smokey.
 6        | Stop code - fully exits the program and returns control to the caller.
 7        | Standby - adds `standby` to the persistent argument list, and restarts Smokey in standby mode.
 8        | `!!/master` - runs `git checkout deploy` and resets restart and crash counter before rebooting Smokey.
 10       | Socket failure - sleeps for 5 seconds before rebooting to let the network stabilize.