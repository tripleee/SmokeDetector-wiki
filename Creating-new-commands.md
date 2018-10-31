> This document covers how to create a new command, which basically means that is it a guide on `chatcommands.py`.

## 1. The perfect function

Define a function that is the same name as the command you want. If you want a command called `!!/createcommand`, you would write a function like this:

```python
@command()
def createcommand():
    return None
```

This command will do nothing. The function returns a string or `None`. If a string is returned, the string will be posted to chat. If `None` is returned, nothing will be posted to chat. You can put anything (read: the thing you want to do with this command) inside the function body.

## 2. Configuration of the `@command()`

Supported arguments:

**command**(*privileged=False*, *whole_msg=False*, *arity=None*, *aliases=[]*, *give_name=False*, *reply=False*)

To tweak the settings of your command, you have to edit the parameters inside `@command()`

- `whole_msg` - `True` or `False`: If `True`, you can include a parameter `msg` in your function. `msg` is a [ChatExchange](https://github.com/Manishearth/ChatExchange) message object. The default is `False`. The `msg` argument will always come first, if there is any other argument.

  Example:
  ```python
  @command(whole_msg=True)
  def createcommand(msg):
      return None
  ```

- `privileged` - `True` or `False`: If `True`, the user has to have [SD privileges](https://github.com/Charcoal-SE/SmokeDetector/wiki/Privileges#smokedetector-privileges-sd) to execute the command. The default is `False`.

  Example:
  ```python
  @command(privileged=True)
  def createcommand():
      return None
  ```

  You can also manually return the non-privileged response if you want:

  ```python
  @command(whole_msg=True)
  def createcommand(msg):
    if not is_privileged(msg.owner, msg.room):
      raise CmdException(GlobalVars.not_privileged_warning)
    return "Hello"

- `aliases` - an array of strings: In addition to the function name, the function will be executed if the command is equal to the alias.

  Example:
  ```python
  @command(aliases=['create-command', 'create_command'])
  def createcommand():
      return None
  ```
  The function will be executed with `!!/create-command`, `!!/create_command` or`!!/createcommand`.

- Command arguments - Type (`int`, `str` etc): The arguments of the command and the type, So `!!/foo bar` would translate to `@command(str)` and `!!/foo 1 bar` would be `@command(int, str)`.

  Example:
  ```python
  @command(str, int)
  def createcommand(name, args):
      return None
  ```
  The command type will translate to an argument.

  **NOTE**: When mixing with `whole_msg`, the `msg` argument will come first while the `whole_msg` argument will come after the command arguments, like

  ```python
  @command(str, whole_msg=True)
  def createcommand(msg, name):
      return None
  ```

- `give_name` - `True` or `False`: When `True`, a parameter called `alias_used` can be added, which shows which alias was used. See [L287 of `chatcommands.py`](https://github.com/Charcoal-SE/SmokeDetector/blob/3fae27a1f1a2fc5053c438047a55359f963eb013/chatcommands.py#L287). This parameter will be supplied as a keyword argument.

- `arity` - tuple of `int`s: Allows the number of command argument to be in the range. (eg `arity=(0,2)`) allows the command to have 0, 1 or 2 arguments. Absent values will be provided as `None`.

- `reply` - `True` or `False`: Defaults to `False`. If `True`, the command will only execute if it is a reply or by `sd` feedback, not `!!/`. If `False`, the command will only execute if `!!/` is used.

## 3. Post something

To post data that is what you expected, simply execute `return "some message"`

If you encounter an error, you can raise a `CmdException` with a string as the error message. The string will be sent to chat. The difference is that with `return`, the response can be suppressed if the command is issued in "silent mode" (ends with an additional hyphen, e.g. `!!/command-`). With `raise CmdException`, the response suppression will be ignored and Smokey will always response with the string in the exception.

```python
@command()
def somerandomcommand():
    if True:
        raise CmdException("Error: this error will be fixed in 6 to 8 weeks! HAHA")
    return None
```

If you want to send a message to all the rooms that Smokey is running in, use `tell_rooms`:

```python
tell_rooms("A message")
```

The longhand version of this (which allows additional configuration) is:

```python
tell_rooms(message, (roles to have...), (roles not to have...))
```

It's recommended that you send messages to rooms that are interested in debug messages, instead of spamming all rooms. You can use `tell_rooms_with`:

```python
tell_rooms_with('debug', "A debug message")
```

You can also use `tell_rooms_without` to post to all rooms without a specific role:

```python
tell_rooms_without("metatavern", "Tavern on the Meta sucks")
```

