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

```<chat host>:
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

- room id - room id for the rooms with which SmokeDetector interacts. For example: 12345:
commands - true/false boolean flag which determines if SmokeDetector listens for commands in the room
- msg_types - kinds of messages the room will receive, as described in the role_string types below
- role_string - 
   * `debug`: this is what Charcoal HQ or your main room would have set. Rooms with this set will receive startup messages and other debugging information (basically anything that would have previously been done with GlobalVars.charcoal_hq.send_message).
   * `all` or `site-<site>`: This dictates what sites will have their spam reported to the room. Rooms with all will receive reports from any site, while site-<site> (e.g site-askubuntu.com or site-codegolf.stackexchange.com) will receive reports from those particular sites.
  * `no-<reason>`: This room won't receive reports with the specified reason (e.g no-all-caps title)
  * `metatavern`: A special role created for the Tavern on Meta, currently it just receives messages about blocks (for Town Halls).
  * `delay`: Introduces a 5 minute delay for reports; reports won't be posted if the post has been marked as false positive or deleted within the 5 minute window
- privileges - who can run privileged commands

### Configuring rooms for development

During development, you probably want to avoid posting a bunch of reports and debug messages to our main rooms. In this case, you can set up a custom rooms.yml file to configure where Smokey will post messages. 

Simply create a file named `rooms_custom.yml`, and fill it in using the format described above. If you need a spare room to test in, we have one available for your use:

 - [Charcoal Test](https://chat.stackexchange.com/rooms/65945/charcoal-test)


If you don't want Smokey to post any chat messages, you can simply leave the file blank.
