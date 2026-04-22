<img width="1955" height="1297" alt="CliperX Image 2026-04-22 11 44 52-2" src="https://github.com/user-attachments/assets/1afe7512-d76a-47ce-a371-c97fcd0242c1" />

[English](./README.md) | 简体中文

# AI-UIconfig-skill

`AI-UIconfig-skill` 是一个可复用的 skill，用来把现有 SwiftUI 代码库整理成更易治理的 UI 工作流：包含 render-state 边界、preview mock、样式 token 化，以及仅在 `DEBUG` 下启用的调参和写回工具。

它面向的是那些希望提升 UI 迭代效率、但不想顺手把产品重新设计一遍的团队。

## 适用场景

适合在这些情况下使用：

- SwiftUI UI 代码和运行时逻辑混在一起
- 样式值分散硬编码在许多文件里
- preview 和 mock 状态难维护
- 视觉调节仍然依赖缓慢的“改代码-编译-运行”循环
- 团队希望对已批准的 UI 常量做更安全、更窄范围的源码写回

以下情况不适合作为首选方案：

- 目标是重新做一套视觉设计语言
- 代码库只需要一个很小的一次性 UI 修改
- 主要问题不在 UI，而在运行时逻辑或持久化层

## 你会得到什么

正确应用后，项目通常会得到：

- 更清晰的 runtime/UI 边界
- 可安全预览的 render-state 输入
- 受治理的 tokens 和 metrics
- 覆盖关键状态的 preview mocks 和 gallery
- 根据真实受治理界面生成、并尽量继承项目现有设计语言的 `DEBUG` 实时调节编辑器
- 可保存的调节快照与显式重载
- 对已批准叶子常量的精确写回

默认行为是 `preserve mode`：保持现有产品意图，重点提升控制力，而不是重做视觉设计。只有当新增 UI 需要被纳入同一套体系时，才使用 `extend mode`。

## 如何使用

### 安装

把这个仓库复制或软链接到本地 skills 目录。

```bash
mkdir -p ~/.agents/skills
ln -s "/absolute/path/to/AI-UIconfig-skill" ~/.agents/skills/AI-UIconfig-skill
```

如果你已经使用其他本地 skills 目录，也可以直接放到对应位置。

### 在 Prompt 中调用

示例：

- `Use AI-UIconfig-skill to refactor this SwiftUI surface into render-state and previewable UI.`
- `Use AI-UIconfig-skill in preserve mode. Do not change the visual design.`
- `Use AI-UIconfig-skill to add a DEBUG-only token editor with saved configs and writeback.`
- `Use AI-UIconfig-skill to fold this new module into the existing token/preview/writeback system.`

## 仓库内容

- [SKILL.md](./SKILL.md)
  skill 的正式定义和执行约束。
- [examples/PROMPTS.md](./examples/PROMPTS.md)
  常见使用场景的 prompt 示例。
- [LICENSE](./LICENSE)
  本仓库采用 MIT License。

## 细节放在 `SKILL.md`

这个 README 刻意保持精简。更详细的工作流说明放在 [SKILL.md](./SKILL.md)，包括：

- preserve mode 和 extend mode 的边界
- 执行顺序与治理规则
- preview、调参、写回的要求
- 产出预期与验证步骤

## 维护

这个仓库应持续对齐那些已经在真实项目中验证过的行为。只要可复用工作流发生变化，就应在同一轮维护里同步更新 `SKILL.md`、prompt 示例和公开 README。

## License

本仓库采用 MIT License。详见 [LICENSE](./LICENSE)。
