# Admin Tools

A set of moderation and utility commands for admins - forcing actions, announcing to the server, flying, inspecting inventories, and setting a player's health or hunger directly.

## What It Does

- **Sudo** - force a player to run a command or say something in chat, as themselves.
- **Broadcast** - a server-wide chat announcement, or a big on-screen title with a set duration.
- **Chat Clear** - scroll every online player's chat away, leaving nothing behind (like a fresh join).
- **Fly / Fly Speed** - self-service flight and fly speed, in any gamemode except spectator.
- **Invsee** - a live, editable view of another player's inventory, styled after Fake Player Plugin Origin's own bot inventory GUI.
- **Player Settings GUI** - shift-right-click a player in creative mode to open a full per-player admin menu covering chunk render, visibility, immortal, nickname, team, kit, and every other global setting as a per-player override.
- **Set HP / Set Hunger** - set a player's health to an exact number of hearts (including halves), or their food level directly.

All targets accept either a player's real account name or their current nickname.

## Commands

| Command | Permission | Description |
|---------|------------|-------------|
| `/ssmp sudo <player\|nickname> <command\|message>` | `ssmp.sudo` | Force the target to run a command (with or without a leading `/`) or send a chat message |
| `/ssmp broadcast chat <message>` | `ssmp.broadcast` | Send a chat announcement to every online player |
| `/ssmp broadcast title <message> <seconds>` (alias `screen`) | `ssmp.broadcast` | Show a big on-screen title to every online player for 1-300 seconds |
| `/ssmp broadcast stop` | `ssmp.broadcast` | Cancel the currently active on-screen broadcast early |
| `/ssmp chat clear` | `ssmp.admin` | Clear chat for every online player |
| `/ssmp fly` | `ssmp.fly` | Toggle your own flight (any gamemode except spectator) |
| `/ssmp flyspeed <1-10>` | `ssmp.flyspeed` | Set your own fly speed - 1 is vanilla-normal, 10 is the maximum |
| `/ssmp invsee <player\|nickname>` (alias `/ssmp inv`) | `ssmp.invsee` | Open a live, editable view of a player's inventory |
| `/ssmp sethp <player\|nickname> <hearts>` | `ssmp.sethp` | Set a player's health to an exact amount, e.g. `0.5` for half a heart |
| `/ssmp sethunger <player\|nickname> <0-20>` | `ssmp.sethunger` | Set a player's food level directly |

`/ssmp broadcast` also has the alias `/ssmp bc`.

## Invsee

Opens the same 54-slot inventory-viewer layout as Fake Player Plugin Origin's own bot inventory GUI, but fully live in both directions: items the target picks up, drops, or moves while the GUI is open appear instantly, and nothing gets rolled back when the viewer closes it. In creative mode, right-clicking a player opens their inventory directly - this never interferes with Fake Player Plugin Origin's own bot click handling.

## Player Settings GUI

Shift-right-click a player while in creative mode to open a per-player admin menu, styled the same way as Fake Player Plugin Origin's per-bot settings menu:

- **Chunk render, visibility, immortal, nickname** - the same overrides available in the global Settings GUI, but scoped to just this player.
- **Team** - force-join or force-remove the target from a team, bypassing the normal join flow entirely.
- **Kit** - click to apply a kit to the target's inventory once (a one-time overwrite), or shift-click to set it as their personal default kit, which then overrides their team's kit on every future join or respawn.
- Every other setting from the global Settings GUI is available here too, as a real per-player override - not just for show.

## Set HP / Set Hunger

`/ssmp sethp` sets a player's health to an exact number of hearts, supporting halves (`0.5`, `1.5`, etc.), clamped to their real max health. If the new amount is below their current health, their hunger is automatically lowered just enough that they can't immediately heal back up - but never so low that it also disables sprinting, and never lowered at all if it's already low enough. `/ssmp sethunger` is the standalone version for setting food level directly, independent of health.

## Permissions

| Permission | Default | Effect |
|------------|---------|--------|
| `ssmp.sudo` | op | Use `/ssmp sudo` |
| `ssmp.broadcast` | op | Use `/ssmp broadcast` (chat, title, and stop) |
| `ssmp.fly` | op | Use `/ssmp fly` |
| `ssmp.flyspeed` | op | Use `/ssmp flyspeed` |
| `ssmp.invsee` | op | Use `/ssmp invsee`, or right-click a player's inventory open in creative |
| `ssmp.playersettings` | op | Shift-right-click a player in creative to open the Player Settings GUI |
| `ssmp.sethp` | op | Use `/ssmp sethp` |
| `ssmp.sethunger` | op | Use `/ssmp sethunger` |

`/ssmp chat clear` uses `ssmp.admin` directly rather than its own node.

## Notes

- Every command in this group is a child of `ssmp.admin`, so admins get all of them automatically.
- Sudo, Invsee, and the Player Settings GUI all resolve their target by current nickname as well as real account name.
- Fake Player Plugin Origin's bots are excluded from Invsee and the Player Settings GUI - use its own bot tools for those instead.

## Related Pages

- [Nicknames & Disguises](nick.md) - how nickname resolution works for targeting
- [Teams](teams.md) - what the Player Settings GUI's Team override actually does
- [Auto Kit](auto-kit.md) - what the Player Settings GUI's Kit override actually does
- [Permissions](../PERMISSIONS.md) - the full permission list
