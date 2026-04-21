# Prompt Examples

These examples assume the skill is installed locally as `AI-UIconfig-skill`.

## Preserve Existing UI

```text
Use AI-UIconfig-skill in preserve mode.
Refactor this SwiftUI notch surface into render-state and previewable UI.
Do not intentionally change the current visual design or interaction behavior.
```

## Add A Debug-Only Tuning Editor

```text
Use AI-UIconfig-skill to add a DEBUG-only runtime token editor.
Support single-token reset, whole-session revert, saved config snapshots, and precise writeback.
```

## Govern A New Module

```text
Use AI-UIconfig-skill in extend mode.
This new SwiftUI module already exists.
Fold it into the existing token, preview, runtime tuning, and writeback system.
Do not redesign it.
```

## Preview-First Refactor

```text
Use AI-UIconfig-skill to split this feature into runtime/composer and pure UI layers.
Add render-state mocks and preview galleries for the major states first.
```

## Tokenize Stable Styles Only

```text
Use AI-UIconfig-skill to extract the stable layout and spacing values from this SwiftUI surface.
Do not expose every constant.
Only add values that are worth governing and tuning more than once.
```
