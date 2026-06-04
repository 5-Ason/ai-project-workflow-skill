# Usage Examples

These examples show when to use the skill and what a good result should look like.

## Audit an Existing Workflow

Prompt:

```text
查看我现有的 skills 和 AGENTS.md，会不会太多重复、太重了？每次跑任务都执行很久。
```

Expected result:

- Read the current repository rules before suggesting changes.
- Identify duplicate or stale instructions.
- Recommend what belongs in `AGENTS.md`, what belongs in docs, and what belongs in reusable skills.
- Avoid editing files unless the user asks to implement the plan.

## Standardize a Repository

Prompt:

```text
把这个仓库的 AI 协作规范标准化，方便后续任务自动维护 dev-log、iteration-index 和 project-state。
```

Expected result:

- Create or refine `AGENTS.md` as the entry guide.
- Add or update automatic recording rules.
- Define `direct`, `brief`, `standard`, and `decision` levels.
- Add a project-state policy that keeps stable facts separate from task logs.
- Add validation commands and final reporting rules.

## Keep the Workflow Lightweight

Prompt:

```text
这个项目已经有一套开发流程了。你对比一下，现有流程够不够，还需要补充什么？
```

Expected result:

- Preserve useful project-specific rules.
- Add only the missing guardrails.
- Avoid copying a generic template over the project’s existing workflow.
- Move long examples or templates into reference docs instead of bloating `AGENTS.md`.

## Decide the Recording Level

For a small text or style fix, Codex should usually choose `direct` and write only the minimal log required by the project.

For a single page or service method, Codex should usually choose `brief`.

For cross-module changes, contracts, database changes, permission rules, routing, or core business models, Codex should usually choose `standard`.

For long-lived product or technical choices, Codex should choose `decision`.

## Project-State Boundary

Codex should evaluate `project-state` after each repository change, but should not update it for every task.

Write to project state when:

- Runnable modules change.
- Long-term priorities change.
- Known limitations change.
- Deployment status changes.
- Contract boundaries or core workflow facts change.

Do not write to project state for:

- Ordinary bug fixes.
- One-time implementation details.
- Temporary debugging notes.
- Command output already captured in `dev-log`.
- Short-lived TODOs.