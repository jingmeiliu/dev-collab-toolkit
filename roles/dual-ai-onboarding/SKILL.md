---
name: dual-ai-onboarding
description: >-
  双AI入驻专家。检测并配置 Trae/Cursor 双端 SSOT、Cursor 桥接、Codegraph 与前后端目录；
  可单独 @ 使用，也可由指挥官在安装/入驻流程中调度。
  触发词：@dual-ai-onboarding、@双AI入驻、@双AI入驻专家、配置双AI、双AI入驻、项目AI初始化、生成代码地图。
---

# 双 AI 入驻专家（Dual-AI Onboarding）

> **工具组角色** | **canonical SSOT**: `~/.cursor/skills/dual-ai-onboarding/SKILL.md`
> **Trae**: `~/.trae/skills/dual-ai-onboarding.md`

## 职责

让 **Trae** 与 **Cursor** 共同接管项目：检测配置、验证 Codegraph、识别前后端目录、同步 **SSOT（`.trae/`）** 与 **Cursor 桥接（`.cursor/rules/`）**。

可 **单独 @ 调用**，也可由 **指挥官** 在安装流程中调度。

## 执行入口（必须）

1. **Read** canonical 技能全文：`~/.cursor/skills/dual-ai-onboarding/SKILL.md`（Trae 读 `~/.trae/skills/dual-ai-onboarding.md`）
2. 按 canonical 步骤 **1→5** 严格执行
3. 完成后执行下方「工具组扩展步骤」

## 工具组扩展步骤（dev-collab-toolkit 集成）

入驻报告输出后，额外执行：

1. 若项目尚无 dev-collab 规范：从 `~/.cursor/skills/dev-collab-toolkit/rules/` 合并 generic rules 到 `.trae/rules/`（已有项目 SSOT 优先，只补缺）
2. 在报告中增加 **Dev Collab 就绪** 节：
   ```markdown
   ### Dev Collab 就绪
   - [ ] 可用 `@指挥官` 或「开发协作」发起任务
   - [ ] 角色：@提示词优化专家 / @需求分析拆解师 / @全栈工程师 / @code review / @测试工程师
   ```
3. 若由 **指挥官** 调度：回报指挥官并附入驻报告摘要
4. 若用户 **单独 @ 调用**：直接输出完整入驻报告，提示下一步可用 `@指挥官`

## 触发场景

| 场景 | 说明 |
|------|------|
| 单独入驻 | 用户说「配置双 AI」「让 Trae/Cursor 接管项目」 |
| 安装协作工具 | 指挥官/install 调度（已有项目分支 2A 第一步） |
| 架构师之后 | 新项目用户选定方案后，架构师交回本角色执行入驻 |
| 规范缺失 | 开发任务启动时发现 `.trae/rules/` 不完整 |

## 禁止

- 在项目中复制全局 `dual-ai-onboarding` 或 `dev-collab-toolkit` 技能文件
- 手写 `.codegraph/index.json` 等 JSON 地图
- 在 `.trae/rules/` SSOT 中写入 Cursor frontmatter

## 成功标准

- [ ] `codegraph.db` 可查询
- [ ] `.trae/rules/` 完整，无 Cursor frontmatter 污染
- [ ] `.cursor/rules/` 桥接正常
- [ ] `version-log.md` 已更新（若项目使用迭代跟踪）
