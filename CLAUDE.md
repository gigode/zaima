# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This repository contains `zaima`, a Bash utility that reports login state and installed version information for multiple AI coding CLIs.

## Commands

```bash
./zaima                  # Run all checks
./zaima --help           # Show usage
./zaima --version        # Show tool version
ZAIMA_TIMEOUT=60 ./zaima # Increase per-check timeout
ZAIMA_PROGRESS=0 ./zaima # Disable spinner progress output
```

## Architecture

The `zaima` script runs four checks sequentially:
1. **codex** - login state from `codex login status`, version from `codex --version`
2. **claude-code** - login state from `claude auth status --json`, version from `claude --version`
3. **gemini** - login state from `~/.gemini/` auth configuration, version from `gemini --version`
4. **hermes-agent** - login state from `hermes auth list`, version from `hermes version`

When stdout is a TTY, `zaima` renders a single-line spinner for the active check and clears it before printing the final result line.
