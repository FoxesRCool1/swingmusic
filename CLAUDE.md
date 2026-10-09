# Swing Music

Self-hosted music streaming server in Python (Flask) with a Vue.js frontend.
Features: daily mixes, metadata normalization, album versioning, multi-user, Last.fm scrobbling.

## Run

uv sync --group dev && uv run python -m swingmusic    # starts on http://localhost:1970

## Test

No dedicated test suite in the repo. Locust is in deps for load testing.
Run `uv run python -m swingmusic --test-pro-imports` to verify premium module imports.

## Folder map

src/swingmusic/api/         REST endpoints (Flask-OpenAPI3 blueprints)
src/swingmusic/models/      dataclasses (Track, Album, Artist, Playlist, User)
src/swingmusic/store/       in-memory O(1) hash maps
src/swingmusic/db/          SQLAlchemy + SQLite layer
src/swingmusic/lib/         core business logic (scanning, tagging, search)
src/swingmusic/plugins/     optional plugins (lyrics, mixes, lastfm)
src/swingmusic/crons/       background scheduled tasks
src/swingmusic/premium/     compiled premium modules (.so, Nuitka)
src/swingmusic/setup/       startup: dirs, DB init, migrations
docs/                       architecture and streaming docs
contributing/               contributor README

## Gotchas

- Requires Python 3.11+; ffmpeg must be on PATH
- Premium modules ship as .so; build with `bash scripts/compile-premium-modules.sh`
- `run.py` is the PyInstaller entry point, not the dev entry — use `python -m swingmusic`
- Port defaults to 1970; override with `--port` or `SWINGMUSIC_PORT`
- Client (Vue.js SPA) is served from `client/` or passed via `--client <path>`
