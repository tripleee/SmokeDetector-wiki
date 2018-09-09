SmokeDetector can restart into one of three different statuses:

* Standard mode
* Standby mode
* Reverted mode

## Standby mode

SmokeDetector can be run in standby mode as a backup copy, just in case the main Smokey breaks down.
While in Standby mode, SmokeDetector won't make any reports in chat, send posts to Metasmoke or listen
to commands.

If the main Smokey fails to respond to status pings for a few minutes, metasmoke will automatically choose a standby instance to failover. Any instance can also be manually failovered from the [status page](https://metasmoke.erwaysoftware.com/status) (note: code admin privileges required). The failovered instance will then begin to take over the normal duties of the main SmokeDetector.

> SmokeDetector host note: you can run `python3 nocrash.py standby` to start Smokey directly into Standby mode.

## Reverted Mode

SmokeDetector switches to Reverted Mode when it detects that errors occur in the running version: it goes back to a previous version. When SmokeDetector is in reverted mode, any privileged user can switch back to the master branch using the `!!/master` command when that's necessary.
