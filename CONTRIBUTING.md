# Contributing to vimdungeon

This repository is in a documentation-first setup phase. Treat the current branch as architecture and content-shape groundwork, not as a runtime implementation branch.

## Current Phase Expectations

- Prioritize documents, schema definitions, and sample data over executable features.
- Do not introduce gameplay logic unless the active phase explicitly changes.
- If a new design choice affects behavior, record it in [decisions.md](docs/decisions.md).
- If a new data field is added, update both the relevant schema document and at least one matching example file.

## Working in the Current Phase

- Keep documents in English.
- Prefer small, explicit changes over speculative large rewrites.
- Mark unresolved design questions as `TBD` instead of guessing implementation details.
- Preserve the distinction between planned behavior and implemented behavior.

## Licensing Awareness

- This repository uses a split, non-commercial licensing model described in [LICENSE](LICENSE), [LICENSE-CONTENT](LICENSE-CONTENT), and [NOTICE](NOTICE).
- Contributions may fall under different licensing scopes depending on file purpose. Software-oriented changes generally follow the software license, while game content and educational materials may fall under the content license.
- Contributions to code-oriented files are submitted under [LICENSE](LICENSE). Contributions to content-oriented files are submitted under [LICENSE-CONTENT](LICENSE-CONTENT).
- Contributors should understand that the repository is source-available and not available for commercial use by default.

## Modifying Documentation

When editing design documents:

- Keep product intent in [product.md](docs/product.md).
- Keep player-facing rules in [gameplay.md](docs/gameplay.md).
- Keep system structure and runtime boundaries in [architecture.md](docs/architecture.md).
- Keep world graph and unlock logic in [world-and-progression.md](docs/world-and-progression.md).
- Record accepted architectural decisions in [decisions.md](docs/decisions.md).

## Adding or Changing a Schema

For any schema change:

1. Update the corresponding file in `docs/schema/`.
2. Explain required fields, optional fields, and validation rules.
3. Add or update at least one example file under `data/`.
4. Check that all cross-referenced IDs still resolve cleanly.
5. Note any migration impact in [decisions.md](docs/decisions.md) or [waterfall-plan.md](docs/waterfall-plan.md) when relevant.

## Adding Example Data

Example data is for schema validation and authoring guidance.

- Keep examples intentionally small.
- Avoid placeholder IDs that do not exist elsewhere unless the schema explicitly allows forward references.
- Prefer realistic but minimal content over large mock campaigns.
- Keep example prose clear enough for both human contributors and AI agents.

## Adding Future Levels

When implementation phases begin, level authors should:

- Define or reference the required skills first.
- Keep a level's learning goal narrow and explicit.
- Choose the correct `mode` and `judge`.
- Define a concise starting buffer and a deterministic goal state.
- Keep rewards aligned with the intended progression graph.
- Update the world file when the level becomes selectable on the map.

## Review Checklist

Before merging documentation or content changes:

- File names follow [conventions.md](docs/conventions.md).
- Schema examples still match their documentation.
- New IDs are consistent, stable, and cross-referenced correctly.
- Design decisions are written as accepted facts only when they are actually settled.
