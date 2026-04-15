# Changelog

All notable changes to this project will be documented in this file.

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
