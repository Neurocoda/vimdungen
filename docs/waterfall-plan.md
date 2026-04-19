# Waterfall Development Plan

## Delivery Approach

The project is intentionally organized as a waterfall-style build. Each phase should leave behind stable artifacts before the next phase begins.

This is a planning document, not a record of completed implementation.

## Current Phase

The repository is currently in:

- Phase 1: project structure design and documentation initialization

## Phase Breakdown

| Phase | Focus | Main Deliverables | Exit Criteria |
| --- | --- | --- | --- |
| 1 | Structure and documentation | Repository layout, design docs, schema docs, sample data | Future contributors can understand the product and data model without reading code |
| 2 | Schema and content tooling | Data loaders, validators, content linting, schema tests | Skills, levels, worlds, and saves can be parsed and validated deterministically |
| 3 | Neovim runtime bootstrap | Isolated Neovim launch, minimal Lua bridge, session lifecycle scaffolding | A level buffer can be opened in a clean controlled Neovim instance |
| 4 | Core gameplay loop | Judge engine, step accounting, level start and finish flow, retry support | Lesson and puzzle levels can run end to end with automatic pass or fail |
| 5 | World and progression | Map UI, unlock logic, save persistence, progress panel | Players can unlock, select, replay, and persist progression across sessions |
| 6 | Content expansion and balancing | Early chapter content, challenge scoring tuning, author workflow improvements | The game has a coherent playable learning path |
| 7 | Hardening and release prep | Packaging, QA, regression tests, docs refresh | The project is stable enough for external testing or release |

## Recommended Order of Work

1. Freeze schema shape before writing runtime logic.
2. Build validation tooling before large content authoring begins.
3. Prove isolated Neovim control before designing richer UI behavior.
4. Ship the lesson and puzzle loop before challenge scoring polish.
5. Add world-map persistence after individual level sessions are reliable.
6. Scale content only after authoring and validation workflows are practical.

## Phase 1 Scope

Phase 1 should produce:

- A clear directory tree
- A documented architecture target
- A stable first-pass schema for skills, levels, worlds, and progress
- Minimal example content
- Contribution and naming conventions

Phase 1 should not produce:

- Runtime integration code
- TUI rendering code
- Content loader implementation
- Judge implementation

## Phase Handoffs

Each later phase should start by reviewing:

- [decisions.md](decisions.md)
- [conventions.md](conventions.md)
- [schema/](schema/)

If a later phase requires breaking a Phase 1 contract, the change should be recorded explicitly before implementation proceeds.
