---
name: dev-collab-install
description: >-
  安装开发任务协作工具组到项目。检测 codegraph、区分新/已有项目，配合 dual-ai-onboarding 与架构师生成项目配置。
  触发词：安装协作工具、dev-collab 安装、初始化协作工具组。
---

# Dev Collab Toolkit — 安装与项目入驻

> 本技能由 **指挥官** 在首次使用或 `@安装协作工具` 时调用。

## 0. 全局工具组位置

| 平台 | 路径 |
|------|------|
| Cursor | `~/.cursor/skills/dev-collab-toolkit/` |
| Trae | `~/.trae/skills/dev-collab-toolkit/` |
| Trae-CN | `~/.trae-cn/skills/dev-collab-toolkit/` |
| 双 AI 入驻 | `~/.cursor/skills/dual-ai-onboarding/` |

**禁止** 将全局工具组复制到项目 `.trae/skills/`；项目内只放 **项目专属** 配置。

## 1. 强制：Codegraph 检查

```bash
# 在项目根目录
codegraph init -i    # 若尚未初始化
```

Agent 侧：`codegraph_status`

| 状态 | 动作 |
|------|------|
| 已索引 | 记录 files/nodes，继续 |
| 未索引 | **暂停** 结构相关生成，提示用户安装 Codegraph MCP 并执行 init |
| MCP 不可用 | 告知用户配置 Codegraph MCP（见 [README.md](../README.md) Codegraph 章节） |

## 2. 分支：已有项目 vs 新项目

### 2A. 已有项目

1. 调度 **@双AI入驻**（[roles/dual-ai-onboarding/SKILL.md](../roles/dual-ai-onboarding/SKILL.md)）
2. 双 AI 入驻专家执行 canonical + 工具组扩展步骤
3. 检测 `.trae/rules/`、`.cursor/rules/`、`.codegraph/codegraph.db` 是否就绪
4. 若 generic rules 尚未合并，从 [rules/](../rules/) 补缺项目专属规范
5. 输出 **安装报告**

### 2B. 新项目

1. 调度 `@架构师`（[roles/architect/SKILL.md](../roles/architect/SKILL.md)）
2. 架构师提供 2–3 方案 → **用户选择**
3. 用户确认后：
   - 创建目录结构（前后端、`.trae/`、`.cursor/`）
   - 调度 **@双AI入驻** 完成 SSOT / 桥接 / codegraph
   - 创建 `project-helper.md`
4. 输出 **项目初始化报告**

## 3. 安装报告模板

```markdown
## Dev Collab Toolkit 安装报告

**项目类型**: 已有 / 新建
**Codegraph**: ✅ N files / ❌ 需 init

### 已生成/更新
- [ ] `.trae/rules/*`
- [ ] `.cursor/rules/*` 桥接
- [ ] `.trae/skills/project-helper.md`
- [ ] `.trae/iterations/`

### 角色技能（全局，无需复制）
- 指挥官 → dev-collab-toolkit
- @双AI入驻 / @dual-ai-onboarding
- @提示词优化专家 / @需求分析拆解师 / @全栈工程师 / @code review / @测试工程师 / @架构师

### 下一步
1. 确认 Customize → Rules 桥接已启用
2. 发起开发任务：`@指挥官` 或 `开发协作`
```

## 4. 角色关系

| 角色 | 职责 |
|------|------|
| **@双AI入驻** | SSOT/桥接/codegraph/前后端目录（工具组内置角色） |
| **dev-collab-install** | 安装编排：调度 @双AI入驻 / @架构师 |
| **指挥官** | 开发任务多角色 workflow |

安装时：**指挥官/install → @双AI入驻**（已有项目）或 **@架构师 → @双AI入驻**（新项目）。

## 5. 成功标准

- [ ] `codegraph.db` 可查询
- [ ] 项目 `.trae/rules/` 与 `.cursor/rules/` 桥接正常
- [ ] 全局工具组未复制到项目内
- [ ] 用户可以用 `@指挥官` 发起开发协作 workflow
