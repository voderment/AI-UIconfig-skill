# AI-UIconfig-skill

<img width="1338" height="840" alt="CliperX Image 2026-04-21 13 16 45" src="https://github.com/user-attachments/assets/bd975a1c-1f14-491d-a297-0247d031314d" />

`AI-UIconfig-skill` is a reusable agent skill for making UI refinement more precise, more efficient, and more repeatable during app development.

It is especially well suited to SwiftUI projects, where teams often need a better way to separate visual structure from runtime logic, preview screens in isolation, and fine-tune UI details without getting stuck in slow edit-build-run loops.

Instead of treating UI tuning as scattered one-off edits, this skill helps turn it into a controlled workflow. The result is a codebase that is easier to iterate on, easier to inspect, and safer to adjust when visual polish matters.

It is designed for projects where:

- UI code is mixed with runtime logic
- styles are hardcoded across many files
- Xcode Canvas previews are hard to use
- visual tuning requires too much edit-build-run repetition
- teams want a debug-only runtime editor plus precise writeback

## What It Does

This skill helps an agent reshape a SwiftUI codebase into a UI workflow that supports careful, fine-grained adjustment. In practice, that usually means:

- `Render State` boundaries between runtime logic and pure UI
- governed style tokens / metrics
- preview mocks and preview galleries
- a `DEBUG`-only live tuning editor
- saved tuning snapshots that can be reloaded explicitly
- per-token reset and whole-session revert behavior
- narrow source writeback for approved leaf constants
- writeback that preserves valid source literal syntax instead of risking file corruption
- value-span writeback that preserves each declaration's existing structure and comments
- a single source-defined startup baseline so writeback changes survive rebuilds instead of diverging from a duplicate token default table

This is useful when you want to tune spacing, sizing, opacity, corner radius, semantic colors, or other stable visual parameters with more control than ad hoc source edits provide.

## Default Principle

The default mode is `preserve mode`.

That means:

- existing UI should not be intentionally redesigned
- existing interaction behavior should not be intentionally changed
- the first goal is governance and debuggability, not visual reinvention

The main goal is not to redesign the product. The main goal is to make UI work easier to refine and maintain.

The skill can also work in `extend mode` when new UI already exists and needs to be folded into the same system.

## Why It Fits SwiftUI

SwiftUI is a particularly strong fit for this skill because SwiftUI projects benefit from clean render boundaries, preview-safe view inputs, and reusable style tokens.

When a SwiftUI codebase grows, visual values often become distributed across many views and modifiers. That makes precise UI tuning harder than it needs to be. This skill brings those values into a more governed structure, so visual adjustments become faster, clearer, and less error-prone.

It is most valuable when you want to keep the existing product intent, but gain a better way to inspect, preview, tune, and selectively write changes back into source.

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
- designers or developers need faster and more precise visual iteration
- the project benefits from Canvas previews and isolated mock states
- the team wants a safer way to fine-tune UI without broad refactors

This skill is not the right primary tool when:

- the user wants a brand new visual design language
- the codebase only needs a tiny one-off style tweak
- the main problem is unrelated runtime logic or persistence

## Repository Contents

- [SKILL.md](./SKILL.md)
  The actual skill definition for Codex-style agents.
- [examples/PROMPTS.md](./examples/PROMPTS.md)
  Prompt examples for common usage patterns.
- [LICENSE](./LICENSE)
  The repository is released under the MIT License.

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

More importantly, it should give the team a practical way to make precise UI adjustments during development without turning every visual tweak into a manual search-and-edit exercise.

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
- the published license still matches how you want others to reuse the repository

## Maintenance Rule

This repository is expected to track behavior that has been validated in real projects.

When the governed workflow changes in a project using this skill, the maintainer should explicitly check whether the skill contract changed too.

Changes that usually require that check include:

- render-state boundary changes
- preview coverage changes
- token scope changes
- runtime editor behavior changes
- save/load snapshot behavior changes
- single-item or whole-session revert behavior changes
- writeback targeting/path-resolution changes
- localization rules for the tuning tool
- source-baseline vs saved-snapshot session behavior changes

If the reusable contract changed, update `SKILL.md` and sync the public repository in the same maintenance pass.

## License

This repository is released under the MIT License.

That means other developers can use, modify, and distribute the skill with minimal restrictions, as long as the copyright notice and license text are preserved.
