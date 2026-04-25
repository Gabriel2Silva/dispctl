# dispctl

A display configuration script for GNOME on Wayland, designed as a proper
replacement for the `Super+P` shortcut.

## Why not just use Super+P?

GNOME Shell's built-in `Super+P` switcher (`js/ui/switchMonitor.js`) cycles
through four hardcoded presets by calling
`monitorManager.switch_config(Meta.MonitorSwitchConfigType.*)`:

- **Mirror** — clone all displays
- **Join Displays** — extend all displays in a line
- **External Only** — disable the built-in panel
- **Built-in Only** — disable all external displays

And... that's it. There's no resolution control, no refresh rate selection, no VRR toggle,
no per-monitor configuration, no primary monitor choice, not even persistence beyond
the current session (unlike the display switcher on GNOME Control Center). It's a blunt, barebones preset switcher that applies whatever default
mode Mutter picks for each monitor.

`dispctl` replaces this with a guided, interactive flow that gives
you full control over every relevant setting.

## Features

- Choose any resolution and refresh rate per monitor
- VRR (Variable Refresh Rate) support
- Extend displays in any order with primary monitor selection
- Duplicate displays across monitors with a common resolution
- Configuration is **persistent** across reboots (written to `monitors.xml`
  via `gdctl --persistent`, the same mechanism used by GNOME Settings)
- Monitor names sourced from EDID `display-name` property, same as the
  GNOME Displays panel

## Dependencies

- [`gdctl`](https://gitlab.gnome.org/GNOME/mutter/-/merge_requests/4190) — GNOME Display Controller
- [`zenity`](https://gitlab.gnome.org/GNOME/zenity) — GTK dialog toolkit
- GNOME Shell with Mutter (requires `org.gnome.Mutter.DisplayConfig` D-Bus API)

## Usage

Run directly or bind to a keyboard shortcut (e.g. replacing `Super+P`):

```
dispctl
```

## Recommended setup

In GNOME Settings → Keyboard → Custom Shortcuts, add a shortcut pointing to
the script and assign `Super+P` to it (after disabling the default binding
under System → Switch display configuration).

<img width="640" height="643" alt="output" src="https://github.com/user-attachments/assets/798bde1b-a1d7-46a1-b1cb-91a91e192f62" />
