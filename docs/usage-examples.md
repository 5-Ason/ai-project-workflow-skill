# Usage Examples

These examples show when to use the skill and what a good result looks like.

## Audit and Slim Down a Bloated Workflow

Prompt:

```text
查看我现在的开发流程和 AGENTS.md，是不是太冗余了？给一个极致精简的瘦身方案。
```

Expected result:

- Measure actual file counts, disk usage, and active vs stale items before proposing changes.
- Separate high-value engineering guardrails (API contracts, SQL migrations, tests, release scripts) from high-noise process docs (`dev-log`, oversized index tables, unused multi-state boards).
- Propose collapsing into **3 live docs + 2-tier cadence + a size/link guardrail script**.
- Present archive/deletion trade-offs clearly and wait for approval before modifying files.

## Set Up a Minimal Workflow for a Repository

Prompt:

```text
给这个仓库建立一套极简的 AI 协作规范，既能让后续任务接上上下文，又不要制造一堆过程文档。
```

Expected result:

- Create a compact `AGENTS.md` with real commands, boundaries, and two-tier cadence.
- Create `docs/project-state.md` (current factual snapshot, hard cap <= 150 lines / 12 KB) and `docs/TODO.md` (active work only, delete completed lines, <= 120 lines / 10 KB).
- Add a single-file spec template `docs/specs/_template.md` for larger changes.
- Add a lightweight check script enforcing required entry files, size limits, and live relative links.

## Choose Between Direct Change and Single-File Spec

- For a bug fix, copy tweak, styling adjustment, small config change, or single-module small task: go straight to **Direct Change** — inspect code, implement, verify, and record via a clear semantic Git commit. Do not write a spec or dev-log.
- For cross-module contract updates, schema migrations, permission/state-machine refactors, or multi-module features: write **one** concise spec under `docs/specs/YYYY-MM-DD-<topic>.md`, confirm boundaries and verification criteria, then implement.

## Maintain `project-state.md` Without Bloat

Overwrite stale lines instead of appending chronological logs.

Update `docs/project-state.md` when:

- Environments, deployment architecture, or core runnable modules change.
- Long-term technical invariants or contract boundaries change.
- Known limitations or unresolved pitfalls are added or resolved.

Do not update `docs/project-state.md` for:

- Routine bug fixes or single-task implementation details.
- Per-run test counts, command transcripts, or commit-by-commit changelogs.
- Completed short-lived tasks (delete them from `docs/TODO.md` and rely on Git history).
