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

## Review

1. Create a `domain-functions.yaml` file in the repo root that lists all domain functions:

   ```yaml
   - file: handlers/users_handler.go
     functions:
     - getUser
     - postUser
   ```

   Each entry names the file and the domain functions within it. Only functions listed here are considered domain functions.

2. For each listed function, consider whether it is correct: does it contain no implementation details and have simple flow control?

3. Consider what the domain features of the app are and whether they are covered by clearly organized domain functions.
