# Harlequin snap

[![harlequin](https://snapcraft.io/harlequin/badge.svg)](https://snapcraft.io/harlequin)

Snap packaging for [Harlequin](https://github.com/tconbeer/harlequin), the SQL IDE for your terminal. It includes the DuckDB, SQLite, Postgres and MySQL adapters.

Unofficial build, not affiliated with or endorsed by the Harlequin project.

## Build

```bash
snapcraft pack
```

## Install and try

<a href="https://snapcraft.io/harlequin"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install harlequin
sudo snap connect harlequin:removable-media   # optional: /media, /mnt
harlequin ./my-data.duckdb
harlequin -a sqlite ./my-data.db
```

The headless `hsql` command is available as `harlequin.hsql`.

## Known limitations

- Requires snapd 2.78 or newer. Container cgroup restrictions can still prevent DuckDB and `hsql` from starting.
- Config and cache live under `~/snap/harlequin/current`. Use `--config-path` for an accessible config file; hidden files directly under your normal home are unavailable.
- Clipboard copying requires a terminal that supports OSC 52.
- Host editors and built-in SSH tunnels are unavailable. Run SSH tunnels outside the snap and connect to the forwarded port.
- Only the bundled DuckDB, SQLite, Postgres and MySQL adapters are available.

## Update to a new upstream release

Change `version` in `snap/snapcraft.yaml`, then rebuild.

## Automation

Builds, publishing, and dependency updates use [snap-automation](https://github.com/sidalit/snap-automation).

## License

The packaging is MIT-licensed (see `LICENSE`). Harlequin is MIT-licensed; its dependencies carry their own licenses.
