# AI Project Workflow Skill

An ultra-lightweight AI agent skill for standardizing practical, anti-bloat collaboration workflows in a code repository.

It helps maintainers give coding agents just enough structure—clear rules, a compact factual snapshot, an active TODO list, and automated size guardrails—without drowning the repo in multi-file process ceremonies or ever-growing dev logs.

## Philosophy (v2 Minimal)

Heavy multi-tier documentation workflows (`direct/brief/standard/decision` + `dev-log` + `iteration-index` + separate `prd/`/`design/`/`briefs/`/`decisions/` + multi-state boards) tend to bloat rapidly in solo or small-team repositories and burn context tokens on stale prose.

This skill converges repository governance onto **3 live docs + 2-tier cadence + 1 guardrail script**:

- **3 Live Docs**
  - `AGENTS.md`: stable coding rules, architecture boundaries, validation commands, and high-risk approvals (<= 220 lines).
  - `docs/project-state.md`: overwrite-only factual snapshot of environments, active modules, invariants, and known limits (<= 150 lines / 12 KB).
  - `docs/TODO.md`: single active work list (`In Progress` / `Todo` / `Tech Debt`); delete items when done (<= 120 lines / 10 KB).
  - *(On demand)* `docs/specs/YYYY-MM-DD-<topic>.md`: one-file spec used **only** for major changes.
- **2-Tier Cadence**
  - **Direct Change (default)**: bug fixes, copy/UI tweaks, small configs, single-module enhancements → implement, verify, and let semantic Git commits be the history.
  - **Single-File Spec First (major changes)**: cross-module contracts, schema migrations, permission/state-machine refactors, multi-module features → write one concise spec, confirm boundaries, implement, and update `project-state.md` only if stable facts changed.
- **Automated Anti-Bloat Guardrails**
  - Pair the rules with a tiny script (e.g., `scripts/check-doc-memory.mjs`) that enforces required entry files, line/byte caps, UTF-8 without BOM, and zero broken links in live docs.

## Repository Structure

```text
.
|-- SKILL.md                          # Skill trigger and core minimal workflow
|-- agents/openai.yaml                # UI metadata for skill discovery
|-- references/
|   |-- agent-guide-template.md       # Compact AGENTS.md template
|   |-- auto-recording.md             # Live-doc boundaries, spec template, and guardrail script guide
|   `-- iteration-levels.md           # Two-tier cadence and workflow slimming principles
|-- docs/
|   `-- usage-examples.md             # Example prompts and expected outputs
|-- CONTRIBUTING.md
|-- SECURITY.md
`-- LICENSE
```

## Installation

Clone this repository into your agent's skills directory.

### Codex (macOS / Linux)

```bash
git clone https://github.com/5-Ason/ai-project-workflow-skill.git ~/.codex/skills/ai-project-workflow
```

### Codex (Windows PowerShell)

```powershell
git clone https://github.com/5-Ason/ai-project-workflow-skill.git "$env:USERPROFILE\.codex\skills\ai-project-workflow"
```

### Antigravity / Other Skill-Compatible Agents

Clone into your configured skills directory (for example `~/.gemini/config/skills/ai-project-workflow`) and restart or start a new session.

## Example Prompts

```text
查看我现在的开发流程和 AGENTS.md，是不是太冗余了？给一个极致精简的瘦身方案。
```

```text
给这个仓库建立一套极简的 AI 协作规范：AGENTS.md、project-state、TODO、单文件 spec 模板和防膨胀检查脚本。
```

```text
对比一下当前项目流程：哪些工程护栏必须保留，哪些过程文档可以归档精简？
```

More examples are in [docs/usage-examples.md](docs/usage-examples.md).

## Validation

At minimum, check that:

- `SKILL.md` has valid frontmatter with `name` and `description`.
- The skill name is lowercase hyphen-case (`ai-project-workflow`).
- All files are `UTF-8 without BOM` with valid relative links.
- No private paths, tokens, secrets, project-specific credentials, or production data are committed.

## Scope

This skill does not run external services, modify GitHub by itself, or enforce a specific framework. It gives coding agents reusable instructions for keeping repository workflows lean, verifiable, and bloat-free.

## License

MIT. See [LICENSE](LICENSE).
