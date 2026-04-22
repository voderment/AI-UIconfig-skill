<img width="1955" height="1297" alt="CliperX Image 2026-04-22 11 44 52-2" src="https://github.com/user-attachments/assets/1afe7512-d76a-47ce-a371-c97fcd0242c1" />

[English](./README.md) | 简体中文

# AI-UIconfig-skill

`AI-UIconfig-skill` 是一个可复用的 agent skill，目标是在应用开发过程中，让 UI 的调节更精细、更高效，也更容易反复迭代。

它尤其适合 SwiftUI 项目。对于这类项目，团队常常需要一种更好的方式，把视觉结构与运行时逻辑分离开来，在隔离环境里预览界面，并且更细致地调整 UI，而不必反复陷入缓慢的“改代码-编译-运行”循环。

这个 skill 的重点不是把 UI 调整当作零散的一次性修改，而是把它变成一个可控的工作流。最终效果是：代码库更容易迭代、更容易检查，也更适合在保持产品视觉意图的前提下做精细化打磨。

它特别适用于以下场景：

- UI 代码和运行时逻辑混在一起
- 样式值分散硬编码在许多文件里
- Xcode Canvas 预览难以高效使用
- 视觉调节需要频繁经历“修改-构建-运行”的重复流程
- 团队希望有一个仅在 `DEBUG` 下启用的运行时编辑器，并支持精确写回源码

## 它能做什么

这个 skill 会帮助 agent 把 SwiftUI 代码库整理成一套更适合精细化 UI 调节的工作流。通常包括：

- 在运行时逻辑和纯 UI 之间建立 `Render State` 边界
- 引入受治理的样式 tokens / metrics
- 提供预览 mock 和预览 gallery
- 提供一个仅在 `DEBUG` 下启用的实时调节编辑器，并且这个编辑器不是固定的通用面板，而是根据项目里实际存在的受治理界面和参数自动生成
- 支持保存调节快照，并显式重新加载
- 支持单个 token 重置和整轮会话回退
- 对已批准的叶子常量做精确写回
- 写回时保留合法的源码字面量格式，降低文件损坏风险
- 基于值区间的写回，尽量保留现有声明结构和注释
- 使用单一的源码启动基线，避免写回后与重复的默认 token 表发生偏离

这个编辑器不应该是一个预先写死布局和字段的固定面板。它应当从项目真实存在的结构和已治理参数出发自动生成，这样调节界面和参数集合才能真正贴合应用本身，而不是把所有项目都硬塞进同一套模板。

当你需要更精细地调 spacing、size、opacity、corner radius、语义色或其他稳定的视觉参数时，它会比零散手改源码更高效、更可控。

## 默认原则

默认模式是 `preserve mode`。

这意味着：

- 不应有意重新设计现有 UI
- 不应有意改变现有交互行为
- 第一目标是提升治理能力和可调试性，而不是视觉重塑

它的核心目标不是重做设计，而是让 UI 的调整、维护和演进更容易。

如果项目里已经有新增 UI，需要纳入同一套治理体系，也可以使用 `extend mode`。

## 为什么特别适合 SwiftUI

SwiftUI 天然适合这类工作流，因为它很适合建立清晰的渲染边界、构造可预览的视图输入，以及复用样式 token。

随着 SwiftUI 项目变大，视觉参数通常会分散到很多 view 和 modifier 中，导致精细化 UI 调整越来越困难。这个 skill 的作用，就是把这些值收拢到一套更受治理的结构里，让视觉调整变得更快、更清晰，也更不容易出错。

如果你的目标是在不破坏现有产品意图的前提下，获得更好的检查、预览、调节和有选择地写回源码的能力，这个 skill 就特别合适。

## 核心工作流

推荐按下面的顺序推进：

1. 盘点关键 UI 界面和状态。
2. 拆分 runtime/composer 代码与纯 UI 代码。
3. 引入适合预览的 render-state 输入。
4. 将稳定的样式值 token 化。
5. 建立 preview mock 和 gallery 状态。
6. 添加一个仅在 `DEBUG` 下启用、并根据项目实际受治理界面和参数自动生成的实时调节编辑器。
7. 保存快照，并支持显式重新加载已保存配置。
8. 为已批准的源码常量增加精确写回。
9. 验证构建、预览以及必要的手动运行时行为。

## 关键规则

- 默认保留现有产品意图。
- 不要把每一个常量都暴露成运行时控制项。
- 默认只本地化说明文字和工具 UI，不本地化面向代码的 token key。
- 除非用户明确要求自动恢复，否则重启后应回到源码定义的基线。
- 保存的配置应该是用户显式选择重新加载的快照。
- 写回必须显式、精确，并且避免破坏性修改。

## 最适合的场景

这个 skill 很适合以下情况：

- 应用基于 SwiftUI
- 同一批 UI 界面会被频繁迭代
- 布局和样式值存在重复
- 设计师或开发者需要更快、更精细的视觉迭代
- 项目依赖 Canvas 预览和隔离 mock 状态
- 团队希望以更安全的方式做 UI 微调，而不是进行大范围重构

以下情况则不太适合作为首选方案：

- 用户想要一套全新的视觉设计语言
- 代码库只需要一个很小的一次性样式调整
- 主要问题并不在 UI，而在运行时逻辑或持久化层

## 仓库内容

- [SKILL.md](./SKILL.md)
  Codex 风格 agent 实际使用的 skill 定义。
- [examples/PROMPTS.md](./examples/PROMPTS.md)
  常见使用场景的 prompt 示例。
- [LICENSE](./LICENSE)
  本仓库采用 MIT License。

## 如何使用

### 1. 作为本地 Skill 安装

把这个仓库复制或软链接到 agent 可以读取的本地 skill 目录中。

示例：

```bash
mkdir -p ~/.agents/skills
ln -s "/absolute/path/to/AI-UIconfig-skill" ~/.agents/skills/AI-UIconfig-skill
```

如果你已经使用其他本地 skill 目录，也可以放到你自己的目录结构中。

### 2. 在 Prompt 中调用

可以直接这样写：

- `Use AI-UIconfig-skill to refactor this SwiftUI surface into render-state and previewable UI.`
- `Use AI-UIconfig-skill in preserve mode. Do not change the visual design.`
- `Use AI-UIconfig-skill to add a DEBUG-only token editor with saved configs and writeback.`
- `Use AI-UIconfig-skill to fold this new module into the existing token/preview/writeback system.`

### 3. 选择模式

- `preserve mode`
  适用于你不希望视觉上被明显改动的现有 UI。
- `extend mode`
  适用于已经存在的新 UI，需要被纳入同一套治理系统。

## 预期产出

当这个 skill 被正确应用后，项目通常会得到：

- 更清晰的 `UI/` 结构
- 不依赖真实运行时对象、可以单独预览的纯 UI 视图
- 对关键状态的 render-state mock 覆盖
- 面向稳定治理值的 debug-only 编辑器
- 外部保存的调节快照
- 显式的源码常量写回映射

更重要的是，它能让团队在开发过程中更实际地进行精细化 UI 调节，而不必把每一次视觉微调都变成手工搜索和零散修改。

## 关于本地化

对于运行时调节工具，这个仓库默认假设：

- token key 保持面向代码且稳定
- 参数标题可以继续贴近源码语义
- 说明性文案和工具界面语言应跟随当前 UI 语言

这样既能保证工具可理解，也不会污染代码层面的命名体系。

## 建议发布检查清单

在面向更广泛用户发布之前，建议确认：

- `SKILL.md` 与你在真实项目中验证过的行为一致
- prompt 示例仍然符合当前工作流
- 仓库说明与您实际使用的本地 skill 安装路径一致
- 当前发布的 license 仍然符合你希望他人复用仓库的方式

## 维护规则

这个仓库应该持续对齐那些已经在真实项目中验证过的行为。

当某个项目里的受治理 UI 工作流发生变化时，维护者应明确判断 skill contract 是否也发生了变化。

通常需要重新评估的变化包括：

- render-state 边界变化
- preview 覆盖规则变化
- token 范围变化
- 运行时编辑器行为变化
- 快照保存/加载行为变化
- 单项回退或整轮回退语义变化
- 写回目标或路径解析变化
- 调节工具的本地化规则变化
- 源码基线与已保存快照之间的会话行为变化

如果这些变化影响了这套治理工作流本身，就应该同步更新 `SKILL.md`，并在同一轮维护里更新公开仓库。

## License

本仓库采用 MIT License。

这意味着其他开发者可以在保留版权声明和许可文本的前提下，以较低限制使用、修改和分发这个 skill。
