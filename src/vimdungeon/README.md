# Planned Python Package Layout

This package is intentionally a placeholder in Phase 1. The directory tree exists to make later implementation phases predictable.

Planned subpackages:

- `app`: CLI entry points and session bootstrap
- `content`: YAML loading, normalization, and validation
- `judge`: cursor and text judge logic plus step accounting
- `nvim`: isolated Neovim process control and bridge integration
- `persistence`: save-file loading and writing
- `progression`: world unlocks, skill mastery, and campaign traversal
- `ui`: map screens, menus, and result views

No gameplay logic is implemented yet.
