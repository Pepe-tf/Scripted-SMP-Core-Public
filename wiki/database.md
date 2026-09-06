# Database

An optional MySQL or SQLite backend that syncs plugin data across multiple servers in a network. Config-file only - there's no in-game GUI or toggle for it.

## What It Does

Every module already saves its own data to local files regardless of whether the database is enabled - that's the restart-safe baseline and it never changes, even with the database off. Enabling the database adds a second, additional sync layer on top for:

- Immortal status
- Death and revive statistics
- Death List entries
- Nicknames and disguises
- Teams
- Auto Kits
- Respawn locations
- Chunk render preferences

The local file for each of these is always kept as the fallback. When the database is enabled, it becomes the source of truth across your network - its value takes precedence over the local file at startup and when a player joins.

## Enabling It

Edit `plugins/Scripted-SMP-Core/models/core/config.yml`:

```yaml
database:
  enabled: false      # set true to turn it on
  type: sqlite         # "sqlite" (local file) or "mysql" (remote)
  host: localhost
  port: 3306
  database: scripted_smp
  user: root
  password: ""
  use-ssl: false
  pool-size: 10
```

Run `/ssmp reload` after editing, or restart the server.

- **`type: sqlite`** stores everything in a local `data.sqlite` file in the plugin folder - no separate database server needed. Useful mainly as a staging step before pointing multiple servers at a shared MySQL instance.
- **`type: mysql`** connects to a remote MySQL server using the connection details above, pooled through HikariCP. This is what you want for an actual multi-server network sharing the same data.

## If You Leave It Disabled

Nothing changes. The plugin behaves exactly as it does today - everything above is saved locally and persists across restarts either way. The database only matters if you're running more than one server and want those values to follow a player between them.

## Notes

- Schema changes are tracked and applied automatically on startup - the plugin checks a stored schema version and runs any migrations needed to catch up, so upgrading the plugin with a database already configured doesn't require manual intervention.
- SQLite runs with a single connection (it doesn't support concurrent writers); MySQL uses a real connection pool sized by `pool-size`.
- Connection issues are retried automatically with backoff before anything is reported as failed.

## Related Pages

- [Immortal](immortal.md) - one of the things that syncs through the database
- [Death List](death-list.md) - death/revive statistics also sync through the database
- [Teams](teams.md) and [Nicknames & Disguises](nick.md) - also sync through the database when enabled
