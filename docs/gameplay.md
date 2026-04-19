# Gameplay Design

## Core Loop

The planned core loop is:

1. Select a level from the world map
2. Read the briefing and any built-in teaching text
3. Enter an isolated Neovim session with a prepared buffer
4. Perform edits or movement under the level's rules
5. Trigger automatic completion once the judge conditions are met
6. View the result screen
7. Choose `Retry`, `Next`, or potentially `Back to Map`

Even after a successful clear, the player should be able to replay a level to improve efficiency.

## Level Start

Each level provides:

- A title
- A mode: `lesson`, `puzzle`, or `challenge`
- A judge type: `cursor` or `text`
- A description that can include teaching guidance for basic lessons
- An initial buffer
- An initial cursor position
- A success goal
- Either a hard `step_limit` or a challenge scoring profile

The runtime should prepare a clean, isolated Neovim buffer from this data. No user config should leak into the session.

## Active Play

During active play, the system is expected to:

- Capture key inputs
- Track effective step usage
- Read current buffer and cursor state
- Prevent save or quit commands from breaking the game flow
- Evaluate whether the level goal has been reached

This behavior is planned only. The implementation does not exist yet.

## Judge Types

### `cursor`

Used for movement-focused levels. Success is defined by the final cursor position.

Expected goal shape:

- Target line
- Target column

### `text`

Used for editing and challenge levels. Success is defined by the final buffer contents.

Expected goal shape:

- Target buffer lines

Future extensions such as partial matches or ignored whitespace are `TBD`. The current design assumes exact matching for clarity.

## Result Screen

After a level ends, the player should enter a unified result screen.

Expected actions:

- `Retry`: restart the same level with the same initial state
- `Next`: available after a successful clear and moves to the next unlocked level when applicable
- `Back to Map`: optional but recommended for the map-driven structure

The result screen is intended to normalize flow across all level types.

## Step Accounting

The project does not use a naive "total keys ever pressed" score. Instead, it uses an effective step model that reflects the currently active edit history.

### Baseline Rule

- Every key counts as 1 step by default.

### Special Rule for `u`

- `u` itself counts as 0 steps.
- When `u` undoes a valid edit change block, the steps consumed by that undone change block are removed from the current total.

### Special Rule for `<C-r>`

- `<C-r>` itself counts as 0 steps.
- When `<C-r>` redoes a previously undone edit change block, the steps consumed by that restored change block are added back to the current total.

### Change Block Model

Undo and redo operate on Neovim change blocks, not on individual keys. The design assumes:

- Insert mode from entering insert mode until pressing `<Esc>` is treated as one natural undo block
- Operator-based edits such as `dw` or `ciw` are treated according to the change blocks produced by real Neovim
- Keys that materially formed a change block belong to that block's step cost

This means the score tracks the net cost of the player's currently effective edits, not the peak cost of failed attempts that were fully undone.

### No-Op Undo and Redo

If `u` or `<C-r>` has no applicable change block:

- No steps are added
- No steps are removed

### Practical Examples

Example 1:

- Input: `h`
- Effective steps: `1`

Example 2:

- Input: `iabc<Esc>`
- Effective steps after insert: `5`
- Input then `u`
- Effective steps: `0`

Example 3:

- Input: `dwllu`
- `dw` contributes `2`
- `ll` contributes `2`
- `u` removes the `dw` change block cost and contributes `0`
- Effective steps: `2`

Example 4:

- Input: `ciwnew<Esc>`
- Effective steps after edit: `7`
- Input then `u`
- Effective steps: `0`
- Input then `<C-r>`
- Effective steps: `7`

## Failure and Success Rules by Level Type

### `lesson`

- Hard step limit
- Binary pass or fail
- Designed to reinforce a specific technique

### `puzzle`

- Hard step limit
- Binary pass or fail
- Designed to test combination of known skills

### `challenge`

- No hard failure on a single threshold by default
- Uses score bands or ranks
- Still uses automatic judging for completion of the text goal

The exact challenge scoring formula is part of the schema but its final balance remains `TBD`.
