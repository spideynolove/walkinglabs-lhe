# AGENTS.md

This file provides guidance to Codex, OpenCode, and other `AGENTS.md` readers when working in this repository.

## Project Overview

**Name:** walkinglabs-lhe
**Type:** AI-agent workflow practice workspace
**Description:** A local workspace for hands-on harness engineering practice, source-code exploration, and Claude Code/Codex workflow experiments.

This is not the upstream course repository and not a production application.

## Role & Responsibilities

Your role is to help inspect source material, summarize external repos, run bounded practice tasks, and keep this workspace useful without turning copied templates or generated research into review noise.

## Default Workflow

- Read `README.md` before planning or editing.
- Keep changes small and practical.
- Prefer direct file inspection over broad repo packing.
- Use `repomix` for external repo summaries when the user asks to understand a large source tree.
- Use git-backed Codex review only for tracked files or small focused diffs.
- When running adversarial review, include focus text.
- Do not review all ignored ClaudeKit template folders by default.

## Workflows

- Primary workflow: `./.claude/rules/primary-workflow.md`
- Development rules: `./.claude/rules/development-rules.md`
- Orchestration protocols: `./.claude/rules/orchestration-protocol.md`
- Documentation management: `./.claude/rules/documentation-management.md`
- And other workflows: `./.claude/rules/*`

**IMPORTANT:** Analyze the skills catalog and activate the skills that are needed for the task during the process.
**IMPORTANT:** Before you plan or proceed any implementation, always read the `./README.md` file first to get context.
**IMPORTANT:** Sacrifice grammar for the sake of concision when writing reports.
**IMPORTANT:** In reports, list any unresolved questions at the end, if any.

## Development Principles

- **YAGNI**: avoid over-engineering
- **KISS**: prefer simple solutions
- **DRY**: eliminate real duplication

## Context Rules

`.gitignore` limits git tracking and git-derived review context. It does not block direct file reads.

`.claude/.ckignore` limits ClaudeKit context collection. It does not control git.

Ignored folders can be read when directly relevant:

- `.claude`
- `.agents`
- `docs`
- `guide`
- `scripts`
- `plans`
- `data`
- `output`
- `materials`
- `main`

## ClaudeKit

ClaudeKit content in this repo is a local harness/tooling template. Use it when practicing Claude Code workflows or when the user explicitly asks about ClaudeKit behavior.

Prefer official ClaudeKit CLI commands for refresh or migration checks:

```bash
ck init
ck migrate --dry-run
ck doctor
```

## Coding Rules

- Minimal code only.
- No speculative abstractions.
- No docstrings or comments in code.
- Use existing files and patterns before adding new ones.
- For Python commands, run `source /home/hung/env/.venv/bin/activate` first.
- Install Python packages with `uv pip install`.

## Reports

Keep reports short. Put unresolved questions at the end only when they matter.

## Repository-Specific Purpose

Use this repo for immediate hands-on practice around harness engineering, especially `https://github.com/walkinglabs/learn-harness-engineering` when that is the active target.

Use ignored folders for copied templates, repomix outputs, generated reports, external checkouts, and scratch material. These paths remain readable when named directly, but they should not be assumed to be part of the review target.

`plans/reports` is generated research history. Read it only when the user asks about prior research or ClaudeKit provenance.
