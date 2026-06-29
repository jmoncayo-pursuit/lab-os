# Backlog

Raw ideas and shaped work for this fork of the CAMELS Lab Handbook. Items arrive via the workflow on
the [Planning surface](site/docs/planning/backlog.md) page; each follows the shape in
[`templates/backlog-item.template.md`](templates/backlog-item.template.md).

Read the **Index** first - it is the "what is ready right now" view. The full items follow below it.

## Index

| id | title | size | status |
|---|---|---|---|
| B1 | "Edit this page" resolves to my fork | S | done |
| B2 | A CAMELS glossary page in the handbook | M | ready |
| B3 | Printable "first session" checklist | S | ready |

## Inbox

<!-- Raw, unshaped ideas. Promote one to Items once it has a Problem and a single Done-when. -->

- A short screen recording of the workspace bootstrap, linked from Getting Started.
- A "what changed upstream" page that diffs my fork against `CAMELS-Research-Group/lab-os`.

## Items

## B1 - "Edit this page" resolves to my fork

- **Problem:** the inherited handbook pointed "Edit this page" and the deploy URL at the upstream, so edits and the published site belonged to someone else.
- **Who it helps:** anyone who reads my handbook and wants to propose a fix from the rendered page.
- **Value:** closes the loop from reading to contributing, and makes the deploy unambiguously mine.
- **Rough size:** S - one sitting.
- **Done when:** `cd site && npm run build` is green and no `WatsonWBlair` literal remains in `site/docusaurus.config.ts`.
- **Depends on:** -
- **Status:** done <!-- this is what Task 1 of the sample plan delivers -->

## B2 - A CAMELS glossary page in the handbook

- **Problem:** the handbook uses lab-specific terms (Stage E, latent space, APE) with no single place that defines them, so a new reader has to infer meanings from context.
- **Who it helps:** newcomers onboarding into the CAMELS line who do not yet share the vocabulary.
- **Value:** lowers the cost of the first read; one owning doc for terms keeps definitions single-sourced.
- **Rough size:** M - a few sittings (collect the terms, write the entries, wire the sidebar).
- **Done when:** the built site serves a `/docs/glossary` page that defines at least the terms used on the front page, and the build is green.
- **Depends on:** -
- **Status:** ready

## B3 - Printable "first session" checklist

- **Problem:** a first-time participant has no one-page artifact to follow while bootstrapping the workspace; the steps are spread across several pages.
- **Who it helps:** anyone running their very first session, away from the screen they set up on.
- **Value:** a small, high-leverage convenience that reduces setup mistakes.
- **Rough size:** S - one sitting.
- **Done when:** a single printable page exists in the handbook whose steps a reader can tick through without opening another tab.
- **Depends on:** -
- **Status:** ready
