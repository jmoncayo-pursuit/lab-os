# Development root — CAMELS Research Group workspace orientation

Working from the workspace root (`~/Development/lab-os`), not just inside a single repo, is
intentional — it's where cross-project coordination happens: multi-repo planning, workspace-wide
tooling and rules, cross-repo logs. Per-repo `CLAUDE.md` cascades when a session works inside a
sub-project; the broader view stays available.

This dev home **is** my fork of lab-os (`~/Development/lab-os`): the lab `.claude/rules/` live here
natively — no symlink to manage — and `git pull upstream main` pulls rule updates from the source.
My own project repos nest inside as their own git repos, gitignored from the fork.

## Project lineage

> Confirm/extend — inferred from the global `CLAUDE.md`, not verified here.

1. **`mission-control`** — subagent-driven-development practice project; where agentic workflow habits
   are built before applying them to research code.
2. **`LSCA`** — current primary work: Stage E reconstruction (BlendshapeDecoder, TTSProjector,
   speaker-embedding targets). See `LSCA/CLAUDE.md` for project specifics once nested.

When a "why this design?" or "where does X come from?" question lands, check upstream in this chain
before assuming the answer is new.

## Active or foundational repos

> None are nested under `~/Development/lab-os` yet — this dev home currently holds only the fork
> itself. Nest each as its own gitignored git repo here when work moves in.

| Repo | Role | Status |
|---|---|---|
| `LSCA` | Stage E reconstruction subsystem (BlendshapeDecoder, TTSProjector, speaker-embedding targets); PRs #289 / #302 | Active — Stage E |
| `mission-control` | Subagent-driven-development practice project | Active |
| `Global_Pathways` | Neighbor project | Reference / on demand |

## Tooling

Shared tooling wired in during setup:

- **`lab-os`** — the spec-driven-development conventions. This dev home **is** my fork of lab-os, so
  its `.claude/rules/` live here natively; `git pull upstream main` pulls rule updates from the
  source. Treat these as **starting standards** — adapt or extend as project needs diverge.
  Origin: `github.com/jmoncayo-pursuit/lab-os` (fork) · upstream:
  `github.com/CAMELS-Research-Group/lab-os`.
- **`lab-claude-plugins`** — Claude Code plugins (e.g. `pr-review-loop`) via the lab plugin
  marketplace. Source-of-truth: `github.com/WatsonWBlair/lab-claude-plugins`.
- **`superpowers`** — workflow plugins from the official Claude Code marketplace (brainstorming,
  planning, TDD, subagent-driven execution).

As repos are nested here, list them above so a session at `~/Development/lab-os` sees the whole
workspace.

## Logs and tracking

- **Plans / backlog:** `~/Development/lab-os/_plans/` — tracked by the fork, alongside the rules and log
- **Per-repo logs:** `<repo>/project_log.md`
- **Workspace-level decisions** (cross-repo tooling, infra, workspace-wide conventions):
  `~/Development/lab-os/project_log.md`
- **Cost tracking** (inference spend, infra): `~/Development/lab-os/cost-tracking.md`

Entry format and triggers are defined in the global `~/.claude/CLAUDE.md` and in
`.claude/rules/03-logging.md`.

## Approval gates

Defined in the global `~/.claude/CLAUDE.md`. Cross-cutting items at this level:

- External-facing posts (PRs, issue comments, anything under your name; bot identity OK, user identity not)
- Cloud spend above the stated ceiling; no paid add-ons without approval
- Data exposure risks (raw gated/sensitive data; derived artifacts need PII review per
  `.claude/rules/02-data-protection.md`)
- Destructive operations on shared state
