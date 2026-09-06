# Death List

Every death is logged with full context. Dead players are kicked and can't rejoin until an admin clears them - or go permanent with hardcore mode.

## What It Does

- Every death is recorded: killer, cause, world, exact coordinates, and timestamp.
- Dead players are kicked (after a configurable delay) and soft-banned - they can't rejoin until an admin removes them from the list, or you revive them.
- Optional hardcore mode bans the player permanently instead of soft-banning them.
- Optional spectator mode locks a dead player into spectator instead of kicking them.
- Admins with bypass, and by default anyone with `ssmp.admin`, are immune to all of the above - not kicked, not banned, not recorded.

## Commands

| Command | Permission | Description |
|---------|------------|-------------|
| `/ssmp deathlist` (`dl`) | `ssmp.deathlist.open` | Open the Death List GUI |
| `/ssmp deathlist --list` (`-l`) | `ssmp.deathlist.open` | List dead players in chat, newest first |
| `/ssmp deathlist --remove <name>` (`-r`) | `ssmp.deathlist.remove` | Remove one player from the list |
| `/ssmp deathlist --removeall` (`--clear`, `-c`) | `ssmp.deathlist.clear` | Clear every entry |
| `/ssmp deathlist --info <name>` (`-i`) | *(none)* | Show killer, cause, location, and time for one entry |
| `/ssmp deathlist --count` | *(none)* | Show how many players are currently dead |
| `/ssmp respawn <player>` | `ssmp.respawn.manage` | Revive a player - removes them from the list, clears spectator lock, and teleports them |

## The Death List GUI

A paginated grid of player heads, newest death first. With `ssmp.deathlist.remove`, clicking a head revives that player immediately (same effect as `/ssmp respawn`). The bottom row has Home, Prev/Next/Refresh, page indicator, "Remove First" (removes the oldest entry on the current page), "Clear All Entries" (`ssmp.deathlist.clear`, requires a **shift-click** to confirm so it can't be triggered by accident), and the plugin credit.

## Important Settings

| Setting | Default | Description |
|---------|---------|-------------|
| `enabled` | true | Turn the module on/off |
| `admin-bypass` | true | Ops and `ssmp.admin` are immune - not kicked, banned, or recorded |
| `kick-on-death` | true | Kick the player immediately when they die |
| `kick-delay-ticks` | 10 | Delay between death and the kick/fake-leave message (20 ticks = 1s) |
| `spectator-on-death` | false | Lock dead players in spectator mode instead of kicking |
| `broadcast` | false | Announce the death to every online player |
| `broadcast-message` | *(see config)* | Message template used when broadcast is on, supports `{player}` |
| `max-size` | 0 | Max stored entries, oldest evicted first. 0 = unlimited |
| `ttl-hours` | 0 | Auto-remove an entry after this many hours. 0 = never |
| `effects.enabled` | true | Particles, titles, and sounds on death and revive |
| `hardcore-ban.enabled` | false | Permanently ban the player on death instead of soft-banning |
| `hardcore-ban.reason` | *(see config)* | Ban reason shown to hardcore-banned players |
| `soft-ban.enabled` | true | Block rejoining while dead until an admin clears the entry |
| `record.killer` / `.cause` / `.location` / `.coordinates` / `.timestamp` | all true | Which fields show in the Death List GUI's lore. The underlying data is always recorded regardless of these toggles - they only control what's displayed |

> **Note:** `death-list.respawn-cooldown-seconds` is not currently read by anything - the actual respawn cooldown lives in the [Respawn](respawn.md) module's own config. Leave the copy in Death List's config alone; it has no effect.

## Permissions

| Permission | Default | Effect |
|------------|---------|--------|
| `ssmp.deathlist.open` | op | Open the GUI, use `--list` |
| `ssmp.deathlist.remove` | op | Remove one entry, revive from the GUI |
| `ssmp.deathlist.clear` | op | Clear the whole list |
| `ssmp.deathlist.bypass` | false | Skip recording, kick, ban, and soft-ban entirely |

## Notes

- Soft-banned players are checked at both the pre-login stage and on join, so they're blocked even if something else lets the connection through the first check.
- Hardcore mode uses a real, name-based server ban - it's a separate mechanism from the soft-ban list, and stacks with it if both are enabled.
- Each death entry does capture the player's skin at the time of death, but the Death List GUI currently always renders a player's **live** skin, not the historical one - so that captured data isn't shown anywhere yet.
- Entries are stored in `plugins/Scripted-SMP-Core/data/deathlist.json` and synced to the database if one is configured.
- Fake Player Plugin Origin bots are excluded from the kick path to avoid duplicate leave messages.

## Related Pages

- [Respawn](respawn.md) - revived players land using this module's locations
- [Database](database.md) - death and revive statistics can sync across servers
- [Settings GUI](settings-gui.md) - configure everything above without commands
