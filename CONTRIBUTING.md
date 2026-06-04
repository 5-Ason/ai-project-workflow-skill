# Contributing

Thanks for improving this skill.

## What Belongs Here

Good contributions:

- Make the workflow easier for Codex to apply across different repositories.
- Improve task-level guidance without making small tasks heavier.
- Clarify `AGENTS.md`, project memory, `project-state`, validation, or task-level rules.
- Add concise examples that help maintainers use the skill.

Avoid contributions that:

- Add project-specific paths, ports, credentials, or business rules.
- Turn the skill into a long knowledge base.
- Duplicate the same rule in several files.
- Require a specific framework, package manager, or hosting provider unless clearly marked as an example.

## Editing Guidelines

- Keep `SKILL.md` short and procedural.
- Put detailed guidance in `references/` or `docs/`.
- Prefer concrete instructions over broad advice.
- Preserve the lightweight task levels: `direct`, `brief`, `standard`, and `decision`.
- Keep `project-state` as a stable facts summary, not a task log.

## Validation

Before opening a pull request:

```bash
python path/to/quick_validate.py path/to/ai-project-workflow
```

Also check manually:

```bash
rg "api[_-]?key|token|secret|password|cookie|Bearer|sk-" .
rg "project-state|direct|brief|standard|decision" SKILL.md references docs
```

Do not commit secrets, local credentials, private server addresses, or private project data.