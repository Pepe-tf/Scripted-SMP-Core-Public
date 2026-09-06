# Settings GUI

The easiest way to configure the plugin is inside the game.

## Opening the GUI

Run `/ssmp settings` (alias `/ssmp s`, needs `ssmp.admin`), or open it from the **Main Menu** (`/ssmp menu`).

## Layout

- **Top rows** - settings for the selected category, paginated if there are more than fit on one page.
- **Bottom row** - Reset All, Previous Page, up to 5 category tabs at a time (scroll with the arrows either side if there are more), Next Page, Plugin Credit.

## Categories

| Category | What you can change |
|----------|---------------------|
| General | Master on/off toggle for each module |
| Chat | Proximity chat distances, world-only, mute, proximity events |
| Death List | Soft-ban, hardcore-ban, spectator mode, kick-on-death, kick delay, recorded fields |
| Death Sound | Enabled, proximity range (sound/volume/pitch are shown but config-file only) |
| Respawn | Nearest fallback, cooldown, safe search, teleport-on-removal |
| Chunk Render | Min/max distance, ping mode, dynamic mode, AFK settings |
| Render Players | Visibility distance, admin bypass, max visible |
| Immortal | Enabled, min health, totem bypass |
| Team | Max teams, friendly fire, glow, auto-assign, name limits |
| Nickname | Length limits, duplicate/real-name rules, skins, disguise, random nicknames |
| Debug | Master switch and every subsystem toggle - always the last tab |

Freeze and Auto Kit have no category here - they have nothing to configure, everything about them is command/GUI driven.

> **Note:** This is the *global* settings GUI - it changes the default for everyone. To override a setting for just one player, shift-right-click them in creative mode instead - see [Admin Tools](admin-tools.md)'s Player Settings GUI.

## How to Use

1. Click a bottom-row tab to pick a category.
2. Click a setting to change it.
3. Toggles turn on (green) or off (red).
4. Numbers adjust with Left-click (+1), Right-click (-1), Shift-click (±10).
5. Every change saves to disk the instant you click it - there's nothing to lose by switching tabs or having the GUI close unexpectedly. Closing the menu (or navigating Home) also triggers one final save-all pass as a safety net.

### Reset All

The **Reset All** button resets every module's settings back to their shipped default values - it isn't a gentle "fill in anything missing" operation, it's a real reset. Use it carefully if you've customized values you want to keep.

## Manual Config Files

You can also edit files directly:

```
plugins/Scripted-SMP-Core/models/<module>/config.yml
```

Run `/ssmp reload` after editing.

## Related Pages

- [Commands](../COMMANDS.md) - the full `/ssmp` command tree
- [Debug](debug.md) - visual overlays for tuning distance/chat modules
- [Permissions](../PERMISSIONS.md) - every `ssmp.*` node
- [Admin Tools](admin-tools.md) - the Player Settings GUI, for per-player overrides
