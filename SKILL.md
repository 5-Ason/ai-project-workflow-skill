---
name: ai-project-workflow
description: Standardize ultra-lightweight AI collaboration and development workflows for a code repository. Use when the user asks to create, simplify, or audit AGENTS.md, AI coding guidelines, two-tier development cadence (direct change vs single-file spec), project-state snapshots, active TODO lists, doc-bloat guardrails, or repository-level AI governance. Also use when diagnosing whether an existing documentation workflow has become too heavy or bloated. Do not use for ordinary fixes, simple explanations, running tests, or small implementation tasks unless the user explicitly asks to standardize or audit the workflow.
---

# AI Project Workflow

## 目标

帮助 AI 编码代理为一个代码仓库建立或瘦身出一套**极简、可执行、防膨胀**的协作流程。核心是把精力留在代码、契约、测试与发布护栏上，而不是维护多层过程文档和流水账。

## 工作方式

1. **先审计仓库事实**：读取 `AGENTS.md`、`CLAUDE.md`、`README.md`、现有文档目录、构建/测试/发布脚本与体积大小。不盲目套模板。
2. **判断诉求边界**：区分流程审计、流程瘦身、新项目建流程与普通开发任务。普通代码改动不引入额外流程文档。
3. **保留硬工程护栏，砍掉过程噪音**：优先保留并强化契约校验、数据库迁移目录、自动化测试与发布/授权边界；对膨胀的流水账日志、多态看板和重复文档，主动建议归档或合并。
4. **贴合项目自身**：写规则时只用项目真实路径、技术栈与命令；不把其他项目的端口、业务词、框架约定带入当前仓库。
5. **用脚本锁死防膨胀红线**：不要只靠文字写“保持简短”，应优先配套一个轻量检查脚本，在 CI 或发版前强制校验核心入口存在、体积未超限、活文档无断链。

## 核心骨架：3 个活文档 + 2 档节奏

### 1. 只维护 3 个日常活文档（+ 按需单文件方案）

| 文件 | 唯一职责 | 防膨胀硬约束 |
| --- | --- | --- |
| `AGENTS.md` | AI 入口护栏：编码规范、架构红线、验证命令、高风险授权 | 精简紧凑（建议 ≤ 220 行），不堆大段过程模板 |
| `docs/project-state.md` | 当前系统客观快照：运行环境、核心模块现状、关键边界、未解决的坑 | **覆盖式更新**，禁止追加历史流水账（建议 ≤ 150 行 / 12 KB） |
| `docs/TODO.md` | 唯一活跃工作清单：仅保留「进行中 / 待排查与待做 / 技术债」 | **做完直接删行**，Git 历史即记录（建议 ≤ 120 行 / 10 KB） |
| `docs/specs/`（按需） | 仅大改使用的单文件方案（目标、边界、接口/SQL、验证写在一页里） | 一个大改只建 1 个文件，不拆成 PRD + design + brief + plan 多文件 |

> **默认不新建的高噪音文档**：除非用户明确要求，否则**不再**引入按月 `dev-log/`、`iteration-index` 大表、独立 `decisions/` / `briefs/` 目录、多态看板（Inbox/Ready/Doing/Blocked/Done）或强制 UI 截图同步。若审计发现这些文档已严重膨胀或长期空转，建议将其只读归档至 `docs/archive/`。
>
> 若项目已有自动发版审计目录（如 `docs/release-log/`），继续由发布脚本专用维护，日常开发不碰。

### 2. 开发节奏只分 2 档

- **直接改（默认）**：bugfix、文案、样式、小配置、单模块小需求。读懂相关代码后直接修改、跑对应验证，并用清晰语义化的 Git commit 记录历史，不写过程文档。
- **先写一页方案再改（大改）**：涉及跨端/跨模块契约、数据库改表 SQL、权限/状态机重构、多模块新功能或长期架构调整时，先在 `docs/specs/YYYY-MM-DD-<topic>.md` 写 1 份简洁单文件方案，确认边界与验收后再写代码。

需要更详细边界与防膨胀脚本规范时，读取 `references/iteration-levels.md` 和 `references/auto-recording.md`。

## 调试、验证与安全原则

- **先根因后修复**：遇到 bug 或测试失败，先复现、读错误、追调用链和数据流；连续 3 次修复失败或持续引入新耦合时停止试错，重新评估假设或架构。
- **按风险决定测试深度**：不强制所有小修 TDD；权限、鉴权、状态机、跨端契约、数据库、上传、计费或核心业务规则优先补可失败测试或等价自动化检查。
- **高风险操作必须明确授权**：数据删除、历史重写、force-push、默认分支 push、凭证/密钥、计费、部署与生产数据变更前先复述影响范围和回退方式。
- **完成前用最新证据汇报**：以最新命令输出、测试结果、页面核验或 `git diff --stat` 支撑结论；有未验证项必须写明原因与建议命令。

## 可复用引用

- `references/iteration-levels.md`：2 档开发节奏边界与反膨胀判断。
- `references/auto-recording.md`：3 个活文档维护边界、单文件 spec 模板与校验脚本建议。
- `references/agent-guide-template.md`：极简通用 `AGENTS.md` 模板。

## 输出要求

- 仅审计时：只输出膨胀点、保留建议和精简方案，不改仓库文件。
- 要求落地时：聚焦改造核心入口文档与校验脚本，历史旧文档优先只读归档而非静默丢失；收尾检查 `git diff --stat`、`git status --short` 并运行验证命令。
- 最终回复简洁说明改了什么、验证了什么、各入口文档体积与风险提示。
