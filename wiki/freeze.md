# Freeze

The Freeze module locks players in place - no movement, chat, damage dealt, or interactions.

## What It Does

- Frozen players can't move (they're snapped back to where they were), chat, deal damage, use items, place/break blocks, or interact with anything - including shooting bows or throwing projectiles.
- Frozen players **can still take damage** from other sources - freeze blocks them from acting, not from being acted upon.
- Global freeze locks every player at once (except bypass); a player frozen individually stays frozen regardless of the global toggle, and vice versa - the two are independent and stack.
- Players who join while global freeze is active are frozen immediately and notified.

## Commands

| Command | Permission | Description |
|---------|------------|-------------|
| `/ssmp freeze` | `ssmp.admin` | Toggle global freeze for every non-bypass player |
| `/ssmp freeze <player>` | `ssmp.admin` | Toggle freeze for one specific player |
| `/ssmp freeze status` (or `info`) | `ssmp.admin` | List every currently frozen player |

## Important Settings

This module has no config file - freeze is entirely runtime state, turned on and off with the commands above.

## Permissions

| Permission | Default | Effect |
|------------|---------|--------|
| `ssmp.freeze.bypass` | op | Immune to both global and individual freeze |

## Notes

- Freeze state is in-memory only and resets on every server restart - nothing about who's frozen or whether global freeze is on survives a reload.
- Other plugins can read live freeze state through Bukkit's `ServicesManager` (the plugin publishes its `FreezeManager` there) - compatible bot/NPC plugins honor `/ssmp freeze` instead of ignoring it.

## Related Pages

- [Commands](../COMMANDS.md) - full `/ssmp` command reference
- [Permissions](../PERMISSIONS.md) - every `ssmp.*` node
