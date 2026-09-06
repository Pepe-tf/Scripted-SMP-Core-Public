# Auto Kit

Create item kits in-game and assign them to teams. Members get the kit automatically when they join that team.

## What It Does

- Create kits in creative mode, or Quick Save your current gear as a kit instantly.
- Assign a kit to a team - members receive it automatically on join.
- Equip any kit to yourself with a single click.

## Commands

| Command | Permission | Description |
|---------|------------|-------------|
| `/ssmp autokit` (alias `kit`) | `ssmp.autokit.admin` | Open the Auto Kit GUI |

There are no further arguments or subcommands - every action (create, edit, delete, assign, Quick Save) happens inside the GUI.

## How to Create a Kit

1. Run `/ssmp autokit`.
2. Click **Create Kit**.
3. You're put in creative mode with a clear inventory.
4. Place the items you want into your inventory and armor slots.
5. Type the kit name in chat, or type `cancel` to abort.

## How to Equip or Edit a Kit

- **Left-click** a kit to instantly equip it to yourself.
- **Shift+Right-click** a kit to edit it - change the items in your inventory, then type `done` to save (or a new name to save as a copy), or `cancel` to discard.

## How to Delete a Kit

**Shift+Left-click** a kit once to arm deletion, then shift+left-click the same kit again within 5 seconds to confirm. Clicking a different kit, or waiting longer than 5 seconds, cancels the pending delete instead of confirming it.

## How to Assign a Kit to a Team

- From the Auto Kit GUI: **right-click** a kit, then pick a team from the list. The kit is applied immediately to every online member of that team.
- From a team's own Settings GUI: click the **Kit** item - left-click browses all kits, right-click opens a picker scoped to that one team (also lets you clear its assigned kit).

## Quick Save Kit

The **Quick Save Kit** button captures your current gear without entering the create flow:

- **Left-click** saves your current inventory, armor, and offhand as a kit, auto-named after you (`YourName`, `YourName-2`, and so on).
- **Shift+Right-click** additionally captures your health, hunger, saturation, XP, and active potion effects along with the items - applying that kit restores all of it, not just the inventory.

Quick Saves are grouped under one entry per player in the kit list instead of cluttering it with one item per save.

## Important Settings

Auto Kit has no config file - there's nothing to toggle, everything is managed in-game through the GUI.

## Permissions

| Permission | Default | Effect |
|------------|---------|--------|
| `ssmp.autokit.admin` | op | Open the Auto Kit GUI and manage every kit action - creating, editing, deleting, equipping, and assigning |

## Notes

- Kits are saved in `plugins/Scripted-SMP-Core/data/autokits.yml`, and synced to the database if one is configured.
- A kit that includes saved health/hunger/XP/potion effects only restores that extra state on apply - a kit without it (a normal create/edit or a plain Quick Save) leaves the target's current state untouched.
- Deleting a kit doesn't remove it from a team - reassign or clear the team's kit separately if needed.

## Related Pages

- [Teams](teams.md) - assign a kit to a team so members auto-equip
- [Settings GUI](settings-gui.md) - Auto Kit has no settings category since it has nothing to configure
