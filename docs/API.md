# dock · 0.1.0

Opt-in macOS Dock badges and cancellable attention requests. `Import dock`.
No Dock effect occurs merely by importing the package or asking `DockSupported()`.

| API | Behavior |
| --- | --- |
| `DockSupported() As Boolean` | macOS desktop-process capability; false on Windows/Linux or in headless mode. |
| `DockBadge() As String` | Current badge, empty if none. |
| `SetDockBadge(label)` | Set a custom badge; empty clears it. |
| `SetDockBadgeCount(count, maximum = 99)` | Zero clears; large counts display `99+` (or the chosen maximum). Negative counts are rejected. |
| `New DockAttentionRequest(critical = False)` | Request attention and retain its cancellation token. Informational is the default. |
| `request.Close()` / `request.IsClosed` | Idempotently cancel the request / inspect token ownership. |

Call all Dock operations on the main thread in a real desktop `.app`. Unsupported
platform operations throw `UnsupportedOperationException`, rather than silently
pretending a badge was set. The helper uses AppKit's `NSDockTile` and
`NSApplication.requestUserAttention:` / `cancelUserAttentionRequest:`. Informational
attention can finish automatically; retaining a token does not imply the Dock is
still bouncing. Critical requests need explicit cancellation or activation.

Keep attention handles in a `Try`/`Finally` and call `Close` when the operation no
longer needs attention. The destructor explicitly queues cleanup to the UI thread
if the last reference is released by a worker. Still use explicit Close for prompt
cancellation while the app run loop is alive. Badges are app-wide shared state, not a per-window resource, so the
package does not restore a badge behind another component's back.
