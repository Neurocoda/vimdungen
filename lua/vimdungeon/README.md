# Planned Lua Integration Area

This directory is reserved for the small amount of Lua code that will run inside the isolated Neovim instance.

Expected responsibilities:

- Register editor-side hooks or autocmds
- Expose lightweight state helpers to the Python host
- Guard save and quit behavior during a level session

The Lua layer should stay intentionally thin. Game rules belong in Python unless an editor-local hook is required.
