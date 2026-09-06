# Scripted SMP Core - User Wiki

Welcome to the **Scripted SMP Core** wiki. This guide is written for server owners and admins who want to set up and use the plugin without reading code.

> **Coverage note:** these pages don't yet cover Vanish, Orbital, Random Kit,
> or the newest commands (`/ssmp tp`, `/ssmp team add`/`fixhealth`, `/ssmp
> kit set`) - see [Commands](../COMMANDS.md) for the current, complete
> command list in the meantime.

## What is Scripted SMP Core?

It is a Paper 1.21+ plugin that bundles the most common SMP systems into one place:

- Nicknames, skins, and admin-only disguises
- Death tracking, spectator mode, soft-ban, and revival
- Proximity chat with distance fade, server-wide broadcasts, and chat clear
- Immortality management
- Player freeze
- Team system with leaders, alliances, colored glow, locked teams, and per-team max HP
- Auto kits for teams, with Quick Save
- Custom respawn locations
- Chunk render distance control
- Proximity player visibility
- Death sound effects
- Admin tools: sudo, invsee, fly, set HP/hunger, and a per-player settings GUI
- In-game settings GUI for every module above

## Requirements

- **Server:** Paper 1.21 or newer
- **Java:** 21 or newer
- **Dependency:** [ProtocolLib](https://www.spigotmc.org/resources/protocollib.1997/) 5.4.0+ (hard requirement - the plugin disables itself without it)
- **License:** a valid license key - there is no trial mode

## Quick Start

1. Stop your server.
2. Put the plugin jar and `ProtocolLib.jar` in your `plugins/` folder.
3. Start the server - it creates default configs under `plugins/Scripted-SMP-Core/models/*/config.yml`.
4. Run `/ssmp` to check it loaded.
5. An operator or `ssmp.admin` holder must run `/ssmp license` and enter a valid key in the dialog that opens - there is no trial mode, a key is always required.
6. Run `/ssmp menu` to open the Main Menu hub, or `/ssmp settings` to jump straight into configuration.

## Wiki Pages

| Page | What you will learn |
|------|---------------------|
| [Commands](../COMMANDS.md) | Every `/ssmp` command and what it does |
| [Permissions](../PERMISSIONS.md) | Who can use what |
| [Main Menu](main-menu.md) | The `/ssmp menu` hub GUI |
| [Settings GUI](settings-gui.md) | How to configure the plugin in-game |
| [Nicknames & Disguises](nick.md) | Custom names, skins, and admin disguises |
| [Admin Tools](admin-tools.md) | Sudo, broadcast, fly, invsee, sethp/sethunger, Player Settings GUI |
| [Death List](death-list.md) | Spectator death mode and revival |
| [Chat](chat.md) | Proximity chat and message filters |
| [Immortal](immortal.md) | Temporary god mode |
| [Freeze](freeze.md) | Freeze players in place |
| [Teams](teams.md) | Leaders, alliances, and locked teams |
| [Auto Kit](auto-kit.md) | Create and assign gear kits |
| [Respawn](respawn.md) | Custom respawn locations |
| [Chunk Render](chunk-render.md) | Per-player view distance |
| [Render Players](render-players.md) | Hide distant players |
| [Death Sound](death-sound.md) | Sound on player death |
| [Debug](debug.md) | Visual overlays and console logging |
| [Database](database.md) | Optional cross-server sync |

## Tips

- `/ssmp menu` opens a central hub linking Settings, Teams, Auto Kits, Death List, Respawn, Immortal, Nickname, and Help.
- Most settings can be changed inside the game with `/ssmp settings`.
- If you edit config files by hand, run `/ssmp reload` afterward.
- Admins usually just need `ssmp.admin` - it grants almost everything except the LuckPerms-only chunk render node.
- Each module has its own config file under `plugins/Scripted-SMP-Core/models/<module>/config.yml`.
- Only operators or players with `ssmp.admin` can activate the plugin via `/ssmp license`.
- Run `/ssmp update` any time to check for a new version - the plugin also checks automatically every few hours and warns admins in-game on join if one is available.

## Need Help?

Use `/ssmp help` in-game to open the command reference GUI.
