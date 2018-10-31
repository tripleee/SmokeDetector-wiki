# Rooms

The Wiki page explains the following:
- File structure for the rooms.yml file
- `Commands` within the file that users are allowed to execute
- Message types (`msg_types`) and their description
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
### Glossary

- room id - room id for the rooms with which SmokeDetector interacts. For example: 12345:
commands - true/false boolean flag which determines if SmokeDetector listens for commands in the room
- msg_types - kinds of messages the room will receive, as described in the role_string types below
- role_string - 
   * `debug`: this is what Charcoal HQ or your main room would have set. Rooms with this set will receive startup messages and other debugging information (basically anything that would have previously been done with GlobalVars.charcoal_hq.send_message).
   * `all` or `site-<site>`: This dictates what sites will have their spam reported to the room. Rooms with all will receive reports from any site, while site-<site> (e.g site-askubuntu.com or site-codegolf.stackexchange.com) will receive reports from those particular sites.
  * `no-<reason>`: This room won't receive reports with the specified reason (e.g no-all-caps title)
  * `metatavern`: A special role I made for the Tavern on Meta, currently it just receives messages about blocks (for Town Halls).
- privileges - who can run privileged commands

To leverage these room roles, a flexible new function called `tell_rooms` has been added and replaces almost all of the previous `GlobalVars.special_rooms` or `GlobalVars.charcoal_hq` machinery:

```tell_rooms(message, (roles to have...), (roles not to have...))```
In essence, this broadcast the message to any room with one of the "roles to have," as long as it does not have any of the "roles not to have." An example:

```tell_rooms("Hai", ("all", "site-askubuntu.com"), ("no-offensive answer detected"))```
This will tell rooms with either `all` or `site-askubuntu.com` as long as they don't have `no-offensive answer detected`.

As a shorthand, there exists also `tell_rooms_with` and `tell_rooms_without` when there's only one role to have/not have:

```
tell_rooms("test", ("debug",), ())                   -> tell_rooms_with("debug", "test")
tell_rooms("meta tavern sucks", (), ("metatavern",)) -> tell_rooms_without("metatavern", "meta tavern sucks")
```
### Command system:
Defining a chat command is as simple as appending a decorator to your function:

```
@command(types..., reply=False, whole_msg=False, privileged=False, arity=None, aliases=None, give_name=False)
def <name_of_command>(...):
```

Most of the keyword arguments are not needed and can be omitted to have the default behavior. An explanation of each:

- `types...` - the most important part. These are a list of "functions" that are used to preprocess your arguments (and also define how many arguments your command takes). For instance, a command with `@command(int, int)` will take two strings and run them through int, coercing them to numbers. The most common "types" are Python's built-in `int` and `str` as well as chatcommunicate's `message`, which is used for reply commands that take a ChatExchange message object.

- `reply=<bool>` - if this is `False`, this command is a standard command (`!!/<name>`). If this is True, this is a subcommand (reply to a message, or use shorthand `sd commands...` notation). Subcommands are expected to have to take only one argument, and that argument will be the ChatExchange message object representing what message was replied to.

- `whole_msg=<bool>` - if this is `True`, the message containing the command will be passed in as the first argument. This is useful for retrieving data about who ran the command (`msg.owner`)

- `privileged=<bool>` - if this is `True`, only privileged users can execute this command.

- `arity=(<min arity>, <max arity>)` - an arity override, dictating the minimum and maximum arguments this function can take. Missing arguments will be `None`.

- `aliases=[strings...]` - other names this command can be referred to by (`true` vs `tp`, for instance).

- `give_name=<bool>` - if this is `True`, the alias used will be passed in as a keyword argument `alias_used`.

### Report data:
A nice bonus of all this is that I've made it so that `chatcommunicate` stores a dictionary mapping the message IDs of reports to a tuple containing the post URL and owner URL. This eliminates the ugly `fetch_post_url_from_msg_content` in most cases (if the message isn't in the dictionary for whatever reason, it'll run it automatically to parse it out). Instead, one can simply use the following to retrieve this information:

```get_report_data(message)```

where `message` is a ChatExchange message. Note that this dictionary is pickled along with last messages in the new `messageData.p`.

### Method call for the rooms YAML file

The `rooms.yml` file is called from within the `parse_room_config` method in `chatcommunicate.py` where the `site, site_rooms, roomid, privileges` are passed. 

The method itself is called within the object instance. 
