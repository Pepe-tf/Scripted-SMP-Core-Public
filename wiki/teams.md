# Teams

Named teams with colors, glow outlines, a designated leader, and alliances between teams. Fully admin-managed - there's no self-service join, players are added by an admin through the GUI.

## What It Does

- Admins create and manage teams through a paginated GUI. Each team has a **name**, **color**, optional **leader**, optional **max size**, optional **max HP**, and optional **glow**.
- **Max HP**: caps every non-admin/op member's health at a custom amount instead of the vanilla 10 hearts - set it with a left/right/shift-click on the Max HP item in the Create Team or Team Settings GUI (left/right adjusts by 1 heart, shift by 10; right-clicking down to 0 resets it to the default). Applied and kept in sync automatically as members join, leave, or reconnect - server ops and `ssmp.admin` holders are never affected.
- **Leaders**: any admin can designate one member as a team's leader with `/ssmp team setleader`. Scripted SMP Core itself just stores who the leader is and exposes it to other plugins - it's compatible bot/NPC plugins (like Fake Player Plugin Origin) that actually use it for target-priority or defend-the-leader behavior.
- **Alliances**: two teams can be allied with `/ssmp team ally`. Allied teams' members can never deal PvP damage to each other, regardless of the global friendly-fire setting. As with leaders, whether bots avoid auto-targeting allies is up to whatever bot plugin you're running - this module only tracks and exposes the alliance.
- **Locked teams**: setting a team's max size to `0` locks it - nobody can join, but existing members are untouched. This is meant to preserve a team's identity (name, color, kit, alliances) between "scenes" without accepting new members. A negative max size (the default, `-1`) means unlimited.
- **Two different Auto Assign actions exist** - the main Teams GUI's Auto Assign button (and `/ssmp team autoassign`) spread every un-teamed online player across *all* teams, smallest first. The Auto Assign button inside a specific team's own member list instead adds every un-teamed player directly into *that one team*.
- Each team can be linked to one Auto Kit, applied automatically when a member joins the team.
- Friendly fire within a team can be toggled server-wide; alliance damage cancellation is unconditional and separate from that setting.
- Admin glow override lets admins/ops see normal colored glow while normal players see none, or vice versa, depending on how it's configured.

## Commands

Every `/ssmp team` subcommand requires `ssmp.team.admin` - there's no lighter self-service tier at the command level (the finer permissions below only matter for individual GUI buttons).

| Command | Description |
|---------|-------------|
| `/ssmp team` | Open the Teams GUI |
| `/ssmp team create` | Open the Create Team GUI |
| `/ssmp team leave` | Leave your current team |
| `/ssmp team info <team>` | Show member count, lock state, creator, leader, and allies |
| `/ssmp team kick <player>` | Remove a player from their team |
| `/ssmp team setleader <player>` | Set that player as their team's leader (must already be a member) |
| `/ssmp team ally <team1> <team2>` | Toggle an alliance between two teams on/off |
| `/ssmp team allies <team>` | List a team's current allies |
| `/ssmp team autoassign` (alias `aa`) | Spread every un-teamed online player across all teams, smallest first |

There's no `/ssmp team join` command - adding a player to a team is done from the GUI (Teams → pick a team → **+ Add Player**).

## Important Settings

| Setting | Default | Description |
|---------|---------|-------------|
| `enabled` | true | Turn the module on/off |
| `default-color` | WHITE | Color assigned to newly created teams before an admin picks one |
| `default-max-size` | -1 | Default max members per new team. `0` = locked, negative = unlimited, positive = a hard cap |
| `max-teams` | 100 | Max number of teams |
| `global-friendly-fire` | false | Allow teammates to hurt each other |
| `alphanumeric-names` | true | Require team names to be alphanumeric |
| `min-name-length` / `max-name-length` | 1 / 16 | Team name length limits |
| `auto-assign-on-join` | false | Auto-assign un-teamed players on join |
| `auto-assign-skip-admins` | true | When on, Auto Assign skips players with `ssmp.admin` or server op - on by default, so a scene's admins/ops don't get swept into a team by accident |
| `glow-enabled` | true | Show team glow |
| `glow-global` | true | When OFF, nobody sees any glow outline or color at all |
| `glow-admin` | true | When ON, admins/ops see normal team-colored glow. When OFF, admins/ops see none while normal players are unaffected |

## The GUIs

- **Teams GUI** (`/ssmp team`) - paginated team list. Left-click a team to see its members, right-click for its settings, shift-click to delete. Bottom row: Create Team, Auto Assign (spreads across all teams), Clear All Teams (shift-click to confirm).
- **Create Team GUI** - set name, color, max size, and max HP (all adjusted with a left/right/shift-click cycle), then confirm. The team starts empty - the creator isn't automatically added as a member.
- **Team Settings GUI** - rename, recolor, set/clear leader, change max size, change max HP, disband, and manage allies or the team's kit. Any member can leave from here; the rest requires `ssmp.team.admin`.
- **Team Member List** - shift-click a member to toggle them as leader, click to kick, or use Add Player / Remove All / Auto Assign (scoped to this one team).
- **Team Alliances GUI** - a paginated list of every other team; click one to toggle the alliance.

## Permissions

| Permission | Effect |
|------------|--------|
| `ssmp.team.admin` | Full team management - required for every `/ssmp team` command |
| `ssmp.team.gui` | Open the Teams GUI from the Main Menu and see it in the tile list |
| `ssmp.team.create` | Use the Create Team button in the GUI |
| `ssmp.team.leave` | Use the Leave Team button in the GUI |
| `ssmp.team.glow.bypass` | See team glow/color even when admin glow is turned off for admins |

## Notes

- Teams are saved in `plugins/Scripted-SMP-Core/data/teams.yml`.
- Bulk actions (Clear All Teams, Remove All in a member list, both Auto Assign buttons) require a **shift-click** to confirm, and are batched internally so assigning or removing many players at once doesn't stutter the server.
- Colors are picked through an in-game 16-color palette in the Create / Settings GUIs.
- Other plugins can read live team membership, leader, and alliance data through Bukkit's `ServicesManager` (the plugin publishes its `TeamManager` there) - this is how compatible bot/NPC plugins avoid targeting teammates or allies, and prioritize a team's leader.

## Related Pages

- [Auto Kit](auto-kit.md) - assign a kit to a team for instant equip
- [Nicknames & Disguises](nick.md) - nicknames survive joining or leaving a team
- [Settings GUI](settings-gui.md) - configure glow, friendly fire, and name limits
- [Admin Tools](admin-tools.md) - the Player Settings GUI can force-join/remove a player from a team per-player
