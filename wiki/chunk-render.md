# Chunk Render

Automatically manages how many chunks each player sees, layering a default, a saved preference, a LuckPerms cap, an admin override, and optional lag/AFK/ping-based reduction - instead of one flat server-wide setting.

## What It Does

For a normal player, distance is worked out in this order:

1. Start from the server **default** (`max-distance`).
2. Apply the player's own **saved preference**, if they've set one.
3. Cap it to their **LuckPerms** max-distance node, if any.
4. If an admin has **force-set** their distance with `/ssmp chunk set`, that replaces the result outright rather than just capping it.
5. Subtract a **dynamic** reduction if the server is under load (MSPT-based, server-wide).
6. Subtract an **AFK** reduction if the player has been idle.

**Ping mode works differently** - a player who opts into it (or is opted in by an admin) gets their distance recalculated independently: LuckPerms cap → admin override → clamped to ping-mode's own min/max → reduced based on their ping → reduced again for server lag. This calculation ignores their saved preference and AFK state, and its result is what's actually applied to their client. Both the global ping-mode switch and the per-player opt-in need to be on for this to take effect.

## Commands

| Command | Description |
|---------|-------------|
| `/ssmp chunk status` (alias `/ssmp cr`) | Show current settings and state |
| `/ssmp chunk set <chunks> [player]` | Set your own preference, or force a player's distance as an admin override |
| `/ssmp chunk get [player]` | Show computed vs. current view distance |
| `/ssmp chunk reset [player]` | Clear stored preference/override and recalculate |
| `/ssmp chunk ping info` | Show whether ping mode is globally enabled |
| `/ssmp chunk ping on\|off [player]` | With a player: opt them in/out of ping mode. Without: toggle ping mode globally |
| `/ssmp chunk dynamic info` | Show dynamic mode's state and current live reduction |
| `/ssmp chunk dynamic on\|off` | Toggle server-wide lag-based reduction |

Every `/ssmp chunk` command requires `ssmp.chunkrender.admin`.

## Important Settings

| Setting | Default | Description |
|---------|---------|-------------|
| `enabled` | false | Turn the module on/off |
| `min-distance` / `max-distance` | 2 / 32 | Floor and ceiling for computed distance |
| `sync-simulation-distance` | true | Keep simulation distance equal to view distance |
| `admin-bypass` | true | Let `ssmp.chunkrender.bypass` holders skip enforcement entirely |
| `check-interval-ticks` | 40 | How often all players are rechecked |
| `kick-on-refuse` | false | Kick a player (after one warning) who keeps manually overriding their enforced distance |
| `afk-time` | 60 | Seconds idle before AFK reduction applies. 0 disables it |
| `afk-chunks` | 2 | Distance while AFK |
| `afk-spectators` | true | Whether spectators are also subject to AFK reduction |
| `zero-chunks-afk` | false | Reduce AFK players to 0 chunks instead of `afk-chunks` |
| `ping-mode.enabled` | false | Global switch for ping-based reduction |
| `ping-mode.interval` | 100 | Ticks between ping re-checks |
| `ping-mode.min` / `.max` | 2 / 32 | Clamp range specific to ping mode |
| `ping-mode.thresholds` | 100ms→2, 200ms→4, 300ms→6 | Ping at or above each threshold reduces distance by that amount |
| `dynamic-mode.enabled` | false | Global switch for lag-based reduction |
| `dynamic-mode.interval` | 100 | Ticks between server-lag checks |
| `dynamic-mode.thresholds` | 20ms→2, 30ms→4, 40ms→6 | Average tick time at or above each threshold reduces everyone's distance by that amount |
| `save-player-data` | true | Persist each player's preference to disk |
| `recalculate-on-world-change` | true | Recalculate immediately when a player changes world |

## LuckPerms Integration

Grant a node like `ssmp.chunkrender.max.16` to cap a player's distance at 16 chunks. Supports per-world contexts - a world-scoped node takes priority over a global one for that world. With no matching node, a player is effectively uncapped (32).

## Permissions

| Permission | Default | Effect |
|------------|---------|--------|
| `ssmp.chunkrender.admin` | op | Use every `/ssmp chunk` command |
| `ssmp.chunkrender.bypass` | op | Ignore all chunk render limits |
| `ssmp.chunkrender.dynamic.bypass` | op | Ignore server-wide lag-based reduction |
| `ssmp.chunkrender.afk.bypass` | op | Ignore AFK-based reduction |
| `ssmp.chunkrender.max.<N>` | false | LuckPerms-only max-distance node |

## Related Pages

- [Debug](debug.md) - console logging for render-distance calculations
- [Settings GUI](settings-gui.md) - configure every setting above without commands
