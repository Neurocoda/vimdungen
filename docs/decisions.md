# Decision Log

This file is a lightweight ADR-style log for decisions that are already considered accepted at the current stage.

| ID | Decision | Status | Rationale | Consequence |
| --- | --- | --- | --- | --- |
| DEC-001 | Use real Neovim as the editing engine | Accepted | Authentic Vim behavior is the core product value | Runtime architecture must supervise an external editor process |
| DEC-002 | Launch Neovim in a clean isolated configuration | Accepted | User config would make content and scoring inconsistent | The game must bundle its own minimal editor-side setup |
| DEC-003 | Limit v1 gameplay to a single buffer | Accepted | Core editing fluency is the first teaching target | No multi-window, multi-tab, or multi-buffer training in v1 |
| DEC-004 | Save and quit commands must not alter game flow | Accepted | Level sessions should be deterministic and game-owned | The runtime needs command guards and lifecycle control |
| DEC-005 | Support three level modes: `lesson`, `puzzle`, `challenge` | Accepted | The product needs both teaching and optimization-oriented content | Schema and UI must model different completion and scoring expectations |
| DEC-006 | Support two judge types: `cursor` and `text` | Accepted | Early content needs deterministic movement and editing evaluation | Level goals stay simple and auto-judgeable |
| DEC-007 | Use effective step accounting with undo and redo adjustments | Accepted | Raw total key count does not reflect current effective edits | Step tracking must understand change blocks and undo history |
| DEC-008 | Use a static selectable world map in the first release | Accepted | A static map is enough to communicate progression without avatar systems | World data needs graph nodes, edges, and authored positions |
| DEC-009 | Model skills as first-class data entities | Accepted | Skills drive teaching, unlocks, and progress display | Levels and worlds must reference skill IDs rather than hard-coded text only |
| DEC-010 | Do not ship a separate hint system in v1 | Accepted | Early scope should stay focused on level design and progression | Basic lessons may include teaching text directly in descriptions |
| DEC-011 | Use split licensing for software and repository content | Accepted | The project is intended to be source-visible for personal learning and non-commercial evaluation, while restricting commercial use and protecting the value of authored levels, curriculum, and game-design materials separately from code | Software is licensed under PolyForm Noncommercial in [LICENSE](../LICENSE), while non-code content is governed separately by [LICENSE-CONTENT](../LICENSE-CONTENT); contributors must be aware that code and content are treated differently by purpose |
