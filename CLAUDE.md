# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A personal notes/config repository for Music Player Daemon (MPD) setups — not a software project. There is no build, lint, or test tooling. Content is configuration files, a README, and a draw.io diagram.

## Architecture (the setup being documented)

The README describes a "NAS + laptop" topology:

- **Central server**: a single MPD instance on a NAS (TrueNAS) holds the whole music library.
- **Listening endpoints**: each listening location runs its own MPD server *and* client on a computer attached to the DAC/amp/speakers, pulling music from the NAS.

The TrueNAS server side is defined by two files that must stay consistent with each other:

- `truenas_mpd.yaml` — Docker Compose for the `tobi312/rpi-mpd:alpine` image. It bind-mounts NAS dataset paths (`/mnt/[dataset]/...` is a placeholder the user substitutes) into `/var/lib/mpd/{music,playlists,data}` and mounts `truenas_mpd.conf` read-only as `/etc/mpd.conf`. Exposes 6600 (MPD protocol) and 8000 (conventionally the HTTP stream port).
- `truenas_mpd.conf` — the MPD config. All paths in it (`music_directory`, `db_file`, `playlist_directory`, `log_file`, etc.) are *container* paths and must match the compose volume targets. It binds to `0.0.0.0` and advertises via zeroconf. It currently defines no `audio_output` block, so nothing serves port 8000 yet.

If you change a mount target in the YAML, update the matching path in the `.conf` (and vice versa).

## Assets

- `MPD Hardware Flowchart.drawio` is the editable diagram source; `assets/MPD_Hardware_Flowchart.drawio.svg` is the exported image embedded in `README.md`. Re-export the SVG when the diagram changes.

## Checking config changes

No CI exists. Useful manual checks when editing:

```sh
docker compose -f truenas_mpd.yaml config   # validate compose syntax
mpd --no-daemon --stdout --verbose truenas_mpd.conf   # parse-check the MPD config (paths must exist locally or errors are expected)
```

## Notes

- `.gitignore` excludes all `*.txt` files and `.env`.
