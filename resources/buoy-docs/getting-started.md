---
title: "Dock getting started"
summary: "Install dock and use its core API with explicit application ownership."
category: "Guides"
order: 10
keywords: ["dock", "installation", "example"]
related: ["index.md", "api.md", "typed-api.md"]
---

# Dock getting started

## Install and import

Copy the sealed `dock-0.1.0.buipkg` archive into your project `packages/` directory, or install a source/registry dependency named `dock` using BPM and sync it. Then use `Import dock`. The archive includes this documentation as package resources.

Use a consuming source filename such as `main.bui`; a local module named exactly like the package shadows its import.

## Complete usage example

The example is compiler-checked as a complete Buoy module. Functions and Subs are intended to be called from the consuming app at the appropriate user action or lifecycle event.

```buoy
Import dock

Sub UpdateUnreadBadge(unread As Integer)
    If Not DockSupported() Then Return
    SetDockBadgeCount(unread, 99)
End Sub
```

## Integrate with the application

Use SetDockBadgeCount after an explicit application state change. Zero clears a count. Keep DockAttentionRequest alive while attention is useful and Close it in Finally. Informational attention can stop on its own; token ownership does not imply the icon is still bouncing. Critical requests require cancellation or application activation.

## Handle failures and unsupported targets

Negative counts and maximum values below one are rejected before badge changes. Native operations validate main-thread access. Close is idempotent. Worker-thread destruction queues native cleanup onto the main thread, so explicit Close while the run loop is alive remains preferable.

DockSupported requires a macOS desktop process and is false on Windows, Linux, and headless processes. Use Dock effects from the main thread of a real desktop app. Unsupported operations throw UnsupportedOperationException.

Return to the [overview](index.md) or consult the [API reference](api.md).
