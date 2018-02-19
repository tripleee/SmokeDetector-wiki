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

To tweak the settings of your command, you have to edit the parameters inside `@command()`

- `whole_msg` - `True` or `False`: If `True`, you can include a parameter `msg` in your function. `msg` is a [ChatExchange](https://github.com/Manishearth/ChatExchange) message object. The default is `False`.

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

- `give_name` - `True` or `False`: When `True`, a parameter called `alias_used` can be added, which shows which alias was used. See [L287 of `chatcommands.py`](https://github.com/Charcoal-SE/SmokeDetector/blob/3fae27a1f1a2fc5053c438047a55359f963eb013/chatcommands.py#L287).

- `arity` - tuple of `int`s: Allows the number of command argument to be in the range. (eg `arity=(0,2)`) allows the command to have 0, 1 or 2 arguments.

- `reply` - `True` or `False`: Defaults to `False`. If `True`, the command will only execute if it is a reply or by `sd` feedback, not `!!/`. If `False`, the command will only execute if `!!/` is used.

## 3. Post something

To post data that is what you expected, simply execute `return "your message here"`

If you encounter an error, you can raise a `CmdException` with a string as the error message. The string will be sent to chat.

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



