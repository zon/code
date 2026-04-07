# Domain Functions

Domain functions encode the real-world rules and processes the software solves — not the technical infrastructure needed to run it. They should contain no implementation details and have simple flow control. Readability is the highest priority for a domain function. It should be possible to quickly understand everything a repo does just by reviewing it's domain functions.

For example, a messaging app HTTP handler:

```
func postMessage(ctx):
  user = getUser(ctx)
  message = parseMessage(ctx)
  channel = getChannel(message.channelID)
  upsertMessage(user, channel, message)
  publishEvent(channel, message)
  return message
```

## Designation

Read `domain-functions.yaml` in the repo root. This file records what is considered a domain function. Each major feature in the repo should be indexed in this file. The format is like this:

   ```yaml
   - feature: user management
     functions:
     - file: handlers/users_handler.go
       name: getUser
     - file: handlers/users_handler.go
       name: postUser
   ```

Consider if the list of major features and domain functions is correct. Do the major features of the repo match the file? Are the domain functions of each major feature correctly recorded in the file? Is each function really a domain function? Do some functions contain a mix of domain and implimentation logic?

## Major Features

A major feature is a user-facing capability that represents a distinct real-world concern the software addresses.

* **User-facing scope:** Something an end user would recognize as a distinct thing the app does — for example, "send a message", "manage users", "process payments", "handle authentication"
* **Bounded by domain, not infrastructure:**: It's defined by what the software does, not how — so "database access" or "HTTP routing" are not major features, but "message posting" or "channel management" are
* **Covered by one or a small set of domain functions:**: A major feature should have identifiable entry points (handlers, core logic loops, event handlers) that summarize its behavior at a high level
* **Independent enough to name:**: If you can describe it as a noun phrase a non-technical stakeholder would understand, it's likely a major feature

## Flow Control

Well structured domain functions are a little different than a typical function. They can be long and contain a wide variety of behavior. This complexity is acceptable if everything is well abstracted. Domain functions should summarize and encapsulate the logic of a major feature.

A major feature with unique shallow behavior should be covered by only one domain function. Major features that share behavior should share lower level domain functions. Major features with complex flow control should use lower level domain functions.

## Planning Improvements

When problems are discovered, plan specific solutions. Plan a new architecture that better meets our standards. Projects that alter domain functions should require matching updates to `domain-functions.yaml`.