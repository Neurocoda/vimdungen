# Progress Schema

## Purpose

A progress file stores the local player's world position, unlock state, mastered skills, and best performance data.

For Phase 1, the planned save format is YAML for readability and easy fixture authoring. A future runtime may still choose to export or cache JSON internally if needed.

## Top-Level Shape

```yaml
schema_version: 1
kind: progress
profile_id: default
world_id: main-campaign
current_node: lesson-ciw-replace-word-node
completed_levels:
  - lesson-h-left
unlocked_levels:
  - lesson-h-left
  - lesson-ciw-replace-word
mastered_skills:
  - move-left
best_steps:
  lesson-h-left: 1
challenge_scores: {}
last_played_level: lesson-h-left
updated_at: 2026-04-19T00:00:00Z
```

## Fields

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `schema_version` | integer | Yes | Schema version for future migrations |
| `kind` | string | Yes | Must be `progress` |
| `profile_id` | string | Yes | Local save slot identifier |
| `world_id` | string | Yes | Current world or campaign ID |
| `current_node` | string | Yes | Currently selected node on the map |
| `completed_levels` | list of strings | Yes | Cleared level IDs |
| `unlocked_levels` | list of strings | Yes | Available level IDs |
| `mastered_skills` | list of strings | Yes | Skills granted or marked mastered |
| `best_steps` | mapping | Yes | Best effective step count per level ID |
| `challenge_scores` | mapping | Yes | Per-level challenge score records |
| `last_played_level` | string | No | Most recently entered level ID |
| `updated_at` | string | Yes | Last save timestamp in ISO 8601 format |

## Challenge Score Record

Each `challenge_scores.<level_id>` entry may use this shape:

```yaml
challenge_scores:
  challenge-trim-function-call:
    rank: silver
    best_steps: 10
    updated_at: 2026-04-19T00:00:00Z
```

The exact scoring payload may evolve later, but it should remain level-keyed and easy to merge.

## Notes

- `completed_levels` and `unlocked_levels` are intentionally separate because a level can be unlocked before it is completed.
- `best_steps` applies to any level type that uses effective step counting.
- `challenge_scores` is separate so challenge-specific display and ranking can evolve without overloading `best_steps`.
- `current_node` supports returning the player to the same position on the map.

## Example

```yaml
schema_version: 1
kind: progress
profile_id: default
world_id: main-campaign
current_node: lesson-ciw-replace-word-node
completed_levels:
  - lesson-h-left
unlocked_levels:
  - lesson-h-left
  - lesson-ciw-replace-word
mastered_skills:
  - move-left
best_steps:
  lesson-h-left: 1
challenge_scores: {}
last_played_level: lesson-h-left
updated_at: 2026-04-19T00:00:00Z
```
