---
title: First session checklist
description: A printable, self-contained checklist for the first-session bootstrap - every step carries its command, no other tab needed.
---

# First session checklist

Print this page (Ctrl/Cmd+P) - every step carries its command, so you can tick through without opening another tab.

> **Reading the commands:** blocks titled **Terminal** run in your OS terminal;
> blocks titled **Claude session** are typed into an active Claude Code session.

## Before you start

- [ ] Prerequisites in place: a Claude subscription (Pro or Max), Git, GitHub CLI (`gh`), and a GitHub account (no account: use the clone fallback below)
- [ ] Install Claude Code: `npm install -g @anthropic-ai/claude-code` (other installers: [docs.claude.com/en/docs/claude-code/setup](https://docs.claude.com/en/docs/claude-code/setup)); confirm with `claude --version`, then run `claude` once and log in
- [ ] Pick your `<DEV_ROOT>` and use it consistently: `~/Development/lab-os` (macOS/Linux) or `C:\Users\<you>\Development\lab-os` (Windows)

## Set up the workspace

The guided path is one paste: the bootstrap prompt on [Getting Started](/docs/getting-started) has Claude interview you and perform these same steps, confirming before anything is forked, cloned, deleted, moved, or overwritten. The steps below are that work, one command at a time.

- [ ] Fork and clone into `<DEV_ROOT>` (origin = your fork, upstream = the source):

  ```bash title="Terminal"
  gh repo fork CAMELS-Research-Group/lab-os --clone -- <DEV_ROOT>
  ```

  No GitHub account? Fall back to:

  ```bash title="Terminal"
  git clone https://github.com/CAMELS-Research-Group/lab-os.git <DEV_ROOT>
  git -C <DEV_ROOT> remote add upstream https://github.com/CAMELS-Research-Group/lab-os.git
  ```

- [ ] Global config: fill `<DEV_ROOT>/templates/global-CLAUDE.template.md` into `~/.claude/CLAUDE.md` (Windows: `C:\Users\<you>\.claude\CLAUDE.md`); if one already exists, merge - never silently overwrite
- [ ] Dev-root map: create `<DEV_ROOT>/.claude/CLAUDE.md` from `<DEV_ROOT>/templates/dev-root-CLAUDE.template.md`, adjusting paths (the rules already live at `<DEV_ROOT>/.claude/rules`; `git pull upstream main` keeps them current)
- [ ] Make the fork yours: reset `project_log.md` from `templates/project_log.template.md`; remove `docs/superpowers/specs/` and `site/`; replace `README.md` with a short dev-home note keeping a one-line upstream pointer; stage the cleanup on a branch
- [ ] Re-home your plan into `<DEV_ROOT>/_plans/`; nest any existing codebase at `<DEV_ROOT>/<project>/` as its own git repo and add `/<project>/` to `<DEV_ROOT>/.gitignore` (no code yet: skip the nesting)
- [ ] Install the plugins:

  ```text title="Claude session"
  /plugin marketplace add WatsonWBlair/lab-claude-plugins
  /plugin install pr-review-loop@lab-claude-plugins
  /plugin install superpowers@claude-plugins-official
  ```

## Verify

- [ ] `git -C <DEV_ROOT> remote -v` shows origin = your fork, upstream = `CAMELS-Research-Group/lab-os` (clone fallback: origin and upstream both = `CAMELS-Research-Group/lab-os`)
- [ ] `<DEV_ROOT>/.claude/rules` lists the rule files (`01-workflow.md`, `02-data-protection.md`, ...)
- [ ] `~/.claude/CLAUDE.md` and `<DEV_ROOT>/.claude/CLAUDE.md` exist with no `<...>` placeholders
- [ ] `project_log.md` is the fresh stub; `site/` and `docs/superpowers/specs/` are gone; your plan is in `_plans/`
- [ ] `/plugin` lists `pr-review-loop@lab-claude-plugins` and `superpowers@claude-plugins-official`
- [ ] Smoke-test the rules: in a fresh Claude Code session at `<DEV_ROOT>`, ask "what are the lab's commit-message rules?" - the answer should come from `01-workflow.md` (`feat:`, `fix:`, lowercase subject); if not, confirm the session was opened within `<DEV_ROOT>`

## First project repo

- [ ] Create the repository and clone it into `<DEV_ROOT>` alongside the other repos: `gh repo create <name> --private --clone` (your own account for the onboarding sandbox)
- [ ] Add a `.gitignore` for your stack covering `.env` and other secret-bearing files, model artifacts (`.pt`, `.npy`, `.task`, `.onnx`, `.bin`, `.safetensors`), and anything derived from gated datasets
- [ ] Seed `CLAUDE.md` from `templates/repo-CLAUDE.template.md` at the repo root (or `.claude/CLAUDE.md`) and fill the placeholders - dense writing for an AI reader, 8 KB budget
- [ ] Seed `project_log.md` from `templates/project_log.template.md`, keeping the `## Standing Decisions` and `## Entries` headings exactly as shipped
- [ ] Copy lab-os's `.github/pull_request_template.md` into your repo's `.github/`, adjusting checklist items (skip the CI caller YAML - phase 2, not yet required)
- [ ] Make your first commit following the lab conventions (`feat:`, `fix:`, lowercase subject, under 72 characters)
