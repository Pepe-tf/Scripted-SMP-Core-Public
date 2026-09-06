# Respawn

Create custom respawn points in-game. Players respawn at the nearest safe one instead of their bed or world spawn.

## What It Does

- Create named respawn points from your current location.
- On respawn, the plugin picks the active point if it's safe, otherwise the nearest saved point in the same world, and falls back to world spawn if nothing else is safe.
- By default a player's own bed or respawn anchor still takes priority over custom points - turn on `ignore-vanilla-respawn` to always use the custom system instead.
- Works with the Death List's revive command - a revived player lands at a custom respawn point the same way.

## Commands

| Command | Permission | Description |
|---------|------------|-------------|
| `/ssmp respawn` (alias `rs`) | `ssmp.respawn.manage` | Open the Respawn Locations GUI |
| `/ssmp respawn <player>` | `ssmp.respawn.manage` | Revive a player - removes them from the Death List, restores survival mode, and teleports them to a respawn point |

All point management (create, select active, delete) happens in the GUI - there's no command form for it.

## The Respawn Locations GUI

- **Create Respawn Point** saves your current location, block-centered with your facing direction, auto-named after you.
- **Left-click** a location to make it the active point.
- **Right-click** a location to preview-teleport there yourself (no permission beyond opening the GUI).
- **Shift-click** a location to delete it - if it was active, the active slot is cleared.

The active point shows as green concrete with a glint; every other saved point shows as stone brick.

## Important Settings

| Setting | Default | Description |
|---------|---------|-------------|
| `enabled` | true | Turn the module on/off |
| `teleport-on-removal` | true | Teleport to the active point when a player is removed from the Death List |
| `nearest-fallback` | true | If no active point is set, use the nearest saved point in the same world |
| `ignore-vanilla-respawn` | false | When true, always use the custom point or world spawn - beds and respawn anchors are never checked |
| `respawn-effects` | true | Play visual/sound effects and a title when a custom respawn triggers |
| `safe-search-radius` | 5 | How far to search around a point for safe ground before falling back further |
| `respawn-cooldown-seconds` | 0 | *(currently has no effect - see note below)* |

> **Note:** `respawn-cooldown-seconds` is present in the config and the Settings GUI, but nothing in the plugin currently enforces it. Setting it to a non-zero value won't change respawn behavior yet.

## Permissions

| Permission | Default | Effect |
|------------|---------|--------|
| `ssmp.respawn.manage` | op | Open the Respawn Locations GUI and revive players |

## Notes

- Locations are saved in `plugins/Scripted-SMP-Core/data/respawn-locations.yml`, and synced to the database if one is configured.
- A location is only used if it's actually safe (solid ground, room to stand, no fire/lava/hazards) - the plugin spirals outward from a saved point looking for safe ground before giving up and trying the next fallback.

## Related Pages

- [Death List](death-list.md) - revived players respawn using this module
- [Settings GUI](settings-gui.md) - configure fallback behavior and safe-search radius
