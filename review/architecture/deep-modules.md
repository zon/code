# Deep Modules

A deep module is a software component that provides powerful, complex functionality while exposing a simple, narrow public interface. Is the code effectively broken down into deep modules?

- Does this module have a well-defined single area of responsibility?
- Is there other code that should be replaced with calls to this module?
- Is the public interface simple relative to the functionality it provides? (few parameters, intuitive names, minimal concepts a caller must understand)
- Does the interface hide implementation details, or does it leak internal state, types, or decisions that callers shouldn't need to know about?