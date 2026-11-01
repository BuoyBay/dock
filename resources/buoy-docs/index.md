---
title: "Dock"
summary: "Opt into macOS Dock badges and explicitly owned attention requests."
category: "Overview"
order: 0
keywords: ["dock"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# Dock

The dock package adds application-wide badge labels and cancellable user-attention requests. Importing it and checking support are inert. Badges belong to the application rather than to an individual window.

## Platform support

DockSupported requires a macOS desktop process and is false on Windows, Linux, and headless processes. Use Dock effects from the main thread of a real desktop app. Unsupported operations throw UnsupportedOperationException.

## Start reading

- [Getting started](getting-started.md) walks through installation and a complete example.
- [API reference](api.md) describes public symbols, state, errors, and ownership.

## Scope

Use SetDockBadgeCount after an explicit application state change. Zero clears a count. Keep DockAttentionRequest alive while attention is useful and Close it in Finally. Informational attention can stop on its own; token ownership does not imply the icon is still bouncing. Critical requests require cancellation or application activation.
