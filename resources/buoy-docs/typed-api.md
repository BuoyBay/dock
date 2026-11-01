---
title: "dock typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["DockAttentionRequest"]
dependencies: []
symbols: ["DockAttentionRequest"]
related: ["api.md", "getting-started.md", "index.md"]
---

# dock typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## Dock functions

### DockSupported

`Public Function DockSupported() As Boolean`

Dock effects are opt-in and available only in a macOS desktop process.

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

### DockBadge

`Public Function DockBadge() As String`

No parameters.

#### Returns

| Type |
| --- |
| `String` |

### SetDockBadge

`Public Sub SetDockBadge(label As String)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `label` | `String` | `ByVal` | Required |

Returns: no value.

### SetDockBadgeCount

`Public Sub SetDockBadgeCount(count As Integer, maximum As Integer = 99)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `count` | `Integer` | `ByVal` | Required |
| `maximum` | `Integer` | `ByVal` | `99` |

Returns: no value.

## DockAttentionRequest

`Public Class DockAttentionRequest`

Keep this handle and Close it on the main thread when attention is no longer needed.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `IsClosed` | `Boolean` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(critical As Boolean = False)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `critical` | `Boolean` | `ByVal` | `False` |

Returns: no value.

### Close

`Public Sub Close()`

No parameters.

Returns: no value.

### Destructor

`Public Sub Destructor()`

No parameters.

Returns: no value.
