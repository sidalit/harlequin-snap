<div align="center">

<img src="snap/gui/harlequin.png" alt="Harlequin logo" width="128" />

# Harlequin

**The SQL IDE for your terminal**

[![harlequin](https://snapcraft.io/harlequin/badge.svg)](https://snapcraft.io/harlequin)
[![Base: core26](https://img.shields.io/badge/Base-core26-2C8C3C?logo=canonical&logoColor=white)](https://snapcraft.io/core26)
![Confinement: strict](https://img.shields.io/badge/Confinement-strict-2C8C3C)
[![Maintainer: sidaliteir](https://img.shields.io/badge/Maintainer-sidaliteir-2C8C3C?logo=snapcraft&logoColor=white)](https://snapcraft.io/publisher/sidaliteir)
![Architectures: amd64 and arm64](https://img.shields.io/badge/Architectures-amd64%20%7C%20arm64-2C8C3C?logo=linux&logoColor=white)

[Getting Started](#getting-started) · [Configure](#configure) · [Limitations](#limitations) · [Build](#build) · [Support](#support) · [License](#license)

Unofficial snap packaging for [Harlequin](https://github.com/tconbeer/harlequin), a terminal SQL editor with DuckDB, SQLite, Postgres and MySQL adapters.

</div>

---

## Getting Started

<a href="https://snapcraft.io/harlequin"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install harlequin
harlequin ./my-data.duckdb
```

Use `harlequin -a sqlite ./my-data.db` for SQLite. The headless command is available as `harlequin.hsql`.

## Configure

There are no `snap set` options. Configure Harlequin through its command-line options or configuration file.

Config and cache use `~/snap/harlequin/current`. Select an accessible config file with `harlequin --config-path ~/harlequin.toml`.

To access files under `/media` or `/mnt`:

```bash
sudo snap connect harlequin:removable-media
```

## Limitations

- Requires snapd 2.78 or newer. Container cgroup restrictions can still prevent DuckDB and `harlequin.hsql` from starting.
- Hidden files directly under your normal home directory are inaccessible; keep databases and config in an accessible folder.
- Clipboard copying requires terminal support for OSC 52.
- Host editors and built-in SSH tunnels are unavailable. Create SSH tunnels outside the snap and connect to the forwarded port.
- Only the four bundled database adapters are available.

## Build

```bash
git clone https://github.com/sidalit/harlequin-snap.git
cd harlequin-snap
sudo snap install snapcraft --classic
snapcraft pack
```

## Support

- **Installation or snap issues:** [open a packaging issue](https://github.com/sidalit/harlequin-snap/issues).
- **Application bugs:** [report them upstream](https://github.com/tconbeer/harlequin/issues).

## License

Snap packaging: [MIT](https://github.com/sidalit/harlequin-snap/blob/main/LICENSE).
