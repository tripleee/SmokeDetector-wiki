SocketScience is SmokeDetector's internal library to allow for direct communication between instances. We use this instead of a more obvious solution like websockets because it doesn't require any special considerations or configuration from hosts: whereas websockets would require hosts to open a port, SocketScience uses chat - which every instance is already connected to.

SocketScience has two primary use-cases:

 - Send some data to other instances
 - Do something with data that another instance has sent

These are, respectively, covered by the `send` and `register` methods.

## Send some data
In short: call `SocketScience.send(payload)`.

`payload` should be a `dict`. The keys of this dict are _message types_ - for example, you might have one message type for metasmoke up/down reports (`metasmoke_state`), and another for Smokey pings (`ping`). Do not use top-level dict keys for properties of your message; instead, assign another dict to the key for the relevant message type in the top level dictionary.

**Bad:**
```python
SocketScience.send({'location': GlobalVars.location, 'time': time.time()})
```

**Good:**
```python
SocketScience.send({'ping': {'location': GlobalVars.location, 'time': time.time()}})
```

This construct is important, because it's what the receiving end relies on to work.

## Receive some data
When SmokeDetector starts, you should register a callback with SocketScience for the message type you want to respond to. To do this, call `SocketScience.register(prop, cb)` - `prop` is the relevant message type, and `cb` is a method that SocketScience will call when a message of that type is received.

For example, if you want to respond to ping events by telling Charcoal HQ which instance pinged and when (this is a terrible idea and I will hunt you down if you do it, but it serves as an example):

```python
def handle_ping(data):
    chatcommunicate.tell_rooms_with('debug', '{} pinged at {}'.format(data['location'], data['time']))

SocketScience.register('ping', handle_ping)
```

As that example indicates, your callback will be passed a single parameter, containing the contents of the data dict for _that message type only_.

## Full example
Say you want to create a new message type `beverages` that makes every instance serve a user a `!!/coffee` or `!!/tea` instead of just one (this is also a terrible idea).

```python
# ws.py (most of file omitted)
def serve_beverage(data):
    chatcommunicate.tell_rooms_with('debug', ':{} *serves another {}*'.format(data['message_id'],
                                                                              data['beverage_type']))

SocketScience.register('beverage', serve_beverage)
```

```python
# chatcommands.py (relevant sections only)
@command(whole_msg=True)
def coffee(msg):
    # rest of command omitted
    SocketScience.send({'beverage': {'message_id': msg.id, 'beverage_type': 'coffee'}})

@command(whole_msg=True)
def tea(msg):
    # rest of command omitted
    SocketScience.send({'beverage': {'message_id': msg.id, 'beverage_type': 'tea'}})
```