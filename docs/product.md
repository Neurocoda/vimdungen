# Product Overview

## Vision

`vimdungeon` is a CLI/TUI Vim training game that uses a real Neovim instance as its editing core. The product goal is to help players internalize Vim as an editing language made of motions, operators, text objects, and composition patterns rather than as a disconnected list of shortcuts.

## Intended Users

Primary users:

- Developers who want to learn Vim editing fluency without switching their entire daily workflow at once
- Current Vim beginners who know a few commands but cannot yet combine them confidently
- Intermittent Vim users who want deliberate practice instead of passive repetition

Secondary users:

- Experienced Vim users who want optimization-oriented challenges
- Content authors who want to add structured practice sets later

## Learning Promise

The game should help the player move from:

1. Recognizing individual motions
2. Executing simple edits with confidence
3. Combining motions, operators, and text objects
4. Applying those combinations to realistic code-shaped editing tasks
5. Optimizing for fewer steps and cleaner command composition

## Learning Path

The content model is chapter-based. The exact chapter list is still `TBD`, but the expected progression is:

1. Foundational movement and mode awareness
2. Basic operators and repeatable edit patterns
3. Text objects and composition
4. Small code-oriented editing puzzles
5. Efficiency-focused challenges on realistic snippets

The map and skill system should reinforce this path by showing what the player has learned and what a future level expects.

## Level Types

### `lesson`

- Focuses on a single new concept or a very small concept cluster
- May include teaching text inside the level description
- Uses a hard step limit
- Should minimize ambiguity about the intended technique

### `puzzle`

- Requires recombining already introduced skills
- Still uses a hard step limit
- Should reward reasoning about Vim grammar rather than trial and error

### `challenge`

- Targets optimization and fluency rather than binary pass or fail
- Uses scoring instead of hard failure
- May use more realistic snippets and broader solution space

## Design Principles

- Authenticity over simulation: use real Neovim behavior whenever possible.
- Fluency over memorization: train editing language, not isolated commands.
- Small deterministic tasks: early content should have clear goals and automatic judging.
- Visible progression: the map and skill graph should tell the player what has been learned and what is next.
- Authorable content: skills, levels, and world structure should be data-driven.
- Local-first state: progress should be stored locally and remain easy to inspect.
- Engineering clarity: future contributors should be able to reason about content and runtime boundaries without reverse engineering hidden rules.

## Product Boundaries

The first release intentionally excludes:

- Multi-window training
- Multi-buffer workflows
- User configuration loading
- Narrative-heavy story systems
- A standalone hint system

These constraints keep the first version focused on core editing fluency.
