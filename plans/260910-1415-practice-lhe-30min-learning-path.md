# 30-Minute Learning Path: practice-lhe

Basis: session repo scan + repomix pack (`output/practice-lhe-pack.txt`). Files verified on disk.
practice-lhe = walkinglabs/learn-harness-engineering checkout: project-based course on AI coding-agent harnesses.

## Reading Order (25 min)

### 1. `practice-lhe/README.md` — 5 min
Read only: "What Harness Engineering Actually Means" → "Quick Start: Improve Your Agent Today" → "Syllabus".
Skip: badge rows, What's New, Visual Preview.
Look for:
- Course claim: harness = 5 subsystems (instructions, state, verification, scope, lifecycle)
- Project progression 01→06 (basic app → agent-architecture variants → perf)
- Pointer to `skills/harness-creator/` as the actionable distillation

### 2. `practice-lhe/skills/harness-creator/SKILL.md` — 8 min (core)
Look for:
- 5-subsystem table — the whole course compressed:
  - Instructions → `AGENTS.md`/`CLAUDE.md`
  - State → `feature_list.json`, `progress.md`
  - Verification → `init.sh` / documented commands
  - Scope → feature deps + done criteria
  - Lifecycle → `session-handoff.md`, end-of-session routine
- "First Move" procedure (inspect → ask only non-inferable context)

### 3. `practice-lhe/projects/project-01/README.md` + starter harness — 5 min
Files: `README.md`, `starter/CLAUDE.md`, `starter/feature_list.json`, `starter/init.sh`
Look for:
- Each file = one subsystem row made real
- Starter vs `solution/`: how feature states + progress.md differ

### 4. project-01 starter code skim — 7 min
Order: `src/main/main.ts` → `src/main/ipc-handlers.ts` → `src/services/qa-service.ts` → `src/renderer/App.tsx`
Look for:
- Electron 3-process split: main / preload / renderer
- IPC boundary (renderer → preload → ipc-handlers)
- Business logic in `src/services/` (document, indexing, persistence, qa); `src/shared/types.ts` = contract
- App is just the vehicle; harness files around it = the actual course subject

## Hands-On Exercise (5 min)

```bash
cd practice-lhe
bash tools/audit-harness.sh projects/project-01/solution
bash tools/audit-harness.sh projects/project-01/starter
```

- Zero dependencies (pure bash), exit 0 = all CRITICAL pass
- Compare the two runs: which CRITICAL/RECOMMENDED items differ
- Map every audit section back to one of the 5 subsystems

## Done Check

Name all 5 subsystems + minimal artifact for each, without looking.
