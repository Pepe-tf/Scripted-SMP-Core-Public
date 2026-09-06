# Permissions Reference - Scripted SMP Core

All permission nodes use the **`ssmp.`** prefix. Every node defaults to
**`op`** unless noted otherwise. See [COMMANDS.md](COMMANDS.md) for what each
command does.

---

## Master Admin

| Permission | Default | Description |
|---|---|---|
| `ssmp.admin` | `op` | Grants every permission listed under "Children of `ssmp.admin`" below in one grant. |

**Children of `ssmp.admin`:**
`ssmp.deathlist.open`, `ssmp.deathlist.remove`, `ssmp.deathlist.clear`,
`ssmp.deathlist.bypass`, `ssmp.chat.bypass`, `ssmp.immortal`,
`ssmp.freeze.bypass`, `ssmp.chunkrender.admin`, `ssmp.renderplayer.bypass`,
`ssmp.respawn.manage`, `ssmp.team.admin`, `ssmp.gamemode`,
`ssmp.gamemode.others`, `ssmp.nick.set`, `ssmp.nick.others`,
`ssmp.nick.admin`, `ssmp.nick.disguise`, `ssmp.nick.manage`, `ssmp.sudo`,
`ssmp.broadcast`, `ssmp.fly`, `ssmp.flyspeed`, `ssmp.invsee`,
`ssmp.playersettings`, `ssmp.sethp`, `ssmp.sethunger`, `ssmp.durability`,
`ssmp.heal`, `ssmp.vanish`, `ssmp.orbital.admin`, `ssmp.tp`

> **Note:** `ssmp.autokit.admin` is **not** a child of `ssmp.admin` - it must
> be granted separately if you want your admins to manage Auto Kits.

---

## Death List

| Permission | Default | Description |
|---|---|---|
| `ssmp.deathlist.open` | `op` | Open the Death List GUI (`/ssmp deathlist`), list, and view entries. |
| `ssmp.deathlist.remove` | `op` | Remove a player from the Death List (`--remove`). |
| `ssmp.deathlist.clear` | `op` | Clear all Death List entries (`--removeall`). |
| `ssmp.deathlist.bypass` | `false` | Bypass soft-ban / death-list tracking entirely. Intended for **non-admin** players who need immunity - not included in `ssmp.admin`. |

---

## Chat

| Permission | Default | Description |
|---|---|---|
| `ssmp.chat.bypass` | `op` | Ignore proximity chat distance limits and chat mute; hidden join/quit messages. |

---

## Chunk Render Distance

| Permission | Default | Description |
|---|---|---|
| `ssmp.chunkrender.admin` | `op` | Access to every `/ssmp chunk` subcommand (`set`, `get`, `reset`, `ping`, `dynamic`). |
| `ssmp.chunkrender.bypass` | `op` | Ignore all chunk render distance limits. |
| `ssmp.chunkrender.dynamic.bypass` | `op` | Ignore server-wide dynamic (lag-based) reduction. |
| `ssmp.chunkrender.afk.bypass` | `op` | Ignore AFK-based chunk reduction. |
| `ssmp.chunkrender.max.<N>` | `false` | **LuckPerms-only** node. Soft-caps max render distance to `<N>` chunks, e.g. `ssmp.chunkrender.max.16`. |

**Children of `ssmp.chunkrender.admin`:** `ssmp.chunkrender.bypass`,
`ssmp.chunkrender.dynamic.bypass`, `ssmp.chunkrender.afk.bypass`

---

## Player Visibility (Render Players)

| Permission | Default | Description |
|---|---|---|
| `ssmp.renderplayer.bypass` | `op` | Bypass proximity visibility distance. |

> All of `/ssmp rp`'s own subcommands (`status`/`toggle`/`distance`/etc.) are
> gated by the general `ssmp.admin` node, not a dedicated `ssmp.renderplayer.admin`.

---

## Immortality & Freeze

| Permission | Default | Description |
|---|---|---|
| `ssmp.immortal` | `op` | Toggle immortality on other players (`/ssmp immortal`, Immortal Management GUI). |
| `ssmp.freeze.bypass` | `op` | Immune to global and individual freeze - movement, chat, damage, and all interactions remain unaffected. |

> `/ssmp freeze`'s own subcommands are gated by `ssmp.admin`.

---

## Respawn

| Permission | Default | Description |
|---|---|---|
| `ssmp.respawn.manage` | `op` | Open the Respawn Location GUI and manage respawn points. |

---

## Teams

| Permission | Default | Description |
|---|---|---|
| `ssmp.team.admin` | `op` | Full team management - `create`, `leave`, `info`, `kick`, `autoassign`, `add`, `fixhealth`, `setleader`, `ally`, `allies`, and grants every child below. |
| `ssmp.team.gui` | `op` | Open the Teams GUI. |
| `ssmp.team.create` | `op` | Create a new team. |
| `ssmp.team.leave` | `op` | Leave your current team. |
| `ssmp.team.glow.bypass` | `op` | See all team glow outlines regardless of membership. |

**Children of `ssmp.team.admin`:** `ssmp.team.gui`, `ssmp.team.create`,
`ssmp.team.leave`, `ssmp.team.glow.bypass`

---

## Teleport

| Permission | Default | Description |
|---|---|---|
| `ssmp.tp` | `op` | Teleport a player, everyone online, a team, or a random amount of players to a destination (`/ssmp tp`). |

---

## Auto Kits

| Permission | Default | Description |
|---|---|---|
| `ssmp.autokit.admin` | `op` | Open the Auto Kit GUI, manage kit definitions, apply a kit directly to a player, and assign a kit to a team (`/ssmp autokit`/`/ssmp kit`). Not a child of `ssmp.admin` - grant it separately. |

---

## Nicknames & Disguises

| Permission | Default | Description |
|---|---|---|
| `ssmp.nick.set` | `op` | Set your own nickname/skin via the Nickname GUI or `/ssmp nick`. |
| `ssmp.nick.others` | `op` | Set or reset another player's nickname. |
| `ssmp.nick.admin` | `op` | Bypass nickname length/character/duplicate/cooldown restrictions. |
| `ssmp.nick.disguise` | `op` | Make one player look exactly like another real player (`/ssmp nick set <target> as <identity>`) - every use is logged. |
| `ssmp.nick.manage` | `op` | Bulk/data-management name commands (`reset @a`, `random @a`, `saveall`, `refresh`, `realname`, `debug`). |

---

## Moderation & Utility

| Permission | Default | Description |
|---|---|---|
| `ssmp.sudo` | `op` | Force another (optionally nicknamed) player to run a command or send a chat message. |
| `ssmp.broadcast` | `op` | Broadcast a chat message or big on-screen text to the whole server. |
| `ssmp.fly` | `op` | Toggle your own flight in any gamemode except spectator. |
| `ssmp.flyspeed` | `op` | Set your own fly speed, 1-10. |
| `ssmp.invsee` | `op` | Open a live, editable view of another (optionally nicknamed) player's inventory, or right-click them in creative. |
| `ssmp.playersettings` | `op` | Open the per-player admin settings menu by shift-right-clicking a player in creative. |
| `ssmp.sethp` | `op` | Set a player's health in exact hearts, locking their hunger so it can't regen back. |
| `ssmp.sethunger` | `op` | Set a player's food level directly, 0-20. |
| `ssmp.durability` | `op` | Set the durability of the item in your hand as a percentage, 1-100. |
| `ssmp.heal` | `op` | Fully restore health, hunger, saturation and exhaustion for a player, everyone online, or a team. |
| `ssmp.vanish` | `op` | Toggle complete invisibility for yourself or another player, admin or not - only fellow vanished players can see them, ops included. |

---

## Orbital

| Permission | Default | Description |
|---|---|---|
| `ssmp.orbital.admin` | `op` | Trigger orbital strikes directly, give orbital payload items, and view status (`/ssmp orbital`, alias `/ssmp os`). |

---

## Gamemode

| Permission | Default | Description |
|---|---|---|
| `ssmp.gamemode` | `op` | Change your own gamemode (`/gamemode`, `/gmc`, `/gms`, `/gma`, `/gmsp` and their aliases). |
| `ssmp.gamemode.others` | `op` | Change another player's gamemode. |

---

## LuckPerms Integration

For **chunk render max-distance**, assign LuckPerms permission nodes like:

```
ssmp.chunkrender.max.8
ssmp.chunkrender.max.16
ssmp.chunkrender.max.32
```

These are checked dynamically and support world-contexts.

---

*Last updated for Scripted SMP Core v1.2.5.1*
