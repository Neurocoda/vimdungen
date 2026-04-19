# World and Progression Design

## World Model

The main menu is planned as a static, selectable world map rather than a character-walking overworld. The world is modeled as a graph of nodes and edges.

Why a graph:

- It supports chapter structure without forcing a linear list
- It expresses branching unlocks naturally
- It aligns well with both skill prerequisites and level prerequisites

## Core Concepts

### Chapters

Chapters are logical content groups. A chapter may represent a learning theme such as movement, operators, or code-editing composition.

Expected chapter responsibilities:

- Provide ordering in the broader curriculum
- Group nodes for map rendering and progress reporting
- Give content authors a stable structure for expansion

### Nodes

A world node is a selectable map element.

Planned node types:

- `hub`: a chapter anchor or non-playable connector
- `level`: a playable node that maps to a level definition

Each node should carry:

- A stable `id`
- A `chapter`
- A display `label`
- A `position`
- Optional `level_id`
- Unlock conditions

### Edges

Edges connect nodes on the map. In the initial static selection design, they primarily describe adjacency and progression readability, not free movement simulation.

## Node Positioning

The first map is static. Node positions should therefore be authored data rather than computed layout.

Recommended model:

- `x` and `y` coordinates in a normalized map space
- A renderer later converts them into terminal or TUI coordinates

This keeps the authored world independent from any one UI implementation.

## Unlock Model

The system needs to support both:

- Unlocks based on completed levels
- Unlocks based on mastered skills

The world schema therefore allows unlock conditions to reference either or both.

Planned unlock evaluation:

1. Start with baseline nodes that have no requirements.
2. Read the player's completed levels and mastered skills from the save file.
3. Evaluate node unlock conditions.
4. Merge in any direct unlock rewards recorded in progress.

The exact precedence between graph-based unlocks and direct reward unlocks is still `TBD`, but both are first-class concepts in the data model.

## Skill Tree and Level Graph Relationship

Skills are not embedded only inside levels. They are separate modeled entities because they serve multiple purposes:

- They describe the learning curriculum
- They drive unlock conditions
- They support a visible skill tree or progress summary
- They provide a reusable abstraction across many levels

Levels may:

- Focus on one or more skills
- Use previously learned skills
- Grant skills when completed

The world graph answers "where can I go next?" while the skill graph answers "what have I learned and what is still missing?"

## Progress Panel Intent

The map UI is planned to include a top-right progress area.

Its purpose is to give quick context without opening a separate menu:

- Current chapter or selected node context
- Completed level count
- Mastered skill count
- Possibly the selected node's relevant skills
- Possibly best-step or challenge-rank summaries

The panel should reinforce long-term learning structure, not overwhelm the player with analytics.

## Retry and Progression

A completed level remains replayable. This matters for two reasons:

- Players should be able to optimize routes and step counts
- Challenge-style mastery depends on repeatability

Progression should therefore distinguish:

- Whether a level has been cleared
- Whether it is currently unlocked
- What the player's best performance was

## Initial Scope Constraints

For v1:

- The map is static and selection-based
- No avatar movement is required
- No dynamic node generation is required
- Unlock rules should stay declarative and data-driven

Anything more dynamic is intentionally postponed until the core learning loop is stable.
