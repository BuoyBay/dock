---
title: "Dock API"
summary: "Opt into macOS Dock badges and explicitly owned attention requests."
category: "Reference"
order: 20
keywords: ["dock", "API", "lifecycle"]
symbols: ["DockSupported", "DockBadge", "SetDockBadge", "SetDockBadgeCount", "DockAttentionRequest", "DockAttentionRequest.IsClosed", "DockAttentionRequest.Close"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# Dock API

Import the `dock` package. Constructors below use the class name; invoke them with `New`. Listed members are public client APIs; native declarations and trampoline helpers are implementation details.

## Public surface

| Symbol | Contract |
| --- | --- |
| `DockSupported() As Boolean` | Checks whether macOS desktop Dock integration is available. |
| `DockBadge() As String` | Returns the current label, or an empty string when clear. |
| `SetDockBadge(label As String)` | Replaces the application-wide label; an empty string clears it. |
| `SetDockBadgeCount(count As Integer, maximum As Integer = 99)` | Displays count, clears zero, or displays maximum followed by + when exceeded. |
| `DockAttentionRequest(critical As Boolean = False)` | Starts and owns one native attention request; informational by default. |
| `DockAttentionRequest.IsClosed As Boolean` | Reports whether this object has retired its token, not whether the Dock is visibly bouncing. |
| `DockAttentionRequest.Close()` | Idempotently retires this request and schedules native cancellation as required. |

## Ownership and timing

Use SetDockBadgeCount after an explicit application state change. Zero clears a count. Keep DockAttentionRequest alive while attention is useful and Close it in Finally. Informational attention can stop on its own; token ownership does not imply the icon is still bouncing. Critical requests require cancellation or application activation.

## Errors and result interpretation

Negative counts and maximum values below one are rejected before badge changes. Native operations validate main-thread access. Close is idempotent. Worker-thread destruction queues native cleanup onto the main thread, so explicit Close while the run loop is alive remains preferable.

## Platform behavior

DockSupported requires a macOS desktop process and is false on Windows, Linux, and headless processes. Use Dock effects from the main thread of a real desktop app. Unsupported operations throw UnsupportedOperationException.

See the [complete usage example](getting-started.md) and the [package overview](index.md).

[Full typed API: properties, parameters, defaults, and returns](typed-api.md)
