# vimdungeon

Train Vim like a language, not a list of shortcuts.

`vimdungeon` is a CLI/TUI Vim training game built around a real Neovim instance. It teaches editing fluency through structured levels, map-based progression, and skill-driven unlocks instead of a flat checklist of shortcuts.

## Status

The repository is currently in Phase 1: project structure design and documentation initialization.

What exists today:

- Project structure and placeholder package layout
- Product, gameplay, architecture, progression, and decision documents
- Schema documentation for skills, levels, worlds, and progress saves
- Minimal sample data files that validate the planned schemas

What does not exist yet:

- Gameplay runtime
- Neovim process integration
- Lua bridge code
- Content loaders or validators
- TUI screens

## Product Goals

- Use real Neovim behavior as the editing engine rather than a simulator.
- Teach motions, operators, text objects, and composition as an editing language.
- Organize practice into lesson, puzzle, and challenge levels.
- Drive content through YAML-authored skills, levels, and world maps.
- Keep progression local-first with a single-player save file.

## Non-Goals

- Simulating Vim in custom input logic
- Training multi-window, multi-tab, or multi-buffer workflows in v1
- Loading the player's personal `vimrc` or `init.lua`
- Allowing save or quit commands to break or bypass the game loop
- Shipping a separate hint system in the first release

## High-Level Architecture

The planned runtime has three main layers:

- Python host application: owns the CLI/TUI flow, content loading, progression, judging, and save management
- Isolated Neovim instance: provides authentic modal editing and text manipulation
- Thin Lua bridge inside Neovim: captures state, applies command restrictions, and exposes editor-side hooks

Authoring data lives beside the codebase in YAML files:

- Skills describe what the player learns
- Levels describe starting state, goals, and rewards
- Worlds describe map layout and unlock graph
- Progress saves describe the local player state

See [architecture.md](docs/architecture.md) for the detailed design.

## Project Structure

```text
.
├── CONTRIBUTING.md
├── README.md
├── data/
│   ├── levels/
│   ├── saves/
│   ├── skills/
│   └── worlds/
├── docs/
│   ├── architecture.md
│   ├── conventions.md
│   ├── decisions.md
│   ├── gameplay.md
│   ├── product.md
│   ├── waterfall-plan.md
│   ├── world-and-progression.md
│   └── schema/
├── lua/
│   └── vimdungeon/
├── prototypes/
├── scripts/
├── src/
│   └── vimdungeon/
└── tests/
```

Main directory purposes:

- `docs/`: design documents, architecture notes, and schema references
- `data/`: authored content and save examples
- `src/`: planned Python application package layout
- `lua/`: planned editor-side Lua integration points
- `tests/`: future unit, integration, and schema validation coverage
- `scripts/`: future developer tooling such as validation and packaging helpers
- `prototypes/`: scratch space for experiments that should not be treated as production content

## Documentation Map

- [product.md](docs/product.md): product intent, audience, learning path, and design principles
- [gameplay.md](docs/gameplay.md): level loop, judging, retry behavior, and step accounting
- [architecture.md](docs/architecture.md): planned Python, Neovim, and Lua collaboration model
- [world-and-progression.md](docs/world-and-progression.md): world graph, unlocks, and progress panel intent
- [waterfall-plan.md](docs/waterfall-plan.md): phase plan for waterfall delivery
- [decisions.md](docs/decisions.md): accepted project decisions
- [schema/](docs/schema): content schema references and examples

## Planned Development Phases

1. Documentation and structure design
2. Schema loaders and validation tooling
3. Isolated Neovim bootstrap and input capture
4. Core gameplay loop and judge engine
5. World map, progression, and saves
6. Content authoring, balancing, and UX polish
7. Packaging, QA, and release hardening

The detailed phase breakdown lives in [waterfall-plan.md](docs/waterfall-plan.md).

## Licensing

`vimdungeon` is source-available under a split, non-commercial licensing model.

- Software code and software-related files are covered by [LICENSE](LICENSE), which contains the PolyForm Noncommercial License 1.0.0.
- Game content and educational or game-design content are covered by [LICENSE-CONTENT](LICENSE-CONTENT).
- Scope guidance and third-party notices are summarized in [NOTICE](NOTICE).

Commercial use of the repository, its software, or its game content is not allowed without separate permission from the author.
