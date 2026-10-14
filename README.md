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
sudo snap install harlequin                   # or a local build: ./harlequin_2.16.1_*.snap --dangerous
sudo snap connect harlequin:removable-media   # optional: /media, /mnt
harlequin ./my-data.duckdb
harlequin -a sqlite ./my-data.db
```

The headless `hsql` command is available as `harlequin.hsql`.

## Known limitations

### Needs snapd 2.78 or newer

DuckDB reads the memory limit of its cgroup (`memory.max`) when it starts. Before snapd 2.78, strict confinement blocks that file for apps started from a user session, and DuckDB aborts with `Attempted to dereference unique_ptr that is NULL!`. This also breaks the SQLite adapter's `hsql`, which uses DuckDB internally. Check with `snap version` and, if needed, run `sudo snap refresh snapd`.

For the same reason, DuckDB still aborts inside LXD containers, where `/sys/fs/cgroup/memory.max` exists at the root and stays blocked.

### Only amd64 and arm64

DuckDB and PyArrow, which Harlequin needs, publish wheels for amd64 and arm64 only. Building them from source for the other architectures is not practical, so the snap is built for these two.

### Config and cache files

Inside the snap, your home folder for config and cache is `~/snap/harlequin/current`. Harlequin reads its config from `~/snap/harlequin/current/.config/harlequin/config.toml` instead of `~/.config/harlequin/config.toml`, and does not see a `~/.harlequin.toml`. A `harlequin.toml`, `.harlequin.toml` or `pyproject.toml` in the current folder is still found, and `--config-path` accepts any non-hidden file in your home folder. DuckDB extensions are downloaded to `~/snap/harlequin/current/.duckdb`.

### Clipboard

Copying uses the OSC 52 terminal escape, which works in most modern terminals. The system clipboard tools (`xclip`, `wl-copy`) are not available inside the snap.

### SSH tunnels and external editor

`--ssh-host` and opening a buffer in `$EDITOR` run programs from your system, which a strict snap cannot reach. Run SSH tunnels yourself (`ssh -L ...`) and connect Harlequin to the forwarded port.

### Other adapters

Only the DuckDB, SQLite, Postgres and MySQL adapters are included. Adapters cannot be added to an installed snap.

## Update to a new upstream release

Change `version` and `source-tag` in `snap/snapcraft.yaml`, then rebuild.

## License

The packaging is MIT-licensed (see `LICENSE`). Harlequin is MIT-licensed; its dependencies carry their own licenses.
