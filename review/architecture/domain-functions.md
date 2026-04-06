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

1. Read `domain-functions.yaml` in the repo root. It lists all domain functions:

   ```yaml
   - file: handlers/users_handler.go
     functions:
     - getUser
     - postUser
   ```

2. For each listed function, read the implementation and verify:
   - **Shallow flow control:** the function may have simple top-level conditions but avoids deep nesting — complex branching is delegated to lower-level functions
   - **No implementation details:** it contains no parsing, querying, formatting, error handling boilerplate, or other infrastructure concerns

3. Consider what the domain features of the app are and whether they are covered by clearly organized domain functions.
