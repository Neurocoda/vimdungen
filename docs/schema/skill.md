# Skill Schema

## Purpose

A skill describes a learnable Vim capability that can appear in teaching material, progression requirements, and progress summaries.

Skills are first-class data, not just text embedded in levels.

## Top-Level Shape

```yaml
schema_version: 1
kind: skill
id: move-left
name: Move Left with h
category: movement
track: core
description: Move one character left in Normal mode with h.
depends_on: []
chapter: chapter-01
order: 10
```

## Fields

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `schema_version` | integer | Yes | Schema version for future migrations |
| `kind` | string | Yes | Must be `skill` |
| `id` | string | Yes | Stable skill identifier |
| `name` | string | Yes | Human-readable skill name |
| `category` | string | Yes | Broad grouping such as `movement`, `editing`, `operator`, or `text-object` |
| `track` | string | Yes | Either `core` or `optional` |
| `description` | string | Yes | Brief description of the capability |
| `depends_on` | list of strings | Yes | Skill IDs that should be learned first |
| `chapter` | string | Yes | First chapter where the skill belongs or is introduced |
| `order` | integer | Yes | Sort key within the chapter or category |

## Notes

- `track` captures the "core versus optional" concept without needing two boolean fields.
- `depends_on` should reference other skill IDs, not level IDs.
- `chapter` is a curriculum hint, not a world-node reference.
- `order` should be stable so UI and content tools can sort predictably.

## Example

```yaml
schema_version: 1
kind: skill
id: change-inner-word
name: Change Inner Word
category: editing
track: core
description: Replace the current word contents with ciw.
depends_on: []
chapter: chapter-01
order: 30
```
