# Debug

The Debug category shows extra console logging, and particle overlays for two of the distance-based systems. Useful when tuning Chat, Chunk Render, or Render Players.

## What It Does

- Logs per-subsystem diagnostic info to console.
- Draws particle rings and lines in-world for the two systems that support it: Chat and Render Players.

## How to Use

1. Run `/ssmp settings`.
2. Go to the **Debug** category (always the last tab, regardless of how many other categories exist).
3. Turn on **Master Switch** - nothing below it does anything until this is on.
4. Turn on the subsystems you want to debug.

There's no `/ssmp debug` command - every toggle lives in the Settings GUI, or in `plugins/Scripted-SMP-Core/models/debug/config.yml` if you'd rather edit the file directly.

## Subsystems

| Subsystem | Default | What it shows |
|-----------|---------|----------------|
| Chat | off | Chat filtering/delivery decisions in console |
| Chat Particles | off | **Visual overlay** - proximity rings and lines around chat range |
| Chunk Render | off | Per-player render-distance calculations in console |
| Render Players | off | Visibility tick/hide/show decisions in console |
| Render Players Particles | off | **Visual overlay** - proximity rings and lines for visibility distance |
| Death List | off | Death List GUI action logging |
| Death Sound | off | Death sound trigger and proximity decisions |
| GUI | **on** | GUI click, drag, and creative-inventory event logs |
| Immortal | off | Damage-cap and death-cancellation logging |
| Team Glow | **on** | Team glow/color packet interception logging |
| Auto Kit | off | Kit apply/save action logging |
| Respawn | off | Respawn location resolution logging |
| Nickname | off | Appearance-reload decisions and observer refresh counts |

## Notes

> **Warning:** Debug mode can reduce server performance, especially the particle overlays. Turn it off when you're done tuning.

- Only Chat and Render Players have a particle-overlay toggle - every other subsystem is console-log-only.
- Most subsystem toggles default to off, but **GUI** and **Team Glow** ship on by default.

## Related Pages

- [Settings GUI](settings-gui.md) - the Debug category lives here
- [Chunk Render](chunk-render.md) and [Render Players](render-players.md) - the two modules debug overlays help tune most
