# Main Menu

The Main Menu is a central hub GUI that links every other module's GUI together, with a Home button and back-navigation on every screen.

## Opening the GUI

Run `/ssmp menu` (alias `/ssmp gui`). No permission is required to open the menu itself - each tile is individually gated, and anyone can at least reach Help.

## Tiles

| Tile | Requires | Opens |
|------|----------|-------|
| Settings | `ssmp.admin` | Settings GUI |
| Teams | `ssmp.team.gui` | Teams GUI |
| Auto Kits | `ssmp.autokit.admin` | Auto Kit GUI |
| Death List | `ssmp.deathlist.open` | Death List GUI |
| Respawn Points | `ssmp.respawn.manage` | Respawn Locations GUI |
| Immortal Manager | `ssmp.immortal` | Immortal Management GUI |
| Nickname | `ssmp.nick.set` | Nickname GUI |
| Help | *(none)* | Help GUI |

Tiles you don't have permission for still show up, but as a locked/greyed-out item instead of opening anything. Freeze and Chat have no tile here - they're command-only.

## Back-Navigation and Home

- Closing a sub-menu with **Back** returns you to whichever screen opened it - usually the Main Menu, but it can be several levels deep (for example Teams → Team Settings → Color Picker).
- If a GUI was opened directly by command rather than from the menu, Back falls back to the Main Menu instead of leaving you with nothing to return to.
- Every screen also has a dedicated **Home** button that jumps straight back to the Main Menu, skipping the back-navigation chain entirely.

> **Note:** Opening Settings or Help always starts at the first category and first page - neither one remembers where you left off the last time you opened it.

## Notes

- `/ssmp help` opens a separate, dedicated Help GUI (the command reference) rather than the Main Menu - the Main Menu's own Help tile opens the same GUI.
- The Help GUI groups every command into five tabs: All, Core, Manage, World, and Misc, filtered to only show commands you have permission to use.
- The credit button in the corner of the Main Menu prints the installed plugin version to chat.

## Related Pages

- [Commands](../COMMANDS.md) - full `/ssmp` command reference
- [Settings GUI](settings-gui.md) - the most commonly used tile
