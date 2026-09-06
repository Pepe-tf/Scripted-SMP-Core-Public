# Render Players

Hides players from each other beyond a configurable distance - independent of chunk render distance.

## What It Does

- Two players outside the visibility distance simply can't see each other, entity-wise - no fading, just a hard visible/hidden toggle.
- Admins with the bypass permission can be configured to always be visible to everyone, always be able to see everyone, or both.
- An optional cap limits how many players anyone can see at once, closest first, on top of the distance limit.

## Commands

| Command | Description |
|---------|-------------|
| `/ssmp rp status` | Show current settings |
| `/ssmp rp toggle` | Turn the module on/off |
| `/ssmp rp distance <blocks>` | Set the visibility distance |
| `/ssmp rp adminvisible` | Toggle whether bypass players are always visible to everyone |
| `/ssmp rp adminseeall` | Toggle whether bypass players can always see everyone |
| `/ssmp rp maxvisible <number>` | Set the max players anyone can see at once (0 = unlimited) |

Every `/ssmp rp` command requires `ssmp.admin`.

## Important Settings

| Setting | Default | Description |
|---------|---------|-------------|
| `enabled` | false | Turn the module on/off |
| `distance` | 5 | Max blocks apart two players can be and still see each other |
| `check-interval-ticks` | 5 | How often visibility is recalculated |
| `admin-visible` | true | `ssmp.renderplayer.bypass` holders are always visible to everyone, ignoring distance |
| `admin-see-all` | true | `ssmp.renderplayer.bypass` holders can always see everyone, ignoring distance |
| `max-visible` | 0 | Max players visible to any one viewer at once. 0 = unlimited (distance only) |

## Permissions

| Permission | Default | Effect |
|------------|---------|--------|
| `ssmp.renderplayer.bypass` | op | Grants both the always-visible and see-all behaviors above |

## Notes

- This is a straight visibility toggle (Bukkit show/hide player), not a fade or blur effect.
- `max-visible` only trims the normal, in-range player list - bypass players who are shown unconditionally aren't affected by the cap, but do count toward it.
- A world change is picked up on the next regular recheck, not instantly.

## Related Pages

- [Chunk Render](chunk-render.md) - a separate, complementary distance system
- [Debug](debug.md) - has a particle-overlay debug mode for this module too
- [Settings GUI](settings-gui.md) - configure every setting above without commands
