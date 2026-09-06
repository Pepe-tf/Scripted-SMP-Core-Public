# Death Sound

The Death Sound module plays a sound whenever a player dies.

## What It Does

- Plays a configurable sound on every player death.
- Can be restricted to nearby players with proximity mode.

## Commands

There are no commands for this module. `Enabled` and `Proximity Only`/`Hearing Range` can be changed from `/ssmp settings`; the sound, volume, and pitch are shown there for reference but are only editable by hand-editing the config file.

## Important Settings

| Setting | Default | Description |
|---------|---------|-------------|
| `enabled` | true | Turn the module on/off |
| `sound` | `entity.wither.spawn` | Sound to play |
| `volume` | 1.0 | Sound volume |
| `pitch` | 1.0 | Sound pitch |
| `proximity.enabled` | false | Only nearby players hear it |
| `proximity.distance` | 500 | Proximity range |

## Notes

- Use any valid Minecraft sound key, like `entity.wither.spawn`.
- This works even if the Death List module is disabled.
- Enable the Death Sound toggle in the Debug category to log trigger/proximity checks to console.

## Related Pages

- [Death List](death-list.md) - the death event that triggers this sound
- [Debug](debug.md) - troubleshoot proximity mode
