---
title: Glossary
description: Short definitions of the lab-specific terms used across this handbook - from agentic workspace to Stage E - each linked to the page that owns it.
---

# Glossary

Short definitions of the terms this handbook leans on, alphabetized; where a term has an owning page, the entry links it - that page is the source of truth.

### agentic development

Working with an AI that carries out tasks, not just answers questions. The front page calls the same thing agent-empowered development; the setup and workshops exist to make it the default way lab work happens. Owning page: [Getting Started](/docs/getting-started).

### agentic workspace

The setup that makes every session start from the same conventions: Claude Code, the persistent context files (the [CLAUDE.md](#claudemd) layers), the shared lab rules that load into every session, and two plugins. [Getting Started](/docs/getting-started) builds it in one Claude-guided paste.

### APE

The architecture line inside [LSCA](#lsca) - the model architecture the CAMELS latent-space work is built on.

### autonomous loop

An unattended Claude run - overnight or while you are away - under a safety contract: you wake to either an increment that passed the verification gate or a clean halt plus an actionable digest, never an unchecked finished feature. Halt contract, iteration caps, and a wall-clock kill are part of the mandate. Owning page: [Autonomous loops](/docs/working-with-claude/autonomous-loops).

### backlog

The lightweight front door to planning: a raw idea lands in `BACKLOG.md`'s Inbox, gets shaped into an item with a single checkable Done-when, then moves to Items with an Index row. An item is ready when its Done-when is one observable check. Owning page: [Planning surface](/docs/planning/backlog).

### CAMELS

Conversational Agents in Multimodal Embedded Latent Space - the research program the lab is organized around, run by the CAMELS Research Group. This handbook is that group's field guide to spec-driven, agent-empowered development.

### CI adherence checks

Three shared GitHub Actions checks lab-os defines once as reusable workflows, adoptable by any repo with one small caller file: `log-lint` validates project-log structure, `docs-budget` warns when always-loaded files exceed their byte budgets, and `merge-bar-check` verifies the PR description against the template. Owning page: [Tooling Tour](/docs/tooling-tour).

### Claude Code

Anthropic's AI coding assistant - the agent the lab's sessions run in, and the core of the agentic workspace. Install and login: [Getting Started](/docs/getting-started).

### CLAUDE.md

Instruction notes Claude reads automatically at the start of every session. The lab stacks three layers - global (who you are, how you work), dev-root (a map of your dev home), and per-repo (one project's details); every applicable layer loads, and when two disagree the most specific wins. Owning page: [Getting Started](/docs/getting-started).

### dev home (`<DEV_ROOT>`)

Your development home: the local clone of your lab-os fork (default `~/Development/lab-os`, or `C:\Users\<you>\Development\lab-os` on Windows). Your own projects live in their own git repos nested inside it, gitignored so their history never tangles with the upstream pull. Owning page: [Getting Started](/docs/getting-started).

### gate

A repo's designated verification command, run unpiped before every merge. A green gate proves the checks pass - not that every claimed guarantee is tested - so always re-run it yourself; piping hides the exit code and an agent's self-report is not evidence. Owning page: [Verify](/docs/working-with-claude/verify).

### gated dataset

A license-restricted human-subject dataset. Raw content, anything that could re-identify a participant, and unreviewed derived artifacts never enter a repo; which datasets count as gated is declared per-repo. Source of truth: [`02-data-protection.md`](https://github.com/CAMELS-Research-Group/lab-os/blob/main/.claude/rules/02-data-protection.md); tour: [The Rules, Explained](/docs/rules-explained).

### lab-os

The lab handbook repository and the cross-repo conventions it carries: the rules, templates, CI checks, and this site. Newcomers fork it as their development home, so the rules live natively in their workspace and `git pull upstream main` keeps them current. Repo: [CAMELS-Research-Group/lab-os](https://github.com/CAMELS-Research-Group/lab-os).

### lab rules

Four lab-wide rule files under `.claude/rules/` - workflow, data protection, logging, docs - that load into every Claude session and that the PR-review tooling reads at review time. lab-os owns the 0x-numbered files; per-repo rules number from 10 up and can extend or override them. Owning page: [The Rules, Explained](/docs/rules-explained).

### latent space

A learned representation space where a model encodes its inputs as coordinates, so similar things sit near each other. In [CAMELS](#camels) it is the shared multimodal embedded space: signals from more than one modality are embedded into a single space the conversational agents operate in.

### LSCA

The repository that is the current home of the [CAMELS](#camels) research line - the multimodal latent space, its architecture, and the training pipeline. It sits at the end of the lab's research lineage (SSUR_POC, Vibe_App, cs627, then LSCA).

### merge bar

The checklist a change must clear before merging: gate green and run unpiped, PR template complete, review findings resolved, log cleanup done, doc-sync triggers checked, single concern. Partly automated by the `merge-bar-check` CI job. Source of truth: [`01-workflow.md`](https://github.com/CAMELS-Research-Group/lab-os/blob/main/.claude/rules/01-workflow.md), Merge Bar.

### onboarding arc

The path a new member walks through the handbook: the landing page, the guided environment setup, the Working with Claude methods read, then a first brainstorm and spec on a sandbox project. The play-test protocol walks this same arc to stress-test the handbook - see [How to Play-Test](/docs/play-testing).

### play-testing

Stress-testing the handbook by walking the onboarding arc as if brand-new and filing a friction issue for every snag - friction is the data the lab wants. Includes the 15-minute stall rule: file the issue first, then ask for help. Owning page: [How to Play-Test](/docs/play-testing).

### plugins

Add-on capabilities for Claude Code installed during setup: `pr-review-loop` from the lab's plugin marketplace and `superpowers` from the official marketplace, whose process skills several lifecycle stages lean on. Install commands: [Getting Started](/docs/getting-started); marketplace details: [Tooling Tour](/docs/tooling-tour).

### PRD

Product requirements document - the living spec written before any non-trivial build: problem, success criteria, scope, constraints, plan, open questions. No code is written until sign-off, and silence is not approval. Owning page: [Working with Claude](/docs/working-with-claude).

### project log

The decision log each repo keeps at `project_log.md`: weighty decisions, irreversible or external events, and direction changes, each with the why, so a future session can pick the project up cold. Entries are immutable once merged, and the `log-lint` CI check parses the file's structure. Source of truth: [`03-logging.md`](https://github.com/CAMELS-Research-Group/lab-os/blob/main/.claude/rules/03-logging.md).

### sandbox project

A low-stakes, disposable project used as the learning vehicle for the onboarding arc - the front page's core skills get practiced by building it, in your own repo where mistakes are cheap. The [Workshop Program](/docs/workshops) instead runs on your own real project.

### spec-driven development (SDD)

Writing down what to build, and the plan to build it, before any code. The lab runs it as a seven-stage lifecycle with Claude - brainstorm, specify, plan, build, verify, review, close - with verify and review as the checkpoints where work earns the right to advance. Owning page: [Working with Claude](/docs/working-with-claude).

### Stage E

The reconstruction subsystem of the [CAMELS](#camels) pipeline - the stage that turns latent representations back into output signals. It currently spans the BlendshapeDecoder, the TTSProjector, and speaker-embedding targets.

### subagent

A helper AI agent that implementation is delegated to during the Build stage, rather than hand-coding everything in one session. Subagents discard context and return only their report, so each task's brief must stand alone; completion is git-authoritative - a task is done when the commit exists, not when the agent says so. Owning page: [Build](/docs/working-with-claude/build).

### workshop program

A three-part facilitated sequence - Planning, Building, Closeout - that takes one real project of your own from raw idea to retrospective, self-paced or as a live cohort. It superseded the earlier two-week onboarding project. Owning page: [Workshop Program](/docs/workshops/).

### workspace map

The dev-root [CLAUDE.md](#claudemd): the file that orients Claude to your workspace - which repos exist and how they relate. Seeded from [`templates/dev-root-CLAUDE.template.md`](https://github.com/CAMELS-Research-Group/lab-os/blob/main/templates/dev-root-CLAUDE.template.md) during setup ([Getting Started](/docs/getting-started)).
