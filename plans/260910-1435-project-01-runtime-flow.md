# project-01 Runtime + Harness Flow (verified, exact paths)

Base: `practice-lhe/projects/project-01/starter`. All line refs from source read 2026-09-10.

## Boot chain (what runs first)

```
npm run dev                       (package.json scripts.dev)
└─ scripts/dev.js                 3 execSync steps, aborts on failure
   1. npx tsc -p tsconfig.node.json   → dist/main/main.js + dist/preload/preload.js
   2. npx vite build                  → bundles src/renderer/index.html → dist/renderer
   3. npx electron .                  → reads package.json "main": dist/main/main.js
```

## Electron main wiring (src/main/main.ts)

Module scope, before `app.whenReady()`:
1. `dataDir = userData/knowledge-base-data` (main.ts:39)
2. `new PersistenceService(dataDir)` (:40)
3. `new DocumentService(persistence)` (:41)
4. `new IndexingService(persistence)` (:42)
5. `new QaService(persistence, indexingService?)` (:43)
6. `registerIpcHandlers(ipcMain, {documentService, indexingService, qaService})` (:45)
7. `whenReady` → BrowserWindow (contextIsolation=true, nodeIntegration=false, preload=dist/preload/preload.js)

## IPC boundary (single source of truth: src/shared/types.ts:47 `IPC_CHANNELS`)

9 channels, each `ipcMain.handle` in src/main/ipc-handlers.ts → service method:
- documents: LIST / IMPORT / GET / DELETE
- indexing: START / STATUS / CHUNKS
- qa: ASK_QUESTION / GET_HISTORY

## Preload bridge (src/preload/preload.ts)

`contextBridge.exposeInMainWorld('knowledgeBase', api)` (:22) — namespaced API (`documents.*`, `indexing.*`, `qa.*`), 1:1 with channels. Renderer types: src/renderer/types.d.ts.

## Renderer (src/renderer/)

`main.tsx` → `createRoot(#root).render(<App/>)` → `App.tsx` calls `window.knowledgeBase.*`; UI parts in `components/{ImportPanel,DocumentList,DocumentDetail,QuestionPanel,StatusBar}.tsx`.

## Services (src/services/) — where logic lives

- `persistence-service.ts` — fs wrapper, subdirs (data/documents/index), JSON store
- `document-service.ts` — import = copy + extract + metadata; list/get/delete
- `indexing-service.ts` — chunking, status
- `qa-service.ts` — domain core. NOTE: canned answers (:15-20), fake latency `setTimeout(100+rand*400)` (:52), no-docs fallback (:127). Simulated QA, no LLM.

## Where to modify behavior

| Change | File |
|---|---|
| Q&A behavior | `src/services/qa-service.ts` (replace canned answers/latency) |
| New IPC command | `src/shared/types.ts` (channel) → `src/main/ipc-handlers.ts` (handler) → `src/preload/preload.ts` (api) → `src/renderer/types.d.ts` |
| UI | `src/renderer/App.tsx` + `components/*` |
| Service wiring, window, data dir | `src/main/main.ts` |
| Storage layout | `src/services/persistence-service.ts` |
| Build/dev pipeline | `scripts/dev.js`, `vite.config.ts`, tsconfigs |
| Verification | `package.json` scripts — starter has ZERO test files, `npm test` finds nothing |

## starter vs solution (settled)

- solution = simulated agent output: `claude-progress.md` session log in agent voice; app backend byte-identical to starter; delta = 7 harness artifacts (AGENTS.md, CLAUDE.md, feature_list.json, init.sh, claude-progress.md, docs/PRODUCT.md, docs/ARCHITECTURE.md) + cosmetic renderer polish.
- Practice in starter. LEARN from solution — it is the only complete harness instance in p01. Ignoring it discards the answer key.
- Starter lacks the verification gate entirely (`npm test` = no test files) — building starter's own init.sh + feature_list.json IS the assignment.
