# Conventions

## Documentation Language

- All repository documentation is written in English.
- If a design detail is unresolved, mark it as `TBD`.
- Do not describe planned behavior as if it is already implemented.

## File Naming

- Markdown documents: lowercase kebab-case, for example `world-and-progression.md`
- YAML content files: lowercase kebab-case, for example `lesson-h-left.yaml`
- Python modules and packages: lowercase snake_case
- Lua module directories: lowercase names that match runtime module paths

## ID Design

All authored IDs should be stable and human-readable.

General rules:

- Use lowercase kebab-case
- Avoid spaces
- Avoid encoding version numbers into IDs
- Keep IDs unique within their entity namespace

Recommended patterns:

- Chapters: `chapter-01`, `chapter-02`
- Skills: `move-left`, `change-inner-word`
- Levels: `lesson-h-left`, `puzzle-delete-word`, `challenge-refactor-loop`
- World IDs: `main-campaign`
- World nodes: `<level-id>-node` or `<chapter-id>-hub`

## YAML Style

Recommended formatting:

- Two-space indentation
- Top-level keys ordered with `schema_version` and `kind` first
- One list item per line
- Prefer plain scalars unless quoting improves clarity
- Use block scalars only for genuinely multi-line prose

Authoring rules:

- Cross-reference existing IDs whenever possible
- Keep examples minimal and coherent
- Prefer explicit fields over overloaded shorthand
- Use lists of strings for buffer content to keep line structure unambiguous

## Cursor Coordinates

Schema documents use 1-based `line` and 1-based `column` values for authoring clarity.

If a runtime API uses a different indexing model later, the loader should convert values at the boundary instead of leaking API-specific indexing into content files.

## Chapter and Content Naming

Use chapter titles that express the learning theme rather than implementation detail.

Good examples:

- `Foundations`
- `Operators and Objects`
- `Code Editing Patterns`

Avoid:

- `Chapter 1 Stuff`
- `Misc`

## Skill Naming

Skill IDs should name the capability, not the lesson file.

Prefer:

- `move-left`
- `change-inner-word`
- `delete-to-end-of-line`

Avoid:

- `lesson-01`
- `h-key`

## Level Naming

Level IDs should encode both level type and intent.

Prefer:

- `lesson-h-left`
- `puzzle-swap-words`
- `challenge-trim-function-call`

## World Authoring

- Keep node coordinates stable once published
- Keep unlock logic declarative
- Do not duplicate the same progression rule in multiple places unless the redundancy is intentional and documented

## Save Authoring

Progress files are local runtime state, not authored campaign content. Even so, example saves should still follow the same naming and formatting discipline so they remain useful as fixtures and test data.
