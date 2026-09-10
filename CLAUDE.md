# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Name:** walkinglabs-lhe
**Type:** AI-agent workflow practice workspace
**Description:** A local workspace for hands-on harness engineering practice, source-code exploration, and Claude Code/Codex workflow experiments.

This is not the upstream course repository and not a production application.

## Role & Responsibilities

Your role is to help inspect source material, summarize external repos, run bounded practice tasks, and keep this workspace useful without turning copied templates or generated research into review noise.

## Workflows

- Primary workflow: `./.claude/rules/primary-workflow.md`
- Development rules: `./.claude/rules/development-rules.md`
- Orchestration protocols: `./.claude/rules/orchestration-protocol.md`
- Documentation management: `./.claude/rules/documentation-management.md`
- And other workflows: `./.claude/rules/*`

**IMPORTANT:** Analyze the skills catalog and activate the skills that are needed for the task during the process.
**IMPORTANT:** You must follow strictly the development rules in `./.claude/rules/development-rules.md` file.
**IMPORTANT:** Before you plan or proceed any implementation, always read the `./README.md` file first to get context.
**IMPORTANT:** Sacrifice grammar for the sake of concision when writing reports.
**IMPORTANT:** In reports, list any unresolved questions at the end, if any.

## Hook Response Protocol

### Privacy Block Hook (`@@PRIVACY_PROMPT@@`)

When a tool call is blocked by the privacy-block hook, the output contains a JSON marker between `@@PRIVACY_PROMPT_START@@` and `@@PRIVACY_PROMPT_END@@`. **You MUST use the `AskUserQuestion` tool** to get proper user approval.

**Required Flow:**

1. Parse the JSON from the hook output
2. Use `AskUserQuestion` with the question data from the JSON
3. Based on user's selection:
   - **"Yes, approve access"** -> Use `bash cat "filepath"` to read the file
   - **"No, skip this file"** -> Continue without accessing the file

**Example AskUserQuestion call:**
```json
{
  "questions": [{
    "question": "I need to read \".env\" which may contain sensitive data. Do you approve?",
    "header": "File Access",
    "options": [
      { "label": "Yes, approve access", "description": "Allow reading .env this time" },
      { "label": "No, skip this file", "description": "Continue without accessing this file" }
    ],
    "multiSelect": false
  }]
}
```

**IMPORTANT:** Always ask the user via `AskUserQuestion` first. Never try to work around the privacy block without explicit user approval.

## Python Scripts (Skills)

When running Python scripts from `.claude/skills/`, use the venv Python interpreter:
- **Linux/macOS:** `.claude/skills/.venv/bin/python3 scripts/xxx.py`
- **Windows:** `.claude\skills\.venv\Scripts\python.exe scripts\xxx.py`

This ensures packages installed by `install.sh` are available.

**IMPORTANT:** When scripts of skills failed, don't stop, try to fix them directly.

## [IMPORTANT] Consider Modularization
- If a code file exceeds 200 lines of code, consider modularizing it
- Check existing modules before creating new
- Analyze logical separation boundaries
- Use kebab-case naming with long descriptive names when adding files
- After modularization, continue with main task
- When not to modularize: Markdown files, plain text files, bash scripts, configuration files, environment variables files, etc.

## Documentation Management

Keep durable project guidance in tracked root files first:

```
README.md
AGENTS.md
CLAUDE.md
```

Use ignored `docs` material as copied reference or generated research unless the user asks to promote a file into tracked documentation.

**IMPORTANT:** *MUST READ* and *MUST COMPLY* all *INSTRUCTIONS* in project `./CLAUDE.md`, especially *WORKFLOWS* section is *CRITICALLY IMPORTANT*, this rule is *MANDATORY. NON-NEGOTIABLE. NO EXCEPTIONS. MUST REMEMBER AT ALL TIMES!!!*

## Repository-Specific Purpose

Use this repo for immediate hands-on practice around harness engineering, especially `https://github.com/walkinglabs/learn-harness-engineering` when that is the active target.

Use `repomix` when the task is to understand a large external repository. Store large external checkouts, generated summaries, and scratch material under ignored folders such as `main`, `materials`, `data`, or `output`.

`.gitignore` affects git tracking and git-derived review context. It does not prevent Claude from reading ignored files when the task names them directly.

`.claude/.ckignore` affects ClaudeKit context collection. It does not affect git or Codex review unless a tool explicitly reads it.

Keep Codex review bounded to tracked changes or named files. Always add focus text to `/codex:adversarial-review`.

Treat `.claude`, `.agents`, `docs`, `guide`, `scripts`, and `plans` as local ClaudeKit or research material by default, not as application code. `plans/reports` is generated research history; read it only when asked about prior research or provenance.
