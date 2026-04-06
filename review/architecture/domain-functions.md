# Domain Functions

Domain functions encode the real-world rules and processes the software solves — not the technical infrastructure needed to run it. They should contain no implementation details and have simple flow control. Readability is the highest priority for a domain function.

For example, a messaging app HTTP handler:

```
func postMessage(ctx):
  user = getUser(ctx)
  message = parseMessage(ctx)
  channel = getChannel(message.channelID)
  upsertMessage(user, channel, message)
  publishEvent(channel, message)
```

## Review

1. Read `domain-functions.yaml` in the repo root. It lists all domain functions grouped by feature — HTTP handlers, command handlers, core logic loops, and event handlers:

   ```yaml
   - feature: user management
     functions:
     - file: handlers/users_handler.go
       name: getUser
     - file: handlers/users_handler.go
       name: postUser
   ```

2. For each listed function, read the implementation and verify:
   - **It really is a domain function:** the function's purpose really is a domain concern
   - **Shallow flow control:** the function's flow control logic isn't too deep
   - **No implementation details:** if the function contains implementation logic that should be extracted

3. Consider what the domain features of the app are and whether they are covered by clearly organized domain functions.

When problems are discovered, plan specific solutions. Plan a new architecture that better meets our standards.