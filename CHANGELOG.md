# Changelog

All notable changes to this project will be documented in this file.

## 0.2.0 - 2026-04-15

Dashboard-style terminal release.

### Added

- TTY dashboard layout with header, table rows, and summary footer
- Per-assistant themed badges for `codex`, `claude-code`, `gemini`, and `hermes-agent`
- Color-coded login status badges
- Dashboard summary counts for `ok`, `no`, and `missing`

### Changed

- Interactive terminal mode now renders a richer monitoring-style panel instead of plain result rows
- Non-TTY output still falls back to compact plain text for piping and scripts

### Notes

- Dashboard mode is enabled automatically on TTY output
- Existing `ZAIMA_PROGRESS=0` behavior remains supported

## 0.1.0 - 2026-04-15

Initial public release.

### Added

- One-command AI CLI status checker via `zaima`
- Checks for `codex`, `claude-code`, `gemini`, and `hermes-agent`
- Normalized output format for login state and installed version
- Single-line spinner progress for interactive terminal use
- `--help` and `--version` support
- README with installation, usage, output format, and limitations

### Notes

- `gemini` login state is inferred from local auth configuration files
- `zaima` is optimized for quick terminal inspection rather than strict CI validation
