# Nicknames & Disguises

Players can set a cosmetic display name and color for themselves. Admins can set or reset anyone's nickname, copy skins, generate random identities in bulk, or fully disguise a player as another real Minecraft account. Every change goes live instantly for everyone nearby - no reconnect needed.

## What It Does

- Players pick their own nickname, color, and whether it replaces their floating nametag.
- Admins can set or reset any player's nickname, copy a skin from one player onto another, and reset skins.
- `/ssmp nick as` disguises a player as a real Minecraft identity - name and skin, if that identity is online or has a fetchable skin. This is an admin-only moderation/content tool, and every disguise is logged with who applied it.
- `/ssmp nick random` rolls a random adjective+noun nickname and a random skin pulled from a curated donor pool, either for one player or the whole server at once.
- Changes update the tab list, floating nametag, and world-rendered skin for everyone else immediately. This works the same for a real player, a Fake Player Plugin Origin bot, and a Bedrock/Geyser player. Only the changed player's **own** view of themselves (e.g. third-person) can't be live-updated this way - see [Self-View Reload](#self-view-reload-experimental) below.
- A player's real name and UUID never change - nicknames and disguises are cosmetic only, so permissions and moderation always resolve to the real account.

## Commands

All subcommands are under `/ssmp nick` (aliases `/ssmp name`, `/ssmp n`).

| Command | Permission | Description |
|---------|------------|-------------|
| `/ssmp nick` | `ssmp.nick.set` | Open the Nickname GUI (players only) |
| `/ssmp nick set <nickname> [color]` | `ssmp.nick.set` | Set your own nickname and color |
| `/ssmp nick reset` | `ssmp.nick.set` | Reset your own nickname |
| `/ssmp nick nametag [on\|off]` | `ssmp.nick.set` | Toggle your nametag override (flips if no argument) |
| `/ssmp nick status` | `ssmp.nick.set` | Show your current nickname, color, and nametag state |
| `/ssmp nick skin <player>` | `ssmp.nick.set` | Copy an online player's skin onto yourself |
| `/ssmp nick skinreset` | `ssmp.nick.set` | Clear your own skin override |
| `/ssmp nick random [--skin\|--name]` | `ssmp.nick.set` | Roll a random nickname and/or skin for yourself |
| `/ssmp nick other <player> <nickname> [color]` | `ssmp.nick.others` | Set another player's nickname |
| `/ssmp nick reset <player>` | `ssmp.nick.others` | Reset another player's nickname |
| `/ssmp nick skin other <player> <copyFrom>` | `ssmp.nick.others` | Copy one online player's skin onto another |
| `/ssmp nick skinreset <player>` | `ssmp.nick.others` | Clear another player's skin override |
| `/ssmp nick random <player> [--skin\|--name]` | `ssmp.nick.others` | Roll a random nickname and/or skin for one player |
| `/ssmp nick set <target> as <identity>` | `ssmp.nick.disguise` | Disguise a player as a real Minecraft identity (name + skin) |
| `/ssmp nick reset @a` | `ssmp.nick.manage` | Reset every stored nickname on the server |
| `/ssmp nick random @a [--skin\|--name]` | `ssmp.nick.manage` | Roll a random nickname/skin for every online non-op player |
| `/ssmp nick saveall` | `ssmp.nick.manage` | Force-save all nickname data immediately |
| `/ssmp nick refresh <player>` | `ssmp.nick.manage` | Force a full visual reload of a player for everyone |
| `/ssmp nick realname <player>` | `ssmp.nick.manage` | Show a nicked/disguised player's real name and UUID |
| `/ssmp nick debug <player>` | `ssmp.nick.manage` | Show full state: real name, UUID, nickname, color, nametag, skin override, and who disguised them (if anyone) |

`--skin` and `--name` on `random` are mutually exclusive - use one to roll only that half, or omit both to roll a new nickname **and** a new skin together.

## The Nickname GUI

Open with `/ssmp nick` (no arguments). Self-service only - it can't edit another player's nickname.

- Click **Nickname** to type a new one, **Color** to open the color picker, **Nametag** to toggle your nametag override. These stage as pending changes - nothing applies until you click **Apply**.
- Click **Skin** to copy an online player's skin - this applies immediately, it isn't staged.
- Click **Random** to roll a random nickname (staged, not yet applied).
- Click **Reset** to immediately clear your nickname, color, and nametag override.
- The **Preview** item shows what your pending changes will look like before you commit them.
- Closing the GUI or clicking **Back** without clicking **Apply** discards any staged nickname/color/nametag changes.

## Important Settings

| Setting | Default | Description |
|---------|---------|-------------|
| `enabled` | true | Turn the module on/off |
| `min-length` / `max-length` | 3 / 16 | Nickname text length limits (color doesn't count) |
| `alphanumeric-only` | true | Require nickname text to be letters/numbers only |
| `prevent-duplicates` | true | Block two players holding the same nickname at once |
| `cooldown-seconds` | 0 | Seconds between self-service nickname changes. `ssmp.nick.admin` always bypasses. 0 = no cooldown |
| `nametag-default-visible` | true | Whether a freshly-set nickname replaces the floating nametag by default |
| `prevent-real-player-names` | true | Block self-service nicknames matching a real account name. Doesn't affect `as` disguise, which exists specifically to do this on purpose |
| `prevent-real-player-names-check-offline` | false | Extend the check above to every player who has ever joined, not just online ones (heavier lookup) |
| `skins-enabled` | true | Master switch for skin copying (`/ssmp nick skin`) |
| `reload-on-change` | true | Instantly reload a changed player's name/skin for every observer, no reconnect. Leave this on |
| `random-nickname-enabled` | true | Allow `/ssmp nick random` |
| `disguise-enabled` | true | Allow `/ssmp nick set <target> as <identity>` |
| `reload-host` | *(empty)* | Experimental - see [Self-View Reload](#self-view-reload-experimental) |
| `reload-port` | 0 | Port override for `reload-host`, 0 = auto-detect |

## Self-View Reload (Experimental)

Everyone *else* sees a changed player's new name/skin live thanks to `reload-on-change`. The changed player's own view of themselves (third-person, their own client-side render) can't be updated that way - a client only renders its own skin from what it cached at login.

`reload-host` attempts to fix this by reconnecting the player back to the same server the instant their own appearance changes. It's **off by default and not recommended**: during testing, the reconnect reliably produced a hard client disconnect instead of a seamless one, even in the best-case scenario. Only enable this to experiment, and only test it on an alt account. Setting `reload-host` also requires your server to accept transfers (`accepts-transfers=true` in `server.properties`) - the plugin enables this for you automatically on startup if it's off, but the change needs a server restart to take effect.

## Permissions

| Permission | Default | Effect |
|------------|---------|--------|
| `ssmp.nick.set` | op | Set your own nickname, use the GUI, skin, nametag, status, and random (self) |
| `ssmp.nick.others` | op | Set, reset, or skin-copy another player |
| `ssmp.nick.admin` | op | Bypass length, character, duplicate, and cooldown restrictions |
| `ssmp.nick.disguise` | op | Disguise a player as a real identity via `as` |
| `ssmp.nick.manage` | op | Bulk operations (`reset @a`, `random @a`), `saveall`, `refresh`, `realname`, `debug` |

## Notes

- Disguising is a moderation/content-creation tool, not a way to evade identification - every disguise is recorded with who applied it, visible via `/ssmp nick debug <player>`.
- `random @a` deliberately skips online operators, so it's safe to run during a minigame round without accidentally randomizing staff who are watching.
- If a disguise identity has no real skin to copy, or `/ssmp nick random` rolls a skin, the plugin pulls from a curated donor pool of real, skinned Minecraft accounts instead of leaving it blank.
- A player's UUID is never changed by any of this - only their displayed name and skin - so permissions and other plugins always resolve the real account underneath.
- Nickname data is saved to `plugins/Scripted-SMP-Core/data/nicks.yml`, and also synced to the database if one is configured.
- `debug.nick` in the Debug settings category logs the appearance-reload pipeline in detail - useful if a name/skin change isn't showing up for everyone.

## Related Pages

- [Teams](teams.md) - team glow and colors work alongside nicknames
- [Settings GUI](settings-gui.md) - the Nickname category covers every setting above
- [Permissions](../PERMISSIONS.md) - every `ssmp.*` node
