# Immortal

Grant a player temporary immunity from dying - damage still lands, but their health can never drop below a configured floor.

## What It Does

- An immortal player's health is capped at a minimum instead of being allowed to hit zero - damage still applies and still hurts, it's just rescaled so they land exactly at the floor instead of dying.
- Holding a Totem of Undying (either hand) skips immortal protection entirely for that hit, so the totem still works normally instead of being silently overridden.
- Status persists across restarts by default - no database required. If you do have the database enabled, immortal status also follows a player between servers on your network.

## Commands

| Command | Permission | Description |
|---------|------------|-------------|
| `/ssmp immortal` | `ssmp.immortal` | Open the Immortal Management GUI |
| `/ssmp immortal <player>` (alias `immo`) | `ssmp.immortal` | Toggle immortality for that player |

## The Immortal Management GUI

A searchable, paginated list of online players - immortal players sort first, then admins, then everyone else, alphabetically within each group. Click a player to open their detail view, then click their head again to toggle immortality on or off.

## Important Settings

| Setting | Default | Description |
|---------|---------|-------------|
| `enabled` | true | Master switch for the immortal system |
| `minimum-health` | 1.0 | Lowest health an immortal player can drop to, in half-hearts (1.0 = half a heart, clamped between 0.5 and 20.0) |
| `totem-bypass` | true | Holding a Totem of Undying lets an immortal player die and consume the totem normally |

## Permissions

| Permission | Default | Effect |
|------------|---------|--------|
| `ssmp.immortal` | op | Toggle immortality on other players, from the command or the GUI |

## Notes

- Immortal status is saved to `plugins/Scripted-SMP-Core/data/immortal.yml` regardless of whether a database is configured - that file alone is enough for it to survive a restart.
- With the database enabled, the database value takes precedence at startup and when a player joins, so status can follow them to a different server in the same network.

## Related Pages

- [Database](database.md) - optional cross-server sync for immortal status
- [Settings GUI](settings-gui.md) - the Immortal category covers every setting above
