# Changelog

All notable changes to **Scripted SMP Core** are documented in this file.

---

## [1.2.5.1] - 2026-09-06

### Added
- `/ssmp team add <team> radius:<blocks>` - add every online player within range to a team
- `/ssmp tp <player|@a|--team <name>|--random <amount>> <destination>` - teleport a team or a random subset of players, not just `@a` or one player
- `/ssmp kit <kit> <player>` and `/ssmp kit set <team> <kit>` - apply or assign a kit from the command line, no GUI needed
- `/ssmp team fixhealth <player>` - force-resync a player's max health right now

### Fixed
- Disguising as an offline player could silently hand them a random stranger's skin instead of the real one when Mojang's lookup was rate-limited, with no indication why
- `/ssmp nick skin` (and `skin other`) now fetches from Mojang instead of requiring the source player online
- Team Max HP could leave a player stuck on a custom value forever if their team was deleted without kicking them first, especially once they were made admin/op

---

## [1.2.5] - 2026-08-29

### Added
- `/ssmp sudo <player|nickname> <command|message>` - force a player to run a command or send a message
- `/ssmp broadcast <message> <seconds>` - chat announcement with an optional big on-screen title; `stop` cancels it early
- `/ssmp chat clear` - clears chat for every online player
- `/ssmp fly` and `/ssmp flyspeed <1-10>` - self-service flight and fly speed
- `/ssmp invsee <player|nickname>` - live, editable view of a player's inventory, FPP Origin bot-inventory styled; also opens via right-click in creative
- Shift-right-click a player (creative) for the new Player Settings GUI - per-player overrides for chunk render, visibility, immortal, nickname, team, kit, and every global setting
- `/ssmp sethp <player|nickname> <hearts>` - set exact health (e.g. `0.5`), auto-lowering hunger just enough to block healing without killing sprint
- `/ssmp sethunger <player|nickname> <0-20>` - set food level directly
- Teams can now set a Max HP, capping every non-admin member's health

### Changed
- Team auto-assign now skips ops/admins by default
- Create/Edit Team GUIs reworked - denser layout, Max Size/HP set via click cycle instead of typing

### Fixed
- Nicknamed players weren't recognized by nickname in `/tp` and other commands
- A corrupted `nicks.yml`/`autokits.yml` crashed the whole plugin on startup; now recovers, backs up the broken file, and starts fresh instead - root cause (YAML line-wrap corrupting long skin data) fixed too
- Broadcast's divider could wrap into two lines, and its duration tab-complete could appear mid-message
- Closing Invsee could roll back items picked up while open; sync is now fully event-driven

---

## [1.2.4] - 2026-08-22

### Added
- Nicknames: `/ssmp nick` (or `/nick`, `/name`, or the new Nickname GUI) lets a player set a cosmetic display name; admins can set/reset others, exempt from rules, or disguise a player as another real identity/skin.
- Team leaders (`/ssmp team setleader`), team alliances (`/ssmp team ally`), and locked teams (max size `-1`, keeps identity without allowing joins).
- Gamemode shortcuts (`/gmc`, `/gms`, `/gma`, `/gmsp`, short forms like `s`/`c`/`a`/`sp`/`0`-`3`).
- Auto Kit / Team integration: assign or view a team's kit directly; Quick Saves now grouped and alphabetized.
- Fake Player Plugin Origin 0.26.20.2+: bots prioritize team leaders as targets, defend an attacked leader, and respect team alliances.

### Fixed
- Nickname/skin changes now fully reload for every observer instantly (tab list, nametag, world-render) - previously stuck until reconnect; follow-up fixes for bots' real skins, name-only changes, and disguising an already-disguised player.
- Nonsensical renamed join/quit messages for bots; duplicate-identity disguises now rejected.
- Several GUIs had wrong/invisible button states (dead next-page arrow, disabled buttons looking active, stray glass panes); Quick Save kits losing their ownership tag on edit; team glow nametag ignoring its master toggle.
- Seven commands printed a raw Component dump instead of colored text.

### Changed
- Nick command syntax reordered for clarity; `as <identity>` no longer requires a previously-seen player (fetches from Mojang); `resetall` replaced by `reset @a`; `random`/`random @a` now also randomizes skin and skips ops.
- Auto Kit deletion now requires a confirm click.

### Security
- License key is now encrypted at rest instead of plain text; the device identifier that keeps license verification stable across restarts moved out of a plain, discoverable file into hardened, disguised storage.

### Removed
- Dead, unused `AutoKitSelectGUI` screen.

---

## [1.2.3] - 2026-08-03

### Added
- "Auto Assign" button in a team's own member-list GUI - adds every unassigned online player directly to that specific team, instead of spreading them across whichever team has the fewest members
- `TeamManager`/`FreezeManager` published via Bukkit's `ServicesManager`, so other plugins can check team membership and freeze state - Fake Player Plugin Origin's bots now never auto-target/fight-back a teammate and actually honor `/ssmp freeze`
- Startup banner now shows whether Fake Player Plugin Origin is installed (and its version) under a new "Compatibility" section

### Fixed
- Editing an existing Auto Kit always saved it as empty - the inventory was cleared before the edit was captured back out of it, not after. Capture now happens first
- Assigning/removing a team for many players at once could stutter or freeze the server on large player counts - batched once now instead of per-player
- Auto-assign always skipped anyone with `ssmp.admin`. Off by default now; re-enable with `team.auto-assign-skip-admins`
- Database silently didn't work at all on MySQL - a startup query used SQLite-only index syntax
- A migration comparing old/new death-list files by size could pick the wrong one and lose data
- A corrupted `migration-meta.json` crashed startup instead of falling back to a fresh one
- Team module's bundled config was stuck on an old version, so `team.default-color` never actually applied to newly created teams
- Every config save-on-load created two backups instead of one

---

## [1.2.2] - 2026-08-02

### Changed
- Team glow rebuilt - per-viewer color now uses personal scoreboards instead of hand-rewritten packets; color-setting logic centralized instead of duplicated across four files
- Admin/global glow toggle now actually hides the outline, not just recolors it white, via a narrow packet filter
- Destructive bulk actions (Clear All Teams, Remove All members) now require shift-click, matching Death List
- Team color logic (icon + display color) consolidated into one shared utility
- Gradle's `obfuscate` task now runs clean → build → obfuscate in one click

### Added
- Empty-state placeholders across every list GUI when it has nothing in it yet
- Immortal status now survives a restart with no database configured
- Death/revive stats now also sync to the database
- Database schema migrations are now real, not dead scaffolding

### Fixed
- Immortal Manager could hold a stale reference to a disconnected player
- `team.enabled` did nothing
- Crash in team info/GUI when a team has no creator
- Crash ("Team colors must have hex values") on join or reload on some Paper builds
- Team-colored names could leak into death/quit/join messages for OP'd players
- FakePlayerPlugin bots were never detected (wrong key), causing duplicate leave messages
- Death/revive stats could lose up to an hour of data on restart

### Removed
- `team.highlight-members` - never actually implemented

---

## [1.2.1] - 2026-07-06

### Added
- **Main Menu GUI** (`/ssmp menu`) - central hub linking Settings, Teams, Auto Kits, Death List, Respawn, Immortal, and Help
- **Home button** on every menu
- **Quick Save Kit button** in the Auto Kit GUI - one click saves your current kit; Shift+Right-click also saves health, hunger, XP, and potion effects
- **New debug toggles** for Auto Kit, Respawn, and Death Sound in Settings
- **Update checker** - warns in console and in-game (admins) when a new version is out; run `/ssmp update` to check manually
- Hardened anti-piracy protections
- License offline grace period now actually works (keeps running through a license-server outage instead of locking)

### Changed
- **Auto Kit clicks reworked** - left-click equips a kit, Shift+Right-click edits it
- **Menu navigation fixed** - menus remember your place and Back always works, instead of sometimes closing or losing your spot
- Cancelling a dialog now returns you to the menu that opened it
- Color picker only applies your choice on Confirm
- Settings now saves when switching menus, not only on close

### Fixed
- Death List "Clear All" button was invisible and unusable
- Team color picker wasn't actually applying the chosen color
- Auto Kit creation could get you stuck at the kit list, or clear your inventory unnecessarily
- Crash on player join caused by a Paper/Minecraft chat update
- Crash when finishing/cancelling an Auto Kit edit in chat
- Auto Kit was applied twice on every respawn
- Chat obfuscation was replacing letters instead of whole words
- "Spectator on death" setting was not enforced
- Config reload could drop new settings; config backups piled up forever
- Team/Auto Kit/Respawn data wasn't always saved on shutdown
- **Auto Kit Manager duplication exploit** - Create/Edit could leave the menu open and unprotected, letting items be dragged out into your inventory

---

## [1.2.0] - 2026-06-26

### Added
- **Configurable death kick delay** (`death-list.kick-delay-ticks`, default 0.5s)
- **Team colors** - pick a color per team, shown in previews, nametags, and glow
- **Team glow system** - per-team colored outlines, with an admin-only toggle

### Changed
- `/ssmp license` is now admin-only
- Cancelling a dialog closes it instead of reopening the parent menu

### Fixed
- License-locked boss bar not disappearing for all players after activation

---

## [1.1.1] - 2026-06-23

### Removed
- Free trial mode - a valid license key is now always required

### Fixed
- RSA public key decoding (now supports more key formats)
- Misleading error message on signature failures

---

## [1.1.0] - 2026-06-23

### Added
- Runtime integrity/tamper check at startup
- Internal string encryption to resist static analysis
- Database auto-retry on connection drops, with schema version tracking
- `/ssmp debug team-glow` toggle

### Changed
- Database module overhaul - unified storage with caching and batch writes
- Team config revamped with several new/renamed options
- Immortal status now persists across restarts and servers
- Immortal damage capping fixed

### Fixed
- Team glow colors on newer Paper versions
- Various Team GUI edge cases

---

## [1.0.0] - 2026-06-15

### Added
- **Help GUI** (`/ssmp help`) - searchable, categorized command reference
- **Team Clear-All button** - removes every player from every team in one click

### Changed
- Visual theme overhaul across all GUIs and commands
- First stable release, consolidating all modules

---

## [1.0.1-prerelease] - 2026-06-12

### Fixed
- Fake leave message color for admin bypass

---

## [1.0.0-prerelease] - 2026-06-12

Major update adding team, auto kit, respawn, and death effect systems.

### Added
- **Teams** (`/ssmp team`) - named teams, glow outlines, GUIs, auto-assign
- **Auto Kits** - create/edit kits in-game and assign them to teams
- **Respawn locations** - GUI-managed, with fallback and cooldown
- **Death statistics & effects**
- ProtocolLib is now a required dependency
- `PERMISSIONS.md` reference document

### Changed
- GUI overhaul (reusable inventories, centralized click handling)
- Every module now uses its own config file

### Fixed
- Inventory interactions leaking outside plugin GUIs

---

## [0.4.0-beta] - 2026-06-08

### Added
- 24-hour free trial mode
- License system with hardware-locked verification
- Immortal Management GUI
- Freeze system (`/ssmp freeze`)
- Colored, per-subsystem console logs
- Death kick delay, join/quit toggles, death list admin bypass

### Changed
- Chat now works reliably across worlds
- Immortal GUI search, freeze command, and skin loading improved

### Fixed
- License setup crash, soft-ban bypass bug, frozen players still able to act, missing OP death messages, cross-world chat breakage

---

## [0.3.1-beta] - 2026-06-07

### Changed
- Now works on Java 21+ (previously required Java 25)

---

## [0.3.0-beta] - 2026-06-07

### Added
- **Render Players module** - hides distant players, with admin bypass
- **Unified Debug module** with per-subsystem toggles
- Chunk render rewrite - AFK/ping-aware, Geyser and LuckPerms support
- Chat system overhaul with proximity events
- Per-module config files and automatic config migration

### Changed
- Settings GUI reorganized into 7 categories

---

## [0.2.0-beta] - 2026-06-06

### Added
- **Chunk render distance controller** - per-player settings with smart layered limits (default, saved preference, LuckPerms cap, admin override, AFK/ping/dynamic reduction)
- `/ssmp chunk` command suite and matching permissions
- Settings pagination and better icons

### Fixed
- Items getting stuck when clicking in GUIs

---

## [0.1.0-beta] - 2026-06-05

### Added
- Hardcore death ban, proximity death sound, proximity join/leave/death messages
- Immortality system (`/ssmp immortal`)
- Chat prefix/suffix and a chat debug visualizer
- Sleep voting (disabled by default)

### Fixed
- Chat formatting tags, chat delivery to bypassed players, player names breaking chat formatting, missing death list head skins

---

## [0.0.1-beta] - 2026-06-04

### Added
- **Death List** - tracks player deaths with a management GUI and soft-ban
- **Death Sound** on player death
- **Chat system** with distance-based filtering
- **Settings GUI** with 4 categories
- `/ssmp` core command and tab completion

### Fixed
- Startup crash, deprecated sound API, stuck death screen, inventory interactions outside plugin GUIs
