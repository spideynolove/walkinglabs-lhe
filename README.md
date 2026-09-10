# walkinglabs-lhe

Practice workspace for hands-on harness engineering, source-code exploration, and Claude Code/Codex workflow experiments.

This repository is not the upstream course and not a product implementation. It is a small tracked control layer around local, mostly ignored working materials.

## Purpose

- Explore harness engineering materials, especially `https://github.com/walkinglabs/learn-harness-engineering`
- Use `repomix` to summarize and inspect external source trees
- Practice Claude Code and Codex workflows on bounded tasks
- Keep local ClaudeKit templates available without forcing every review to ingest them

## Current Layout

Tracked files are intentionally minimal:

- `README.md`: project purpose and workflow
- `AGENTS.md`: instructions for Codex/OpenCode-style agents
- `CLAUDE.md`: instructions for Claude Code
- `.gitignore`: keeps copied templates, generated outputs, and research material out of git-backed review context
- `plans/.gitignore`: ignores generated ClaudeKit plans and reports

Ignored folders such as `.claude`, `.agents`, `docs`, `guide`, `scripts`, `data`, `output`, `materials`, and `main` may still exist locally. They are available for direct reading when needed, but they are not part of normal git diffs or Codex review input.

## Git Ignore Policy

`.gitignore` only affects git tracking and tools that build context from git state. It does not stop an AI agent from reading a file if the user or task explicitly points to it.

Use ignored folders for large copied templates, generated analysis, repomix outputs, and upstream checkouts. Move a file out of ignored paths or force-add it only when it becomes part of this repository's durable workflow.

## ClaudeKit Use

ClaudeKit is useful here as a local toolset, not as source code to review. Prefer the official CLI flow when refreshing it:

```bash
ck init
ck migrate --dry-run
```

Use `.claude/.ckignore` for ClaudeKit/LLM context trimming. Use `.gitignore` for git and Codex review trimming.

`plans/reports` is treated as generated research output. Keep it ignored unless a specific report becomes important project documentation.

## Working Pattern

1. Put external repos, repomix output, and scratch data under ignored folders.
2. Ask the agent to inspect specific files or directories by path.
3. Use Codex review only on small tracked changes or focused diffs.
4. Keep permanent workflow decisions in `README.md`, `AGENTS.md`, or `CLAUDE.md`.

For Codex adversarial review, always provide focus text:

```text
/codex:adversarial-review --background focus only on README.md, AGENTS.md, and CLAUDE.md workflow clarity
```
