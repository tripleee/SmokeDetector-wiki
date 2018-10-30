# Rooms

The Wiki page explains the following:
- File structure for the rooms.yml file
- Commands within the file that users are allowed to execute
- Message types and their description
- Chat communication functionality

### File structure

The file is a yaml/yml markdown file which contains the following structure:

```<chat host>:
  <room id>:
    commands: true/false,
    msg_types:
      - <role string...>
      - ...

    privileges: 
      - <user id...>
      - ...
```

room id
commands
msg_types
role_string
privileges
user id


This compactly defines all of the rooms SmokeDetector interacts with. The commands and privileges keys, as you might suspect, define whether SmokeDetector listens for commands in the room and who can run privileged commands respectively. The only thing that's new, really, is msg_types. The msg_types, in essence, defines the kinds of messages the room will receive. A few of the special ones:

debug: this is what Charcoal HQ or your main room would have set. Rooms with this set will receive startup messages and other debugging information (basically anything that would have previously been done with GlobalVars.charcoal_hq.send_message).

all or site-<site>: This dictates what sites will have their spam reported to the room. Rooms with all will receive reports from any site, while site-<site> (e.g site-askubuntu.com or site-codegolf.stackexchange.com) will receive reports from those particular sites.

no-<reason>: This room won't receive reports with the specified reason (e.g no-all-caps title)

metatavern: A special role I made for the Tavern on Meta, currently it just receives messages about blocks (for Town Halls).

experimental: Only rooms with this role will receive reports consisting of only experimental reasons (watchlist).