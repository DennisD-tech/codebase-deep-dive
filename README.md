# codebase-deep-dive（Cursor Skill）

这是一个 **Cursor Agent Skill**，用于对指定的开源项目/项目文件夹做“从 0 到可行动”的深度分析，并产出结构化报告与图解（Mermaid）。

## 如何启用 / 启动

1. 确认 Skill 文件存在：
   - `C:\Users\JJH\.cursor\skills\codebase-deep-dive\SKILL.md`
2. **重启或 Reload Cursor**（让 Cursor 重新发现 Skills）。
3. 在 Cursor 的 Agent 聊天中通过 **斜杠命令**显式调用：

示例：
- `/codebase-deep-dive @.`
- `/codebase-deep-dive @src/ 我想做重构评估，并补齐测试`
- `/codebase-deep-dive https://github.com/<owner>/<repo>.git 我在尝试维护它`

> 说明：该 Skill 默认是“显式触发”模式（不会自动乱触发），只有你输入 `/codebase-deep-dive` 才会生效。

## 功能概览

- **项目地图**：目录结构、关键模块、入口点、核心调用链/数据流线索
- **架构与边界**：架构风格、模块边界与耦合、反模式与技术债热点（带证据）
- **依赖与风险**：核心依赖、潜在安全/供应链/配置风险、可执行审计命令建议
- **质量与测试**：可维护性热点、测试现状、最小可落地测试策略
- **行动清单**：高/中/低优先级改造建议 + 验证方式 + 两阶段路线图
- **图解（Mermaid）**：
  - 流程图：解释“事件/请求如何被处理”，包含异常分支
  - 架构图：解释“模块如何组织、依赖方向是什么”，避免只给目录树

## 使用场景

- **接手陌生仓库**：快速搞清入口、关键路径、风险点
- **维护旧项目**：定位高变更风险面（协议/解析/外部依赖），制定最小修复方案
- **重构前评估**：识别模块边界、耦合点与可测试性缺口，给出路线图
- **安全/供应链排查**：快速列出依赖与潜在风险线索，并给出审计命令

## 输出结果（固定结构）

调用后会按以下 7 个标题输出（顺序固定）：

1. **Executive Summary（要点）**
2. **Project Map（项目地图）**
3. **Architecture & Boundaries（架构与边界）**
4. **Dependencies & Risks（依赖与风险）**
5. **Quality & Testing（质量与测试）**
6. **Action Plan（行动清单与路线图）**
7. **Diagrams（图解）**

其中 **Diagrams（图解）** 必须包含两段 Mermaid 代码块：
- 一个用于“事件/请求处理逻辑”的流程图（`flowchart TD` 或 `sequenceDiagram`）
- 一个用于“模块架构与依赖方向”的架构图（`graph LR`）

