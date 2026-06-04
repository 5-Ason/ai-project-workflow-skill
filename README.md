# AI Project Workflow Skill

A Codex skill for standardizing lightweight AI collaboration workflows in a repository.

It helps maintainers set up project-specific rules for AI coding agents without turning every small change into a heavyweight process. The skill focuses on practical repository governance: `AGENTS.md`, task levels, project memory, Current/Proposal separation, and evidence-based validation.

## What This Skill Does

Use this skill when you want Codex to create, audit, or improve an AI development workflow for a codebase.

It helps Codex:

- Create or refine `AGENTS.md` as the AI entry guide for a repository.
- Define task levels: `direct`, `brief`, `standard`, and `decision`.
- Keep project memory useful through `dev-log`, `iteration-index`, and `project-state` rules.
- Separate `Current` facts from `Proposal` plans.
- Add guardrails for risky operations, debugging, validation, Git, and final reporting.
- Avoid over-documenting small fixes or duplicating rules across too many files.

The skill is intentionally lightweight. It should not trigger for ordinary one-file fixes, simple explanations, or small implementation tasks unless the user explicitly asks to standardize the workflow.

## Why It Exists

AI coding agents work better when a repository tells them how to collaborate. Many projects need a small amount of structure:

- What must the agent read first?
- Which changes need a brief or PRD?
- When should the agent update a development log?
- What belongs in project state, and what should stay out?
- Which checks must pass before the agent says the task is done?

This skill turns those questions into a reusable workflow that Codex can adapt to each repository.

## Repository Structure

```text
.
|-- SKILL.md                         # Skill trigger and core workflow
|-- agents/openai.yaml               # UI metadata for Codex skill discovery
|-- references/
|   |-- agent-guide-template.md       # AGENTS.md structure template
|   |-- auto-recording.md             # Project memory and logging rules
|   `-- iteration-levels.md           # direct / brief / standard / decision guide
|-- docs/
|   `-- usage-examples.md             # Example prompts and expected outputs
|-- CONTRIBUTING.md
|-- SECURITY.md
`-- LICENSE
```

## Installation

Clone the repository into your Codex skills directory.

### macOS / Linux

```bash
git clone https://github.com/5-Ason/ai-project-workflow-skill.git ~/.codex/skills/ai-project-workflow
```

### Windows PowerShell

```powershell
git clone https://github.com/5-Ason/ai-project-workflow-skill.git "$env:USERPROFILE\.codex\skills\ai-project-workflow"
```

Restart Codex or start a new thread so the skill list reloads.

## Example Prompts

```text
帮我审计这个仓库的 AGENTS.md，看看规则是不是太重、重复太多。
```

```text
给这个项目建立轻量 AI 协作流程：任务分级、dev-log、project-state 和验证规则。
```

```text
把这个仓库的 AI 协作规范标准化，方便后续任务自动维护 dev-log 和 project-state。
```

```text
这个项目已有开发流程了。对比一下，哪些规则该保留，哪些该精简？
```

More examples are in [docs/usage-examples.md](docs/usage-examples.md).

## Who Should Use It

This skill is useful for maintainers who want AI agents to help with coding, review, triage, documentation, or release support while preserving repository-specific rules. It is especially helpful for small teams and solo maintainers who need project memory without a heavy process layer.

## Project Memory Model

The skill distinguishes between several memory surfaces:

- `AGENTS.md`: stable rules the agent must know before every task.
- `dev-log`: task-level history and verification results.
- `iteration-index`: a compact index of product or implementation artifacts.
- `project-state`: rolling facts that affect future development decisions.
- `brief`, `PRD`, `design`, `decision`: deeper documents for larger or longer-lived changes.

`project-state` is not a task log. Codex should evaluate it after each repository change, but only update it when stable facts change.

## Validation

If you have the Codex skill creator utilities available, validate the skill folder with:

```bash
python path/to/quick_validate.py path/to/ai-project-workflow
```

At minimum, check that:

- `SKILL.md` has valid frontmatter with `name` and `description`.
- The skill name is lowercase hyphen-case.
- No private paths, tokens, secrets, project-specific credentials, or production data are committed.
- Public-facing documentation explains how to install and use the skill.

## Scope

This skill does not run external services, modify GitHub by itself, or enforce a specific framework. It gives Codex reusable instructions for creating repository-specific workflows.

It is not a replacement for project tests, code review, or maintainer judgment. Treat it as a workflow guide that helps Codex make better local decisions.

## License

MIT. See [LICENSE](LICENSE).