# command-center

A fast task manager with a CLI (`task`), a terminal UI (`task-tui`) and a local web UI. This repository hosts the prebuilt binaries and the installer. The source code is private.

## Install

```sh
curl -fsSL https://raw.githubusercontent.com/TheSophist1976/command-center-releases/main/install.sh | sh
```

Then set it up and start the web UI:

```sh
task setup     # choose your task and notes directories; installs AGENTS.md and the Claude skills
task serve     # web UI at http://127.0.0.1:4287
```

The installer:

- detects your OS and CPU and downloads the matching archive from the latest **stable** release;
- verifies its SHA-256 checksum against the release's `SHA256SUMS` and aborts if it doesn't match;
- installs `task` and `task-tui` into `~/.local/bin`, and offers to add that directory to your `PATH` (it prints the line to add if it can't ask).

It does nothing else: no configuration happens until you run `task setup`.

### Options

| Variable | Effect |
| --- | --- |
| `INSTALL_DIR` | Install somewhere other than `~/.local/bin` |
| `RELEASE_TAG` | Install a specific release instead of the latest stable one, e.g. `RELEASE_TAG=v4.2.0` |

Set them on the `sh` side of the pipe:

```sh
curl -fsSL https://raw.githubusercontent.com/TheSophist1976/command-center-releases/main/install.sh | RELEASE_TAG=v4.2.0 INSTALL_DIR=~/bin sh
```

Pre-releases (tags like `v4.1.0-rc.1`) are skipped by default; pin one with `RELEASE_TAG` to install it.

If you'd rather read the script before running it, it's [`install.sh`](install.sh) in this repository.

## Update

```sh
task update            # install the latest release
task update --check    # only report whether an update is available
```

The web UI also shows the running version in its header and, when a newer release exists, an **Update** button. It restarts the server automatically (expect a second or two of downtime). If `task serve` is already running when you use `task update` from the command line, restart it to finish the update.

## Supported platforms

| OS | CPU |
| --- | --- |
| macOS | Apple Silicon (arm64), Intel (x86_64) |
| Linux | x86_64, arm64 |

Windows is not supported. Linux binaries are built on Ubuntu 22.04 against glibc, so very old distributions may not run them.

## Verifying downloads

Each release publishes `SHA256SUMS` next to the archives (`task-vX.Y.Z-<target>.tar.gz`). The installer and `task update` both check it automatically. The binaries are **not code-signed or notarized**, so the checksum protects against corrupted or tampered downloads from the release page, not against a compromised release.

## Releases

See the [Releases](../../releases) page for all versions.
