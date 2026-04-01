# Domain Logic

Domain logic is the part of a software application that encodes the real-world rules, processes, and calculations governing how data is created, stored, and changed. It is the "brain" of the application, representing the actual problem the software is solving rather than the technical infrastructure needed to run it.

Code should handle domain logic and implementation separately. Code that performs domain logic in particular should be concise, clearly structured, and easy to understand.

Say you were coding a messaging app for example. The messaging domain requirements might be that messages come from users, are posted to channels, and sent as an event for real-time notification. Such an app might have a HTTP handler like this:

```
func postMessage(ctx):
  user = getUser(ctx)
  message = parseMessage(ctx)
  channel = getChannel(message.channelID)
  upsertMessage(user, channel, message)
  publishEvent(channel, message)
```

This function doesn't have any implementation detail. It just calls lower level functions to directly meet domain logic requirements. All domain logic should be isolated like this so we can easily see what apps are doing without noisy implementation details.

HTTP endpoint handlers, command handlers, core logic loops, event handlers, these are parts of the app that are often close to domain logic concerns. These functions should usually only contain domain logic themselves or should call something else to handle domain logic cleanly.