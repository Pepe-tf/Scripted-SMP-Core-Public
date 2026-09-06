# Scripted SMP Core

Core plugin bundling essential systems for Scripted SMP content creation -
nicknames and disguises, teams with leaders and alliances, death tracking with
soft-bans, proximity chat, immortality management, chunk render distance
control, player-visibility distance, auto kits, freeze, custom respawn points,
vanish, orbital strike payloads, and a full in-game settings GUI for every one
of them - all built to work together instead of as separate plugins stepping
on each other.

> **This plugin is closed-source.** This repository exists only to distribute
> the compiled plugin jar and keep documentation easy to find - no plugin
> source code is published here.

> **Version:** `1.2.5.1` · **Author:** F_PP

Requires **Paper 1.21+**, **Java 21**, and **ProtocolLib**.

---

## Download

Grab the latest jar from the **[Releases](../../releases)** page. Each release
lists what changed - see [CHANGELOG.md](CHANGELOG.md) for the full history.

A valid license key is required to run the plugin - see
[Licensing](#licensing) below.

---

## Requirements

| | |
|---|---|
| **Server** | Paper (or a Paper fork) `1.21+` |
| **Java** | **Java 21** |
| **Dependency** | [ProtocolLib](https://www.spigotmc.org/resources/protocollib.1997/) (hard requirement; the plugin disables itself without it) |
| **License** | A valid license key |

---

## Highlights

- **Nicknames & disguises**: players pick a cosmetic display name and color
  (with your own length/charset/cooldown/duplicate rules); admins can set or
  reset anyone's, or fully disguise a player as another real Minecraft
  identity and skin - even one that isn't online, fetched straight from
  Mojang. Changes go live instantly for every nearby player - tab list,
  floating nametag, and world-rendered skin - no reconnect needed.
- **Teams that feel like teams**: named teams with colors, glow outlines, a
  designated leader, alliances between teams (no friendly fire, no
  auto-targeting), a per-team max health cap, locked teams that hold their
  identity without accepting new members, bulk radius-add, and an in-game GUI
  for all of it.
- **Auto Kits**: create and edit kits in-game, assign one directly to a
  player or as a team's default loadout from the command line, and built-in
  randomized kit tiers.
- **Flexible teleporting**: beyond a single player or everyone online, send a
  whole team or a random handful of players to a destination in one command.
- **Death List with soft-bans**: every death is logged with full context
  (killer, cause, location, even the player's skin at the time); dead players
  are kicked and can't rejoin until an admin clears them - or go permanent
  with hardcore mode.
- **Proximity chat**: messages fade out and eventually cut off entirely past
  a configurable distance, so far-away players don't see everything everyone
  says.
- **Chunk render distance control**: a layered system (default → saved
  preference → LuckPerms cap → admin override → dynamic lag-based reduction →
  AFK reduction → ping-based reduction) that keeps view distance sane without
  a flat server-wide setting.
- **Player visibility by distance**: hide players from each other beyond a
  configurable radius, independent of chunk render distance.
- **Vanish, freeze, immortality, and custom respawns**, each with its own
  in-game GUI and command.
- **Orbital strikes**: configurable, admin-triggered payload effects with
  built-in safeguards against overwhelming the server.
- **Moderation & utility toolkit**: sudo, server-wide broadcasts, flight and
  fly speed, a live inventory viewer, exact health/hunger/durability setters,
  and instant full heals - for a player, everyone online, or a whole team.
- **Everything configurable in-game** through one unified Settings GUI, no
  YAML-diving required (though every setting is also a plain config file if
  you'd rather edit it directly).
- **Plays well with Fake Player Plugin Origin**: bots respect team
  membership, alliances, freeze state, and a team's designated leader, and
  can resolve a player's nickname instead of their raw account name.

---

## Quick Start

1. Drop the plugin jar (from [Releases](../../releases)) and
   **ProtocolLib** into your server's `plugins/` folder.
2. Start the server once - it creates default configs under
   `plugins/Scripted-SMP-Core/models/*/config.yml`.
3. Paste your license key into `models/core/config.yml` under `license.key`.
4. Use `/ssmp settings` (or `/ssmp menu`) to configure every module in-game,
   or edit the YAML files directly.
5. Run `/ssmp reload` to apply config changes without a restart.

---

## Documentation

- **[Wiki](wiki/index.md)** - the full user guide: setup, and how every module works
- **[Commands](COMMANDS.md)** - the full command reference (always current)
- **[Permissions](PERMISSIONS.md)** - every permission node, for LuckPerms/PEX setup (always current)
- **[Changelog](CHANGELOG.md)** - what changed in each version
- **[License](LICENSE.md)** - EULA and copyright terms

---

## Support

Ran into a bug, or have a question about your license? Join the official
**[Discord](https://discord.gg/mZVMPNHV64)**.

---

## Licensing

Scripted SMP Core is proprietary, closed-source software - see
[LICENSE.md](LICENSE.md) for the full terms. In short: a purchased license
key grants a non-exclusive, non-transferable right to run the Plugin on one
server; no source code is provided or licensed through this repository, and
the Plugin may not be decompiled, reverse-engineered, redistributed, or
resold.
