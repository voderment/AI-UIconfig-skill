<img width="1440" height="975" alt="Xnip2026-04-22_15-08-10" src="https://github.com/user-attachments/assets/dc3dbbc9-1ac7-40bc-89f8-dda444e82b71" />


English | [简体中文](./README.zh-CN.md)

# AI-UIconfig-skill

`AI-UIconfig-skill` is a reusable skill for turning an existing SwiftUI codebase into a more governable UI workflow with render-state boundaries, preview mocks, tokenized styling, and a `DEBUG`-only tuning + writeback tool.

It is meant for teams that want faster UI iteration without redesigning the product.

## Best Fit

Use this skill when:

- SwiftUI UI code is mixed with runtime logic
- style values are repeated or hardcoded across many files
- previews and mock states are hard to maintain
- visual tuning still depends on slow edit-build-run loops
- the team wants safer, narrower source writeback for approved UI constants

This is not the right primary tool when:

- the goal is a brand new visual design language
- the codebase only needs a tiny one-off UI tweak
- the main problem is unrelated runtime logic or persistence

## What You Get

When applied well, the project usually gains:

- clearer runtime/UI boundaries
- preview-safe render-state inputs
- governed tokens and metrics
- preview mocks and gallery coverage for key states
- a `DEBUG`-only live tuning editor generated from real governed surfaces and aligned, where practical, with the host project's existing design language
- saved tuning snapshots and explicit reload
- precise writeback for approved leaf constants

Default behavior is `preserve mode`: keep the existing product intent and improve control, not visual design. Use `extend mode` only when new UI should be absorbed into the same system.

## How To Use

### Install

Copy or symlink this repository into your local skills directory.

```bash
mkdir -p ~/.agents/skills
ln -s "/absolute/path/to/AI-UIconfig-skill" ~/.agents/skills/AI-UIconfig-skill
```

If you already use another local skills directory, place the repo there instead.

### Prompt It

Example prompts:

- `Use AI-UIconfig-skill to refactor this SwiftUI surface into render-state and previewable UI.`
- `Use AI-UIconfig-skill in preserve mode. Do not change the visual design.`
- `Use AI-UIconfig-skill to add a DEBUG-only token editor with saved configs and writeback.`
- `Use AI-UIconfig-skill to fold this new module into the existing token/preview/writeback system.`

## Repository Contents

- [SKILL.md](./SKILL.md)
  The actual skill definition and execution contract.
- [examples/PROMPTS.md](./examples/PROMPTS.md)
  Prompt examples for common usage patterns.
- [LICENSE](./LICENSE)
  The repository is released under the MIT License.

## What Lives In `SKILL.md`

The README stays intentionally short. See [SKILL.md](./SKILL.md) for the detailed workflow, including:

- preserve mode vs extend mode
- execution order and governance rules
- preview, tuning, and writeback requirements
- output expectations and validation steps

## Maintenance

This repository should track behavior that has been validated in real projects. If the reusable workflow changes, update `SKILL.md`, prompt examples, and the public README in the same pass.

## License

This repository is released under the MIT License. See [LICENSE](./LICENSE) for details.
