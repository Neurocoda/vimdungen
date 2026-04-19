# Level Schema

## Purpose

A level defines a single playable training unit. It contains the starting editor state, success criteria, teaching intent, and progression rewards.

## Top-Level Shape

```yaml
schema_version: 1
kind: level
id: lesson-h-left
title: Step Left with h
mode: lesson
judge: cursor
description: Move the cursor one character left.
chapter: chapter-01
difficulty: 1
skills_focus:
  - move-left
skills_used:
  - move-left
initial_buffer:
  - alpha
initial_cursor:
  line: 1
  column: 3
goal:
  target_cursor:
    line: 1
    column: 2
step_limit: 1
completion: You moved left with h.
insight: Small motions are the alphabet of larger edits.
rewards:
  grant_skills:
    - move-left
  unlock_levels:
    - lesson-ciw-replace-word
```

## Fields

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `schema_version` | integer | Yes | Schema version for future migrations |
| `kind` | string | Yes | Must be `level` |
| `id` | string | Yes | Stable level identifier |
| `title` | string | Yes | Human-readable level title |
| `mode` | string | Yes | `lesson`, `puzzle`, or `challenge` |
| `judge` | string | Yes | `cursor` or `text` |
| `description` | string | Yes | Briefing or built-in teaching text |
| `chapter` | string | Yes | Curriculum grouping |
| `difficulty` | integer | Yes | Relative difficulty, typically `1` to `5` |
| `skills_focus` | list of strings | Yes | Skills this level is designed to teach or emphasize |
| `skills_used` | list of strings | Yes | Skills expected to appear in successful solutions |
| `initial_buffer` | list of strings | Yes | Starting buffer lines |
| `initial_cursor` | object | Yes | Starting cursor position using 1-based line and column |
| `goal` | object | Yes | Judge-specific target definition |
| `step_limit` | integer | Conditionally | Required for `lesson` and `puzzle`; usually omitted for `challenge` |
| `scoring` | object | Conditionally | Recommended for `challenge`; optional otherwise |
| `completion` | string | Yes | Short success message shown after clear |
| `insight` | string | Yes | Teaching takeaway or optimization note |
| `rewards` | object | Yes | Progression grants such as skills or explicit unlocks |

## Goal Object

### For `judge: cursor`

```yaml
goal:
  target_cursor:
    line: 1
    column: 2
```

### For `judge: text`

```yaml
goal:
  target_buffer:
    - name = new
```

## Scoring Object

The first release only needs simple challenge scoring. A challenge level may include:

```yaml
scoring:
  metric: steps
  ranks:
    gold: 8
    silver: 10
    bronze: 14
```

Interpretation:

- Lower values are better
- A completed challenge is ranked by the best threshold met
- Exact presentation is `TBD`

## Rewards Object

```yaml
rewards:
  grant_skills:
    - change-inner-word
  unlock_levels:
    - puzzle-rename-variable
```

Rules:

- `grant_skills` adds mastered skills to progress on completion
- `unlock_levels` can directly unlock additional level IDs
- Empty lists are allowed when a level should not grant anything new

## Example

```yaml
schema_version: 1
kind: level
id: lesson-ciw-replace-word
title: Replace a Word with ciw
mode: lesson
judge: text
description: Replace the current word with new.
chapter: chapter-01
difficulty: 2
skills_focus:
  - change-inner-word
skills_used:
  - change-inner-word
initial_buffer:
  - name = old
initial_cursor:
  line: 1
  column: 8
goal:
  target_buffer:
    - name = new
step_limit: 7
completion: You replaced a word with ciw.
insight: Operators and text objects become powerful when treated as a phrase.
rewards:
  grant_skills:
    - change-inner-word
  unlock_levels: []
```
