# zaima

`zaima` is a small Bash utility that checks whether a set of AI coding CLIs are available, whether they appear to be logged in, and which version is installed.

It is designed for one-shot terminal use:

```bash
zaima
```

In a normal interactive terminal it renders a small dashboard:

```text
+----------------------------------------------------------------------------+
| ZAIMA Dashboard                                                            |
| AI CLI login + version monitor | assistants: 4 | timeout: 20s             |
+----------------------------------------------------------------------------+
| assistant              | login  | version                                  |
+----------------------------------------------------------------------------+
|  COD  codex        |   OK   | codex-cli 0.120.0                          |
|  CLA  claude-code  |   OK   | 2.1.97 (Claude Code)                       |
|  GEM  gemini       |   OK   | 0.37.2                                     |
|  HER  hermes-agent |   OK   | Hermes Agent v0.9.0 (2026.4.13)            |
+----------------------------------------------------------------------------+
| summary | ok=4 | no=0 | missing=0                                       |
+----------------------------------------------------------------------------+
```

When stdout is not a TTY, it falls back to compact plain text:

```text
[COD] codex        | login ok | version codex-cli 0.120.0
[CLA] claude-code  | login ok | version 2.1.97 (Claude Code)
[GEM] gemini       | login ok | version 0.37.2
[HER] hermes-agent | login ok | version Hermes Agent v0.9.0 (2026.4.13)
```

## What It Checks

`zaima` currently checks these assistants:

- `codex`
- `claude-code`
- `gemini`
- `hermes-agent`

For each one it reports:

- whether the command exists on `PATH`
- whether the current user environment appears to be authenticated
- the installed CLI version

## Why This Exists

Most AI CLIs expose login state and version information differently. `zaima` normalizes those checks into one command so you can quickly answer:

- Is the CLI installed?
- Is it logged in?
- Which version is actually being used?

## Requirements

- Bash
- `timeout`
- `rg` (ripgrep)

Optional but expected for full results:

- `codex`
- `claude`
- `gemini`
- `hermes`

If a command is missing, `zaima` prints `login=missing`.

## Installation

### Option 1: run from the repository

```bash
git clone https://github.com/gigode/zaima.git
cd zaima
./zaima
```

### Option 2: symlink into your `PATH`

```bash
ln -sf "$(pwd)/zaima" ~/.local/bin/zaima
```

Then:

```bash
zaima
```

## Usage

### Default

```bash
zaima
```

### Disable the spinner

```bash
ZAIMA_PROGRESS=0 zaima
```

### Disable the dashboard panel

```bash
ZAIMA_DASHBOARD=0 zaima
```

### Increase per-check timeout

```bash
ZAIMA_TIMEOUT=60 zaima
```

### Help and version

```bash
zaima --help
zaima --version
```

## Output Format

TTY mode:

- renders a dashboard panel with themed assistant badges
- shows live per-check spinner progress
- prints a summary footer with aggregated status counts

Non-TTY mode:

- prints one compact line per assistant

Status meanings:

- `ok`: the assistant command exists and the current environment appears authenticated
- `no`: the assistant command exists but authentication was not detected
- `missing`: the command is not available on `PATH`

## Authentication Detection Strategy

`zaima` intentionally uses the current user environment instead of an isolated temp home, so it reflects the login state you actually use at the terminal.

Current checks:

- `codex`: `codex login status`
- `claude-code`: `claude auth status --json`
- `gemini`: local Gemini auth configuration under `~/.gemini/`
- `hermes-agent`: `hermes auth list`

## Progress Display

When stdout is a TTY, `zaima` shows a single-line spinner while each assistant is being checked:

```text
[2/4] checking claude-code  /
```

The progress line is cleared automatically when the check finishes, so the dashboard stays readable.

## Known Limitations

- `zaima` reports login state, not full end-to-end prompt execution health.
- `gemini` authentication is currently detected from local config presence rather than a live prompt round-trip.
- The script is intended for quick terminal inspection, not strict machine-verified CI gating.

## Repository Layout

```text
zaima         Main executable Bash script
README.md     User documentation
CHANGELOG.md  Release history
CLAUDE.md     Repository guidance for coding agents
```

## Development

Basic checks used for this repository:

```bash
bash -n ./zaima
./zaima
```

## Release

Current documented release line: `v0.2.0`
