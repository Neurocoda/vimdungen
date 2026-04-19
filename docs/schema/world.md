# World Schema

## Purpose

A world file defines the selectable campaign map, including chapters, nodes, edges, and unlock conditions.

## Top-Level Shape

```yaml
schema_version: 1
kind: world
id: main-campaign
title: Main Campaign
description: Introductory Vim fluency path.
starting_node: chapter-01-hub
chapters:
  - id: chapter-01
    title: Foundations
    order: 1
    description: Movement and first edits.
nodes:
  - id: chapter-01-hub
    chapter: chapter-01
    type: hub
    label: Foundations
    position:
      x: 10
      y: 15
    unlock:
      requires_all:
        levels_completed: []
        skills_mastered: []
edges:
  - from: chapter-01-hub
    to: lesson-h-left-node
```

## Fields

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `schema_version` | integer | Yes | Schema version for future migrations |
| `kind` | string | Yes | Must be `world` |
| `id` | string | Yes | Stable world identifier |
| `title` | string | Yes | Human-readable world title |
| `description` | string | Yes | Short summary of the campaign |
| `starting_node` | string | Yes | Node ID selected when the player first enters the map |
| `chapters` | list of chapter objects | Yes | Chapter definitions used for grouping and ordering |
| `nodes` | list of node objects | Yes | Authored map nodes |
| `edges` | list of edge objects | Yes | Authored graph connections |

## Chapter Object

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `id` | string | Yes | Stable chapter identifier |
| `title` | string | Yes | Human-readable chapter title |
| `order` | integer | Yes | Chapter ordering key |
| `description` | string | Yes | Short curriculum summary |

## Node Object

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `id` | string | Yes | Stable node identifier |
| `chapter` | string | Yes | Chapter ID that owns the node |
| `type` | string | Yes | `hub` or `level` |
| `label` | string | Yes | Map label |
| `position` | object | Yes | Authored `x` and `y` coordinates |
| `level_id` | string | Conditionally | Required when `type` is `level` |
| `unlock` | object | Yes | Declarative unlock condition |

### Position Object

```yaml
position:
  x: 28
  y: 18
```

Coordinates are authored in normalized map space. The future UI layer converts them into display coordinates.

## Edge Object

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `from` | string | Yes | Source node ID |
| `to` | string | Yes | Target node ID |

The first version assumes directed progression edges. If bidirectional rendering or styling is needed later, the schema can expand.

## Unlock Object

```yaml
unlock:
  requires_all:
    levels_completed:
      - lesson-h-left
    skills_mastered:
      - move-left
  requires_any:
    levels_completed: []
    skills_mastered: []
```

Rules:

- `requires_all` means every listed condition must be satisfied
- `requires_any` means at least one listed condition must be satisfied
- Empty lists mean no requirements in that category
- A node can omit `requires_any` if it is not needed

## Example

```yaml
schema_version: 1
kind: world
id: main-campaign
title: Main Campaign
description: Introductory Vim fluency path.
starting_node: chapter-01-hub
chapters:
  - id: chapter-01
    title: Foundations
    order: 1
    description: Movement and first edits.
nodes:
  - id: chapter-01-hub
    chapter: chapter-01
    type: hub
    label: Foundations
    position:
      x: 10
      y: 15
    unlock:
      requires_all:
        levels_completed: []
        skills_mastered: []
  - id: lesson-h-left-node
    chapter: chapter-01
    type: level
    label: "h: move left"
    level_id: lesson-h-left
    position:
      x: 28
      y: 18
    unlock:
      requires_all:
        levels_completed: []
        skills_mastered: []
edges:
  - from: chapter-01-hub
    to: lesson-h-left-node
```
