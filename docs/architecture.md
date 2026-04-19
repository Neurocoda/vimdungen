# Architecture Overview

## Summary

`vimdungeon` is planned as a Python-hosted CLI/TUI application that launches and supervises an isolated Neovim process. A small amount of Lua code will run inside that Neovim instance to expose editor-side state and hooks back to the Python host.

This document describes the target architecture. It does not describe implemented code.

## Why Real Neovim

The project deliberately uses real Neovim instead of a custom Vim simulator because:

- Vim fluency depends on authentic modal behavior
- Undo blocks, text objects, operators, and edge cases are difficult to simulate faithfully
- Real editing behavior provides better transfer from training to daily use
- The game can stay focused on pedagogy and orchestration instead of recreating an editor

## Planned Runtime Layers

### Python Host

Expected responsibilities:

- CLI/TUI shell
- Session and level lifecycle orchestration
- YAML content loading
- World progression and unlock evaluation
- Step accounting orchestration
- Automatic judging
- Local save management

### Isolated Neovim Process

Expected responsibilities:

- Real modal editing
- Cursor motion
- Buffer mutation
- Undo and redo semantics
- Editor state that the game reads and reacts to

### Lua Bridge

Expected responsibilities:

- Minimal editor-side hooks
- State reporting helpers
- Command restrictions for game safety
- Optional autocmd-based notifications

The Lua layer should remain thin. Game rules belong in Python unless an editor-local hook is strictly required.

## Isolation Strategy

The game should launch a clean Neovim instance that does not read the player's own configuration.

Rationale:

- User mappings would make levels inconsistent
- User plugins could change buffer behavior or UI state
- Reproducibility matters for both scoring and content authoring

Planned isolation properties:

- No user `vimrc` or `init.lua`
- No persistent swap or session carry-over
- Only bundled game-side configuration and Lua hooks

The exact startup command and runtimepath strategy are still `TBD`.

## Single Buffer Decision

The first version is intentionally limited to a single buffer.

Why:

- It matches the learning objective of core editing fluency
- It reduces judge complexity
- It keeps authored content deterministic
- It avoids early scope growth into project navigation or window management

Consequences:

- No multi-buffer puzzles in v1
- No split, tab, or window-management training in v1
- World progression must come from level sequencing, not from in-editor file navigation

## Planned Component Boundaries

The current source tree reserves space for these Python subsystems:

- `app`: CLI entry points and session bootstrap
- `content`: YAML loading and validation
- `judge`: cursor and text judging plus step accounting
- `nvim`: process bootstrap and RPC or bridge integration
- `persistence`: local save I/O
- `progression`: unlock graph and skill mastery logic
- `ui`: map, menus, and result screens

Lua code under `lua/vimdungeon/` is expected to mirror only the editor-side integration concerns.

## Expected Runtime Flow

1. Python loads world, level, and skill data from YAML.
2. Python resolves the selected level and player progress.
3. Python launches an isolated Neovim session.
4. Python injects the level buffer and cursor state.
5. Lua hooks expose editor state or events as needed.
6. Python evaluates steps and judge rules.
7. Python closes the level session and shows the result screen.
8. Python updates local progress and world unlocks.

## Command Safety

The game flow should not be disrupted by save or quit commands. Planned restrictions include blocking or remapping commands such as:

- `:w`
- `:q`
- `:qa`
- `ZZ`
- `ZQ`

The exact enforcement point is `TBD`, but the preferred design is a combination of editor-side guarding and host-side session ownership.
