# Dock badges and bounce

Opt-in macOS Dock badges and cancellable attention requests. `Import dock`.
No Dock effect occurs merely by importing the package or asking `DockSupported()`.

Call all Dock operations on the main thread in a real desktop `.app`. Unsupported
platform operations throw `UnsupportedOperationException`, rather than silently
pretending a badge was set. The helper uses AppKit's `NSDockTile` and
`NSApplication.requestUserAttention:` / `cancelUserAttentionRequest:`. Informational
attention can finish automatically; retaining a token does not imply the Dock is
still bouncing. Critical requests need explicit cancellation or activation.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add dock --git https://github.com/BuoyBay/dock.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## Example

```basic
Import dock

Sub UpdateUnreadBadge(unread As Integer)
    If Not DockSupported() Then Return
    SetDockBadgeCount(unread, 99)
End Sub
```

## Platform and scope

Dock badges and attention requests are macOS features. Check support before use and balance owned attention requests.

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer dock
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
