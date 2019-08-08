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
   * Define which sites will have spam reports posted to the room:
     * `all`: Reports for all sites will be posted to the room.
     * `site-<site>`: The room will receive reports about SE posts on the indicated site (e.g `site-askubuntu.com` or `site-codegolf.stackexchange.com`). There can be multiple `site-<site>` lines to include more than one site.
     * `site-no-<site>`: exclude a site's reports from being posted in the room (e.g. `site-no-stackoverflow.com`); normally used in combination with `all`. There can be multiple `site-no-<site>` lines to exclude more than one site.
   * `debug`: This is what Charcoal HQ or your main room would have set. Rooms with this set will receive startup messages and other debugging information (basically anything that would have previously been done with GlobalVars.charcoal_hq.send_message).
  * `delay`: introduces a 5 minute delay for reports; reports won't be posted if the post has been marked as false positive or deleted within the 5 minute window.
  * `dump`: used for Socket Science. Do not add this, unless you are a developer working on Socket Science. Rooms with the `dump` option *must* exist and not be deleted, or SmokeDetector will fail when becoming the "active" instance. If a room defined as `dump` becomes deleted, then you will probably want to ping the owners of any SmokeDetector instances which have gone off-line as a result. The quickest way to get those instances back will be to have the owners manually pull a new version of rooms.yml from Github with the `dump` removed. SmokeDetector instances that are in standby can be instructed to pull a newer version from GitHub through the status page on metasmoke.
  * `experimental`: Without this option, reports detected for *only* experimental reasons will not be posted in the chatroom. However, this option is all-or-nothing. If `experimental` is included, then *all* reports for *all sites* which are detected for only experimental reasons will be posted in the room. In other words, it ignores the `site--<site>` and `site-no-<site>` settings. From SmokeDetector's point of view, the experimental reasons are defined in `experimental_reasons` in the [globalvars.py](https://github.com/Charcoal-SE/SmokeDetector/blob/master/globalvars.py#L69) file. Experimental reasons are also separately defined on metasmoke (ping a metasmoke developer, if those should change).
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


If you don't want Smokey to post any chat messages, you can simply leave the file blank.
