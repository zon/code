# Domain Logic

Domain logic encodes the real-world rules and processes the software solves — not the technical infrastructure needed to run it. It should be separated from implementation details, and kept concise and easy to understand.

For example, a messaging app HTTP handler:

```
func postMessage(ctx):
  user = getUser(ctx)
  message = parseMessage(ctx)
  channel = getChannel(message.channelID)
  upsertMessage(user, channel, message)
  publishEvent(channel, message)
```

This function contains no implementation detail — it calls lower-level functions to directly express domain requirements. HTTP handlers, command handlers, core logic loops, and event handlers should follow the same pattern: contain only domain logic, or delegate to something that does.