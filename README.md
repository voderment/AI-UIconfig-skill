# AI-UIconfig-skill

`AI-UIconfig-skill` is a reusable agent skill for turning an existing SwiftUI project into a governed UI system that is easier to debug, easier to preview, and safer to tune at runtime without changing the product's visual intent by default.

It is designed for projects where:

- UI code is mixed with runtime logic
- styles are hardcoded across many files
- Xcode Canvas previews are hard to use
- visual tuning requires too much edit-build-run repetition
- teams want a debug-only runtime editor plus precise writeback

## What It Does

This skill helps an agent transform a SwiftUI codebase into a structure with:

- `Render State` boundaries between runtime logic and pure UI
- governed style tokens / metrics
- preview mocks and preview galleries
- a `DEBUG`-only live tuning editor
- saved tuning snapshots that can be reloaded explicitly
- per-token reset and whole-session revert behavior
- narrow source writeback for approved leaf constants

## Default Principle

The default mode is `preserve mode`.

That means:

- existing UI should not be intentionally redesigned
- existing interaction behavior should not be intentionally changed
- the first goal is governance and debuggability, not visual reinvention

The skill can also work in `extend mode` when new UI already exists and needs to be folded into the same system.

## Core Workflow

The expected workflow is:

1. Inventory the important UI surfaces and states.
2. Split runtime/composer code from pure UI code.
3. Introduce render-state inputs for preview-safe UI.
4. Tokenize stable styling values.
5. Build preview mocks and gallery states.
6. Add a debug-only live tuning editor.
7. Save snapshots and support explicit reload of saved configs.
8. Add precise writeback for approved source constants.
9. Validate build, previews, and manual runtime behavior.

## Key Rules

- Preserve existing product intent by default.
- Do not expose every constant as a runtime control.
- Localize explanatory text and tool chrome, not code-facing token keys by default.
- Relaunch should return to the source-defined baseline unless the user explicitly wants auto-restore.
- Saved configs should be explicit snapshots the user chooses to reload.
- Writeback should be explicit, narrow, and non-destructive.

## Best Fit

This skill is a strong fit when:

- the app is SwiftUI-based
- the same UI surfaces are revisited often
- layout and style values are repeated
- designers or developers need faster visual iteration
- the project benefits from Canvas previews and isolated mock states

This skill is not the right primary tool when:

- the user wants a brand new visual design language
- the codebase only needs a tiny one-off style tweak
- the main problem is unrelated runtime logic or persistence

## Repository Contents

- [SKILL.md](./SKILL.md)
  The actual skill definition for Codex-style agents.
- [examples/PROMPTS.md](./examples/PROMPTS.md)
  Prompt examples for common usage patterns.

## How To Use

### 1. Install As A Local Skill

Copy or symlink this repository so the agent can see it as a local skill.

Example:

```bash
mkdir -p ~/.agents/skills
ln -s "/absolute/path/to/AI-UIconfig-skill" ~/.agents/skills/AI-UIconfig-skill
```

If you already keep skills in another local skill directory, place this repo there instead.

### 2. Invoke It In A Prompt

Use direct prompts such as:

- `Use AI-UIconfig-skill to refactor this SwiftUI surface into render-state and previewable UI.`
- `Use AI-UIconfig-skill in preserve mode. Do not change the visual design.`
- `Use AI-UIconfig-skill to add a DEBUG-only token editor with saved configs and writeback.`
- `Use AI-UIconfig-skill to fold this new module into the existing token/preview/writeback system.`

### 3. Choose A Mode

- `preserve mode`
  Use for existing UI you do not want visually changed.
- `extend mode`
  Use when new UI already exists and should be absorbed into the governed system.

## Expected Outputs

When the skill is applied well, the resulting project should usually have:

- a clearer `UI/` structure
- pure UI views that can be previewed without real runtime dependencies
- render-state mock coverage for major states
- a debug-only editor for stable governed values
- external saved snapshots
- explicit writeback mappings to source constants

## Notes On Localization

For runtime tuning tools, this repository assumes:

- token keys stay code-facing and stable
- parameter titles may remain aligned to source semantics
- explanatory descriptions and tool chrome should follow the current UI language

This keeps the tool understandable without polluting the code-facing layer.

## Suggested Release Checklist

Before publishing this skill for broad use, verify:

- `SKILL.md` matches the behavior you actually validated in a real project
- prompt examples still reflect the current workflow
- repository instructions match your preferred local skill installation path
- you have chosen and added an open-source license

## License

Choose and add your preferred open-source license before public release.
