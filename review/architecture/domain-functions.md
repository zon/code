# Domain Functions

Domain functions encode the real-world rules and processes the software solves — not the technical infrastructure needed to run it. They should contain no implementation details and have simple flow control.

For example, a messaging app HTTP handler:

```
func postMessage(ctx):
  user = getUser(ctx)
  message = parseMessage(ctx)
  channel = getChannel(message.channelID)
  upsertMessage(user, channel, message)
  publishEvent(channel, message)
```

This function contains no implementation detail — it calls lower-level functions to directly express domain requirements. HTTP handlers, command handlers, core logic loops, and event handlers should follow the same pattern.

## domain-functions.yaml

Where domain functions are found in a repo, create a `domain-functions.yaml` file in the repo root that lists them:

```yaml
- file: handlers/users_handler.go
  functions:
  - getUser
  - postUser
```

Each entry names the file and the domain functions within it. Only functions listed here are considered domain functions.
