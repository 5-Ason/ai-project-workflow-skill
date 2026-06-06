---
name: ai-project-workflow
description: Standardize lightweight AI collaboration and development workflows for a code repository. Use when the user asks to create or improve AGENTS.md, AI coding guidelines, project iteration workflow, Current/Proposal process, direct/brief/standard/decision task levels, dev-log, project-state, automatic project memory, decision records, PRD/brief templates, or cross-project AI development governance. Also use when auditing whether an existing workflow is too heavy or too loose. Do not use for ordinary one-file fixes, simple explanations, running tests, or small implementation tasks unless the user explicitly asks to standardize or document the workflow.
---

# AI Project Workflow

## 目标

帮助 Codex 为一个代码仓库建立或优化轻量、可执行、可长期维护的 AI 协作流程。重点是让后续任务能按风险选择流程、保留必要项目记忆、完成前可验证，而不是给所有小任务套重流程。

## 工作方式

1. 先审计仓库事实：读取 `AGENTS.md`、`CLAUDE.md`、README、项目文档、脚本、测试入口和现有日志/决策文档。不要先套模板。
2. 判断当前诉求属于流程建设、流程审计、复杂迭代规划，还是普通开发任务。普通小修不引入额外文档流程。
3. 若要建立或优化流程，先保留已有约定，再补最小缺口：Todo 预备池、任务分级、Current/Proposal、自动记录、项目状态维护、验证规则、高风险边界、Git 和完成汇报。
4. 写规则时使用项目自己的路径、技术栈和命令；不要把某个项目的端口、业务词、SQL 目录或框架约定硬套到其他仓库。
5. 收尾前检查 diff、验证结果和新增文档范围；说明哪些规则已落地，哪些只是建议。

## 推荐流程骨架

- `direct`：低风险小修、小文案、单文件配置或单接口小修。直接实现，收尾只记录必要 dev-log；默认不更新 project-state。
- `brief`：单模块功能或体验变化。先写轻量 brief，说明目标、非目标、验收和影响文件，再实现。
- `standard`：跨模块、接口契约、数据库、权限、路由、核心业务模型或用户可见主流程变化。先写 PRD、设计说明或技术说明，再实现；默认检查 project-state。
- `decision`：长期规则或技术路线选择。写 decision，记录背景、选择、备选方案、影响和复审条件；默认检查 project-state。

需要更完整分级说明时读取 `references/iteration-levels.md`。

## Todo 预备池与正式看板

- 如果仓库需要管理“还没进入正式开发”的 bug、需求方向或优化想法，优先建立一个轻量 Todo 预备池，而不是把它们直接塞进正式迭代看板。
- 推荐分层：Todo 看板只管待分流事项和当前状态；详情记录只放背景、复现、验收和关联材料；正式 iteration-index 或等价看板只记录已进入开发链路或已有沉淀的事项。
- Todo 看板应作为状态唯一来源，详情文档不要重复维护状态，避免看板和详情漂移。
- 事项从 Todo 进入开发时，再按 `direct`、`brief`、`standard` 或 `decision` 分流，并链接到 brief、PRD、设计说明、decision 或 dev-log。
- 完成、取消或长期搁置的 Todo 应定期归档，避免当前看板无限变长。

## 项目状态维护

- project-state 是滚动项目事实摘要，不是任务日志；每次仓库产生改动后都要评估是否需要更新，但不要每次强制写。
- 只有影响后续开发判断的稳定事实才写入，例如可运行模块、近期重点、已知问题、下一步优先级、长期决策、部署状态、契约边界或核心流程变化。
- 普通 bugfix、单次实现细节、短期排查过程、临时 TODO 和已写入 dev-log 的过程记录不要写入 project-state。
- 如果更新项目状态，同步更新文件顶部日期，并确保任务索引或等价入口能找到相关沉淀。
## Current 与 Proposal

- `Current` 只记录当前真实事实：已存在页面、接口、配置、数据结构、部署状态、验证结果或已知限制。
- `Proposal` 只记录未来方案：准备怎么改、为什么改、如何验收、影响哪些模块。
- 不要把未来设想写进 Current，也不要让 Proposal 变成没有状态的散文。

## 调试与验证原则

- bug、测试失败或异常行为先复现、读错误、追调用链和数据流，确认根因后再修。
- 连续 3 次修复失败，停止继续堆补丁，重新评估假设、边界或架构。
- 测试按风险决定深度，不强制所有任务 TDD。权限、鉴权、状态机、跨端契约、数据库、上传、计费、收益或核心业务规则优先补可失败测试、最小复现或等价自动化检查。
- 完成前用最新命令输出、页面检查、截图、接口响应或文件 diff 支撑结论。只能部分验证时写清原因。

## 可复用引用

- `references/iteration-levels.md`：任务分级和记录策略。
- `references/agent-guide-template.md`：通用 `AGENTS.md` 结构模板。
- `references/auto-recording.md`：自动项目记忆和 dev-log 规则。

## 输出要求

- 如果用户只是要审计，输出问题、风险和建议，不改仓库。
- 如果用户要求落地，优先改少量入口文档，例如 `AGENTS.md`、`docs/auto-recording.md`、`docs/project-state.md`、`docs/todo/board.md`、`docs/iteration-index.md` 或项目已有等价文件。
- 最终回复说明改了什么、验证了什么、记录在哪里；如果按规则不记录，也说明原因。