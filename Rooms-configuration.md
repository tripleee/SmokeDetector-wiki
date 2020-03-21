The Wiki page explains the following:
- File structure for the rooms.yml file
- Glossary of terms used in rooms.yml
- How to configure SmokeDetector for development

### File structure

The file is a yaml/yml markdown file which has 3 sections, one for each chat domain:
* stackexchange.com
* meta.stackexchange.com
* stackoverflow.com

Each section contains the following structure:

```
<chat host>:
  <room id>:
    commands: true/false,
    watcher: true/false,
    msg_types:
      - <role string...>
      - ...

    privileges: 
      - <user id...>
      - ...
```
### Glossary

- `<chat host>` - The domain in which the chat host is a sub-domain. Stack Exchange has 3 chat domains: chat.stackexchange.com, chat.meta.stackexchange.com, and chat.stackoverflow.com. The correct entries for `<chat host>` corresponding to these domains are `stackexchange.com`, `meta.stackexchange.com`, and `stackoverflow.com`.  Each chat server has independent rate limiting for the chat messages a single user can post. If you're making a test room into which the SmokeDetector user is going to be posting lots of messages, then please create the room on either `meta.stackexchange.com` or `stackoverflow.com`. SmokeDetector currently posts most of it's messages to the `stackexchange.com` chat server, which means it's the one that gets rate-limited the most.
- `<room id>` - room id for the rooms with which SmokeDetector interacts. For example: 12345.
- `commands` - true/false boolean flag which determines if SmokeDetector listens for commands in the room
- `watcher` - true/false boolean flag which determines if during the 2 minute chat edit/delete window, the report receives FP feedback from feedback in that chat room, or the SE post is deleted, then SmokeDetector will delete the report.
- `msg_types` - kinds of messages the room will receive, as described in the following role_string types:
   * Define which sites will have spam reports which are detected for at least one non-experimental reason posted to the room:
     * `all-sites`: Reports for all sites will be posted to the room.
     * `site-<domain>`: The room will receive reports about SE posts on the indicated site (e.g `site-askubuntu.com` or `site-codegolf.stackexchange.com`). There can be multiple `site-<domain>` lines to include more than one site. Meta sites are separate domains. If you want reports for both a main site and its meta site, then that's two entries.
     * `site-no-<domain>`: exclude a site's reports from being posted in the room (e.g. `site-no-stackoverflow.com`); normally used in combination with `all-sites`. There can be multiple `site-no-<domain>` lines to exclude more than one site. The `site-no-<domain>` settings affect all reports, including experimental reports. Meta sites are separate domains. If you want prevent reports for both a main site and its meta site, then that's two entries.
   * Define which sites will have spam reports which are detected for *only* [experimental reasons](https://github.com/Charcoal-SE/SmokeDetector/blob/master/globalvars.py#L79) posted to the room. From SmokeDetector's point of view, the experimental reasons are defined in `experimental_reasons` in the [globalvars.py](https://github.com/Charcoal-SE/SmokeDetector/blob/master/globalvars.py#L79) file. Experimental reasons are also separately defined on metasmoke, which restricts their maximum weight to 1 (ping a metasmoke developer, if those reasons should change).
     * `experimental-all-sites`: Experimental reports for all sites will be posted to the room.
     * `experimental-site-<domain>`: The room will receive experimental reports about SE posts on the indicated site (e.g `experimental-site-askubuntu.com` and/or `experimental-site-codegolf.stackexchange.com`). There can be multiple `experimental-site-<domain>` lines to include more than one site. Meta sites are separate domains. If you want experimental reports for both a main site and its meta site, then that's two entries.
   * `debug`: This is what Charcoal HQ or your main room would have set. Rooms with this set will receive startup messages and other debugging information (basically anything that would have previously been done with `GlobalVars.charcoal_hq.send_message`).
  * `delay`: introduces a 5 minute delay for reports; reports won't be posted if the post has been marked as false positive or deleted within the 5 minute window.
  * `dump`: used for Socket Science. Do not add this, unless you are a developer working on Socket Science. Rooms with the `dump` option *must* exist and not be deleted, or SmokeDetector will fail when becoming the "active" instance. If a room defined as `dump` becomes deleted, then you will probably want to ping the owners of any SmokeDetector instances which have gone off-line as a result. The quickest way to get those instances back will be to have the owners manually pull a new version of rooms.yml from GitHub with the `dump` removed. SmokeDetector instances that are in standby can be instructed to pull a newer version from GitHub through the status page on metasmoke.
  * `metasmoke`: Messages sent from metasmoke are forwarded to this room. This includes things like notification of the first feedback received for a report, CI success/failure which metasmoke is monitoring, etc. This is intended for additional information in Charcoal HQ.
  * `metatavern`: A special role created for the Tavern on Meta, currently it just receives messages about blocks (for Town Halls).
  * `no-<reason>`: This room won't receive reports with the specified reason (e.g `no-all-caps body`)
- `privileges` - who can run privileged commands in this room. There are two mutually exclusive formats to what this section can contain.  
  The first is a list of SE Network user IDs, one per line. Each user ID must be defined in [users.yml](https://github.com/Charcoal-SE/SmokeDetector/blob/master/users.yml).  
  The other format is `inherit`/`additional`:
  * `inherit`: indicates the list of permissions should be inherited from another room.
    * `site`: a "chat host" (see above) which contains the room from which to inherit.
    * `room`: the number of the room from which the list of permitted user IDs is to be inherited.
  * `additional`: a list of SE Network user IDs, one per line, which are privileged in this room in addition to those inherited from the `site`/`room` defined in `inherit`. If `inherit` is used, `additional` is available. When available, it is optional.

### Configuring rooms for development

During development, you probably want to avoid posting a bunch of reports and debug messages to our main rooms. In this case, you can set up a custom rooms.yml file to configure where Smokey will post messages. 

Simply create a file named `rooms_custom.yml`, and fill it in using the format described above. If you need a spare room to test in, we have one available for your use:

 - [Charcoal Test](https://chat.stackexchange.com/rooms/65945/charcoal-test)

If you are going to do testing which will result in the bot posting a lot of messages to chat, it's preferred that you reduce the possibility of SmokeDetector becoming rate-limited. You can do this by, preferably, using a different bot account for your testing. If you need to use the SmokeDetector account, please use a room on chat.stackoverflow.com, as that is the Stack Exchange chat server which gets the lightest traffic from SmokeDetector.

If you don't want Smokey to post any chat messages, you can simply leave the file blank.
