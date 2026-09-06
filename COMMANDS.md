# Commands Reference - Scripted SMP Core

Every command lives under `/ssmp` (alias of `/ssmp-core`). Most subcommands
open an in-game GUI when run with no arguments - see [README.md](README.md)
for a features overview and [PERMISSIONS.md](PERMISSIONS.md) for the
permission each one needs.

`@s` means "myself" wherever a command accepts a single player-name argument.
Anywhere a player name is accepted, a currently-set nickname works too.

---

## General

| Command | Description |
|---|---|
| `/ssmp` | Show plugin info |
| `/ssmp menu` | Open the main menu GUI (alias `/ssmp gui`) |
| `/ssmp help` | Show the help menu |
| `/ssmp version` | Show plugin version |
| `/ssmp reload` | Reload configuration |
| `/ssmp settings` | Open the plugin settings GUI |
| `/ssmp status` | Show system status |
| `/ssmp update` | Check for a plugin update |

---

## Death List

| Command | Description |
|---|---|
| `/ssmp deathlist` | Open the Death List GUI |
| `/ssmp deathlist --list` | List all dead players in chat |
| `/ssmp deathlist --remove <name>` | Remove a player from the list |
| `/ssmp deathlist --removeall` | Clear all entries |
| `/ssmp deathlist --info <name>` | Show death info for a player |
| `/ssmp deathlist --count` | Show total dead count |

---

## Chat

| Command | Description |
|---|---|
| `/ssmp chat status` | Show chat system status |
| `/ssmp chat toggle` | Toggle proximity chat on/off |
| `/ssmp chat adminbypass` | Toggle admin/ops ignoring the distance filters |
| `/ssmp chat cutdistance <blocks>` | Set hard cut-off distance |
| `/ssmp chat fadedistance <blocks>` | Set obfuscation start distance |
| `/ssmp chat worldonly` | Toggle world isolation |
| `/ssmp chat proximityevents` | Toggle proximity filtering for join/leave/death |
| `/ssmp chat mutechat` | Toggle chat mute (blocks all but bypass/ops) |
| `/ssmp chat clear` | Clear chat for every online player (looks like a fresh join) |

---

## Chunk Render Distance

| Command | Description |
|---|---|
| `/ssmp chunk status` | Show chunk render status |
| `/ssmp chunk set <chunks> [player]` | Set render distance (self or target) |
| `/ssmp chunk get [player]` | Get current/rendered distance |
| `/ssmp chunk reset [player]` | Reset to defaults |
| `/ssmp chunk ping [on\|off\|info] [player]` | Toggle ping mode |
| `/ssmp chunk dynamic [on\|off\|info]` | Toggle dynamic mode |

---

## Player Visibility (Render Players)

| Command | Description |
|---|---|
| `/ssmp rp status` | Show render-players status |
| `/ssmp rp toggle` | Toggle render-players on/off |
| `/ssmp rp distance <blocks>` | Set visibility distance |
| `/ssmp rp adminvisible` | Toggle admin always visible |
| `/ssmp rp adminseeall` | Toggle admin see all players |

---

## Immortality & Freeze

| Command | Description |
|---|---|
| `/ssmp immortal <player\|@s>` | Toggle immortality on a player |
| `/ssmp freeze [player\|@s\|status]` | Toggle global freeze, or freeze/unfreeze a specific player |
| `/ssmp freeze @a` | Freeze/unfreeze everyone online at once |
| `/ssmp freeze --team <name>` | Freeze/unfreeze every online member of a team |
| `/ssmp freeze status` | List all currently frozen players |

---

## Respawn Locations

| Command | Description |
|---|---|
| `/ssmp respawn` | Open the Respawn Location GUI (alias `/ssmp rs`) |

---

## Teams

| Command | Description |
|---|---|
| `/ssmp team` | Open the Teams GUI |
| `/ssmp team create` | Open the Create Team GUI |
| `/ssmp team leave` | Leave your current team |
| `/ssmp team info <team>` | Show team info |
| `/ssmp team kick <player>` | Kick a player from their team |
| `/ssmp team autoassign` | Auto-assign all un-teamed players to teams (lowest size first) |
| `/ssmp team add <team> radius:<blocks>` | Add every un-teamed online player within `<blocks>` of you to a team |
| `/ssmp team fixhealth <player>` | Force-resync a player's max health against their current team, or the vanilla default if none |
| `/ssmp team setleader <player>` | Set a team's leader |
| `/ssmp team ally <team1> <team2>` | Toggle an alliance between two teams |
| `/ssmp team allies <team>` | List a team's current allies |

---

## Teleport

| Command | Description |
|---|---|
| `/ssmp tp <player> <destination>` | Teleport a player to another player/`@s` |
| `/ssmp tp @a <destination>` | Teleport every online player to a destination |
| `/ssmp tp --team <name> <destination>` | Teleport every online member of a team to a destination |
| `/ssmp tp --random <amount> <destination>` | Teleport a random amount of online players to a destination |

---

## Auto Kits

| Command | Description |
|---|---|
| `/ssmp autokit` | Open the Auto Kit management GUI (alias `/ssmp kit`) |
| `/ssmp kit <kitname> <player>` | Apply a saved kit directly to a player right now |
| `/ssmp kit set <team> <kitname>` | Assign a kit as a team's auto-kit and apply it to online members |

---

## Nicknames & Disguises

| Command | Description |
|---|---|
| `/ssmp nick` | Open the Nickname GUI (alias `/ssmp name` or `/ssmp n`) |
| `/ssmp nick set <nickname> [color]` | Set your own nickname |
| `/ssmp nick reset [player\|@a]` | Reset your nickname (or another's/everyone's, with permission) |
| `/ssmp nick other <player> <nickname> [color]` | Set another player's nickname |
| `/ssmp nick nametag [on\|off]` | Toggle your floating nametag override |
| `/ssmp nick status` | Show your current nickname info |
| `/ssmp nick skin <player>` | Copy that player's skin onto yourself - works even if they're offline |
| `/ssmp nick skin other <player> <copyFrom>` | Copy a skin onto another player - `copyFrom` can be offline too |
| `/ssmp nick skinreset [player]` | Clear a skin override |
| `/ssmp nick random [player\|@a] [--skin\|--name]` | Generate and apply a random nickname + skin, or only one half |
| `/ssmp nick set <target> as <identity>` | Disguise `<target>` as the real player `<identity>` (logged) |
| `/ssmp nick saveall` | Force-save all nickname data |
| `/ssmp nick refresh <player>` | Re-apply a player's stored nickname state |
| `/ssmp nick realname <player>` | Show a nicked player's real account name |
| `/ssmp nick debug <player>` | Show a player's full name/skin/disguise state |

---

## Moderation & Utility

| Command | Description |
|---|---|
| `/ssmp sudo <player\|nickname\|@s> <command\|message>` | Force a player to run a command (starts with `/`) or send a chat message |
| `/ssmp broadcast chat <message>` | Broadcast a boxed chat message to the whole server (alias `/ssmp bc`) |
| `/ssmp broadcast title <message> <seconds>` | Broadcast big on-screen text for a set duration (e.g. `5s`) |
| `/ssmp broadcast stop` | End the current on-screen broadcast early for everyone |
| `/ssmp fly` | Toggle your own flight in any gamemode except spectator |
| `/ssmp flyspeed <1-10>` | Set your own fly speed (1 = normal, 10 = max) |
| `/ssmp invsee <player\|nickname\|@s>` | Open a live, editable view of a player's inventory (alias `/ssmp inv`) |
| *(shift-right-click a player, creative)* | Open the per-player settings menu - chunk render, visibility, immortal, nick, team, kit |
| `/ssmp sethp <player\|nickname\|@s> <hearts>` | Set a player's health in hearts (e.g. `0.5` = half a heart) - also locks their hunger so it can't regen back |
| `/ssmp sethunger <player\|nickname\|@s> <0-20>` | Set a player's food level directly (0 = starving, 20 = full) |
| `/ssmp durability <1-100>` | Set the durability of the item you're holding, as a percentage |
| `/ssmp heal <player\|@s\|@a\|--team <name>>` | Fully restore health, hunger, saturation, and exhaustion |
| `/ssmp vanish <player\|@s>` | Toggle complete invisibility - hidden from everyone except staff, no join/quit message |

---

## Orbital (alias `/ssmp os`)

| Command | Description |
|---|---|
| `/ssmp orbital status` | Show orbital module status |
| `/ssmp orbital strike <nuke\|stab\|law_nuke\|wither_nuke\|arrow_shot> <x> <y> <z> [world]` | Trigger a strike directly at coordinates |
| `/ssmp orbital strike crosshair <payload>` | Trigger a strike where you're looking |
| `/ssmp orbital give <nuke\|stab\|law_nuke\|wither_nuke\|wolf\|arrow_shot> [player] [amount]` | Give an orbital payload item |

---

## Gamemode

| Command | Alias(es) | Description |
|---|---|---|
| `/gamemode <survival\|creative\|adventure\|spectator\|s\|c\|a\|sp\|0\|1\|2\|3> [player]` | `/gm` | Change your own or another player's gamemode |
| `/gmc [player]` | `/gm1` | Switch to creative mode |
| `/gms [player]` | `/gm0` | Switch to survival mode |
| `/gma [player]` | `/gm2` | Switch to adventure mode |
| `/gmsp [player]` | `/gm3` | Switch to spectator mode |
