# Coding Standards

## Deep Modules

Modules and classes should hide complexity behind simple interfaces. A deep module has a lot of functionality but a narrow, easy-to-use surface area.

- Expose only what callers need; keep implementation details private
- A complex subsystem should be accessible through a small, intuitive API
- Prefer fewer, more powerful abstractions over many fine-grained ones that leak internals

The goal: callers should not need to understand *how* a module works, only *what* it does.