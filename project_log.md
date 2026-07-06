# lab-os — project log

Format: lab standard, `lab-os/.claude/rules/03-logging.md`. Skeleton per
`lab-os/templates/project_log.template.md` (normative — `log-lint` parses this structure).
The `## Standing Decisions` and `## Entries` headings are load-bearing lint anchors: exact
text, one each, never renamed. Entry headers are the only other `##` headings allowed.

## Standing Decisions

- 2026-07-03 14:43 — Loopback bind-pattern adopted as lab rule 05 · .claude/rules/05-network-boundaries.md
- 2026-06-23 07:51 — Plans track at the fork level; only project code nests · #44
- 2026-06-23 06:30 — Fork-of-lab-os is the default Claude-powered dev home · #43
- 2026-06-23 03:05 — Building sample plan ships as a facilitator-only fallback · #42
- 2026-06-19 05:58 — Workshop Program supersedes onboarding-project and one-day Building · #39
- 2026-06-13 15:00 — Handbook content rework gates tester launch · #25
- 2026-06-12 12:00 — Plan-execution logs close with their shipping PR · #18
- 2026-06-11 19:45 — Site owns human-facing docs · #15
- 2026-06-10 21:54 — Split the combined rule into 03-logging.md and 04-docs.md · #9
- 2026-06-10 17:45 — Adopt lab-wide logging & documentation standard · #6

## Entries

---

## 2026-07-03 14:43 — Loopback bind-pattern adopted as lab rule 05

**Decision:** Added `.claude/rules/05-network-boundaries.md`: every fleet/suite listener binds `127.0.0.1` explicitly (env-overridable, bare `listen(port)` is a defect), guards browser-facing routes against DNS rebinding with loopback-only CORS, adds auth before any side-effect route widens, and treats widening beyond loopback as a per-service logged decision. PR-template checklist line and rules-explained site section added with it.
**Why:** The 2026-07-03 fleet codebase audit found three services bound 0.0.0.0 while `~/.fleet/fleet-serve` already carried the correct pattern - drift, not ignorance. A rule the next service copies by default kills the class; the point fixes ride separately (t-cfdd2d, t-ddb958).
**Alternatives:** A STANDARDS.md line (no such file exists here) or folding into 01-workflow (wrong owner - this is a runtime boundary, not commit/PR mechanics); a new always-loaded 0x rule keeps it in every session's context at 1.9KB.
**Refs:** .claude/rules/05-network-boundaries.md, ~/Desktop/CAMELS/_plans/fleet-codebase-audit-2026-07-03.md, ~/.fleet/fleet-serve

---

## 2026-07-02 16:53 — Building exercise landed on main; handbook deployed to the fork's Pages

**Decision:** Merged `design/labos-org-sweep` (building-exercise + the CAMELS-Research-Group org-ref sweep + backlog items B2 glossary and B3 first-session checklist) into `main` (merge 19f7f03), pushed to origin, and deployed the site via the deploy-site workflow. First deploy failed because GitHub Pages was not enabled on the fork; enabled it (build_type workflow) and re-ran to green. Live and verified at https://jmoncayo-pursuit.github.io/lab-os/ - emerald palette in the served CSS with zero old-brand hexes, canonical org refs on getting-started, glossary and checklist pages serving. BACKLOG.md B1-B3 all done; the Building exercise is complete and this fork is now the working dev-home handbook.
**Why:** Jean's explicit go to finish the exercise and land it, so the fork stops being an exercise artifact and becomes the lab's usable front door.
**Refs:** merge 19f7f03, https://jmoncayo-pursuit.github.io/lab-os/, BACKLOG.md, docs/workshops/building/sample-plan.md

---

## 2026-06-30 12:46 — Handbook palette snapped to canonical suite emerald

**Decision:** Replaced the building-exercise teal (#0e7c66/#2eb98f) with the canonical suite emerald (#34d399/#10b981, the Design Agent's exact Infima ramp) on `building-exercise` (commit b231b11), per the lab decision 2026-06-29 20:35 (one design language across suite + handbook). The CAMELS C mark snaps to emerald too (emerald-700 tile for white-stroke legibility). Note: the Design Agent's `design/labos-emerald` applied the same paint but off bare main, dropping the re-home, branding, and planning surface - so the complete emerald state lives on this branch, not there.
**Why:** Suite and handbook must read as one design language for Watson visibility; applying the canon onto the full handbook keeps all the personalization.
**Refs:** commit b231b11, <DEV_ROOT>/project_log.md 2026-06-29 20:35, branch building-exercise

---

## 2026-06-29 19:38 — Building sample-plan run end-to-end on this fork

**Decision:** Ran the Building exercise (`docs/workshops/building/sample-plan.md`, Tasks 1-3) in a throwaway worktree on branch `building-exercise`, main checkout untouched - three commits: re-home identity (9b8ccc9), brand the handbook (f43647a), planning surface (7ef0649). Each task's one-command gate ran separately and unpiped, all green: T1 build + zero `WatsonWBlair|watsonwblair` in the config; T2 build + no `title: 'lab-os'` and no `#5b54e8`; T3 build + `BACKLOG.md`, `templates/backlog-item.template.md`, and `site/docs/planning/backlog.md` all present. Built site eyeballed light and dark - teal #0e7c66 palette, CAMELS mark, branded copy, Planning page wired into the sidebar. Local commits only; the push to origin is deferred to the fork owner.
**Why:** Demonstrate the prescribed onboarding is done on this fork, and rehearse the monitored/autonomous/scaling execution modes with verify-don't-trust: every diff read by hand, not taken from a self-report.
**Refs:** docs/workshops/building/sample-plan.md, branch building-exercise

---

## 2026-06-23 07:51 — Plans track at the fork level; only project code nests

**Decision:** Refines the plan/project homing of #43. Methodology artifacts track in the fork itself,
not a nested repo — the plan and backlog at `_plans/`, the dev-home project log at the fork root. Only
the project *code* is re-homed as a separate gitignored nested repo. #43 homed "the plan/project"
together in the nested repo, conflating two artifacts with different needs.
**Why:** The fork is the methodology/coordination home, and plans are methodology — matching how the
lab already works (the dev root tracks the backlog and plan packets, not per-project). #43's
anti-coupling reason — don't couple `git pull upstream` with project history — bites for a full
codebase, not a handful of plan files in a new path upstream never touches. Splitting keeps that
benefit for the code while a dev-home session sees every plan.
**Refs:** #44, site/docs/getting-started/index.mdx, site/docs/workshops/building/pre-flight.md, docs/workshops/program/design.md

---

## 2026-06-23 06:30 — Fork-of-lab-os is the default Claude-powered dev home

**Decision:** Onboarding now forks lab-os (clone fallback) and uses that fork as the participant's
primary dev home, replacing the clone-as-rules-subdir + junction model. Rules live natively in the
fork; `git pull upstream main` keeps them current. A light cleanup makes the fork their own (reset
project log, drop lab-os's own design history + handbook site). Bring-your-own-project is preserved:
the plan/project is re-homed as its own gitignored repo nested in the fork, keeping a clean history
and inheriting the rules. The junction model is retained as the documented multi-repo power-user path.
**Why:** A fork gives a personal, push-able copy (real PR target, upstream-syncable rules) and drops
the most failure-prone bootstrap step. Nesting the project as a separate gitignored repo recovers the
junction's one benefit — lab tooling kept separate from project work — without it.
**Alternatives:** Junction/multi-repo dev-root — retained as the power-user path, not the default.
Commit the project into the fork (monorepo) — rejected, couples upstream pulls with project history.
**Refs:** #43; #42 (sample plan remains the facilitator-only fallback, unchanged by this)

---

## 2026-06-23 03:05 — Building sample plan ships as a facilitator-only fallback

**Decision:** Added `docs/workshops/building/sample-plan.md` — a pre-baked three-task plan (re-home fork identity · brand the handbook · add a backlog/planning surface) that a participant who reaches Building without a plan of their own runs against their own fork. ENG-tier under `docs/`, not published to the site and not in the sidebar; participants point Claude at the file from their fork's CLI. The fork's `cd site && npm run build` (broken-link-throw) is the gate for all three tasks.
**Why:** The mixed-cohort Building kickoff has newcomers who finish setup with no execution-ready plan and so can't practise the three execution modes. A small real plan unblocks them. Kept non-published to hold the program's bring-your-own-project line ("no prescribed sample project") on the public surface — the fallback exists for the blocked without the handbook advertising a sample as the path. Realises the fallback-starter the 2026-06-19 program decision deferred.
**Alternatives:** Publish as a participant page — rejected, contradicts the no-prescribed-sample stance on the public site. Demo-only build by the facilitator, no participant plan — rejected, leaves newcomers watching instead of practising.
**Refs:** #42, docs/workshops/building/sample-plan.md, Development/_packets/lab-os/workshop-program/

---

## 2026-06-19 05:58 — Workshop Program supersedes onboarding-project and one-day Building

**Decision:** The three-part Workshop Program (Planning → Building → Closeout), published under `site/docs/workshops/`, supersedes the two-week onboarding-project sandbox (now a redirect stub into the program) and the standalone one-day Building-with-Claude material (absorbed into the Building part's exercises). Facilitator runbooks are internal under `docs/workshops/`, not published.
**Why:** One coherent bring-your-own-project arc on a single self-paced + live-facilitated handbook surface, instead of a scattered sandbox plus a one-day track that diverge and double the maintenance. Phase-0 design lock approved by Watson at the overnight-run launch.
**Refs:** #39, Development/_packets/lab-os/workshop-program/

---

## 2026-06-13 15:00 — Handbook content rework gates tester launch

**Decision:** The handbook content + IA is being reworked across all seven pages before testers
are invited; tester launch now waits on the rework. This supersedes the prior round's deferral —
page-content restructuring left to play-test friction data, with launch "unblocked" after the
chrome/IA round. The rework is decomposed: a backbone authoring-conventions round first, then
per-page rounds (Getting Started next).
**Why:** The deferral assumed the existing content was good enough for a first cohort and that
friction data should drive structural change. On review of the shipped site, the content needs
reframing (Working-with-Claude → SDD lifecycle; Onboarding Project → Onboarding Workshop), zero-tech
support, and terminal-vs-Claude command clarity before a tester runs the arc — gaps a cohort hits
immediately, not subtle friction worth waiting for.
**Alternatives:** Launch on current content, rework in parallel — rejected, testers would hit content
already judged inadequate. Partial gate (ship some, defer the reframes) — considered, rejected for a
clean gated rework.
**Refs:** #25, docs/superpowers/specs/2026-06-13-handbook-backbone-conventions-design.md, docs/superpowers/specs/2026-06-12-handbook-frontend-design-round-design.md

---

## 2026-06-12 12:00 — Plan-execution logs close with their shipping PR

**Decision:** A plan's `## Execution Log` closes with the PR that ships it. Post-merge
evidence (deploy green, runtime verification, branch cleanup) goes to a comment on that
PR; bigger facts route per the entry triggers. No trailing entries held for a future PR.
Watson granted a narrow standing pre-authorization (recorded in his global CLAUDE.md):
merge-closeout status comments on his own PRs post without per-action confirmation.
**Why:** The execution log lives in the repo, so merge-time facts always arrive after the
last commit that could carry them. Both prior closeouts hitched entries onto whatever PR
came next (#16 carried the tasks 4–13 closeout), coupling unrelated PRs and dangling when
no next PR exists. The routing table already sends bare status to PR comments — this names
when the log closes so closeout facts stop defaulting into it.
**Alternatives:** Dedicated one-line closeout PRs — rejected, noise against the
single-concern merge bar. Predictive pre-merge entries — rejected, evidence written before
it exists.
**Refs:** #18, docs/superpowers/specs/2026-06-10-logging-and-docs-standard-design.md

---

## 2026-06-11 19:45 — Site owns human-facing docs

**Decision:** The handbook site (`site/`, deployed to watsonwblair.github.io/lab-os) is the
owning home for human-facing docs. Root `BOOTSTRAP.md` and `WORKING-WITH-CLAUDE.md` become
pointer stubs to their site pages; `.claude/rules/` stay AI-tier repo files.
**Why:** Spec D3: one human-facing surface, written for its readers, with build-time link
checking — instead of agent-dense repo markdown doing double duty for stakeholders.
**Alternatives:** Site wraps the repo markdown unchanged — rejected, a brochure over a
codebase; site renders the repo markdown as-is — rejected, agent-dense prose shown to
stakeholders.
**Refs:** #15, docs/superpowers/specs/2026-06-11-lab-os-rename-handbook-site-design.md
