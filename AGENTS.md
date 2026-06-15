# AGENTS.md

> Instructions for coding agents (Codex, Claude Code, Hermes, etc.) working in the Phronesis repository.
>
> **Read this file in full before making any non-trivial change.**

## Project Context

**Phronesis** is a phone-first voice study companion for rigorous conversations about economic theory and recursive macroeconomic modeling. It began as a Brain Fart on 2026-06-14 and is now an active Tool Project.

- **GitHub:** https://github.com/Bonorinoa/Phronesis
- **Owner:** bonorinoa (Augusto Gonzalez Bonorino)
- **Status:** Design-ready / implementation-pending
- **Initial use case:** Macroeconomics qualifier preparation (retake July 31, 2026)
- **Working name origin:** Greek *φρόνησις* — practical wisdom

## Required Reading Before Coding

Before implementing anything, read **at minimum** these documents in `docs/`:

1. [`docs/00_README.md`](./docs/00_README.md) — Canonical project entry point
2. [`docs/01_Project_Overview.md`](./docs/01_Project_Overview.md) — Vision, persona, requirements
3. [`docs/02_System_Architecture.md`](./docs/02_System_Architecture.md) — Components, data flow, state machine
4. [`docs/04_Tool_Specifications.md`](./docs/04_Tool_Specifications.md) — `create_math_object`, `retrieve_documents`, `update_memory`
5. [`docs/05_RAG_and_Ingestion.md`](./docs/05_RAG_and_Ingestion.md) — Document ingestion + retrieval
6. [`docs/06_Context_Management.md`](./docs/06_Context_Management.md) — Prompt structure, token budgets
7. [`docs/07_System_Prompt.md`](./docs/07_System_Prompt.md) — Agent behavior guidelines
8. [`docs/09_Vibe_Engineering_Workflow.md`](./docs/09_Vibe_Engineering_Workflow.md) — How to work
9. [`docs/14_Decision_Engineering_Log.md`](./docs/14_Decision_Engineering_Log.md) — Live decisions and rationale
10. [`docs/15_Design_Spec.md`](./docs/15_Design_Spec.md) — Aesthetic direction (Cool Kaffeehaus)

For visual reference, see [`docs/mockups/design_mockups.html`](./docs/mockups/design_mockups.html).

## Tech Stack (Locked)

| Layer | Tool | Notes |
|---|---|---|
| Frontend | Vercel (PWA) | Vercel AI SDK, mobile-first |
| Voice orchestrator | Pipecat on Modal | High control, custom pipeline |
| Reasoning LLM | MiniMax M3 via Ollama Cloud | Strong agentic + 1M context |
| TTS | MisoTTS on Modal | Open, hosted, 8B params |
| STT | Deepgram Nova-3 | Best real-time technical accuracy |
| RAG / Vector DB | Pinecone | Page-level chunks, 50k token cap |
| Observability | LangSmith | Trace inspection for vibe engineering |

## Design Direction (Locked)

**The Cool Kaffeehaus** — Viennese coffeehouse warmth + Nous Research restraint + Greek cultural alignment. All 6 design questions are locked as of 2026-06-14.

**Five-voice typography:** Fraunces (editorial), Source Serif 4 (reading), Cormorant Garamond (Greek/classical), Inter (working), JetBrains Mono (technical).

**Key aesthetic decisions:**
- Wordmark: `φphronesis` with the φ in oxblood
- Empty state: Hayek quote, *The Fatal Conceit* (1988)
- Page numbers and equation numbers: Greek letters (α, β, γ)
- System dividers: Greek-key meander pattern
- Footer microcopy: Greek transliterations (φιλοσοφία, διάλογος, σοφία)
- Dark mode: Espresso + brass, not Nous-blue

**Full design system:** [`docs/15_Design_Spec.md`](./docs/15_Design_Spec.md) — read this before writing any UI code.

## Core Tools (Implement First)

Three tools must work before anything else:

1. **`create_math_object`** — converts math expressions into `{spoken_text, display_text}`
2. **`retrieve_documents`** — returns raw pages from Pinecone within a 50k token cap
3. **`update_memory`** — stores high-signal memory entries

All three must be tested with MiniMax M3 before integrating voice.

## Conventions

### Project Structure
```
.
├── AGENTS.md                      # this file
├── README.md                      # forward-looking project overview
├── CHANGELOG.md                   # milestone log
├── LICENSE                        # Apache 2.0 (preserved from GitHub initial)
├── .env.example                   # required secrets
├── .gitignore
├── docs/                          # canonical design anchors (read these!)
│   ├── 00_README.md
│   ├── 01_Project_Overview.md
│   ├── 02_System_Architecture.md
│   ├── 03_Component_Design.md
│   ├── 04_Tool_Specifications.md
│   ├── 05_RAG_and_Ingestion.md
│   ├── 06_Context_Management.md
│   ├── 07_System_Prompt.md
│   ├── 08_Observability_and_Evaluation.md
│   ├── 09_Vibe_Engineering_Workflow.md
│   ├── 10_MVP_Scope_and_Development_Plan.md
│   ├── 11_Deployment_and_Hosting.md
│   ├── 12_Open_Questions_and_Future_Ideas.md
│   ├── 13_Glossary.md
│   ├── 14_Decision_Engineering_Log.md     # LIVE — update with every decision
│   ├── 15_Design_Spec.md                   # LOCKED v0.2
│   ├── PROJECT_MANIFEST.md
│   └── mockups/
│       └── design_mockups.html             # 5 phone mockups + tokens strip
└── (code will live in src/ or similar — to be created)
```

### Code Conventions
- **Language:** Python 3.11+ for backend, TypeScript for frontend
- **Package manager:** `uv` for Python (PEP 668), `pnpm` or `npm` for Node
- **Linting:** `ruff` (Python), `eslint` + `prettier` (TS)
- **Testing:** `pytest` for Python, `vitest` for TS
- **No commented-out code.** Remove it.
- **Type hints everywhere** in Python. Strict TypeScript.

### Commit Conventions
- **Conventional commits:** `feat:`, `fix:`, `docs:`, `chore:`, `refactor:`, `test:`
- **Small, atomic commits.** One logical change per commit.
- **Reference the doc** that drove the decision in the commit body when relevant.
- **Update `docs/14_Decision_Engineering_Log.md`** when making architectural decisions.

### Documentation Discipline
- The design docs in `docs/` are **canonical anchors**. Do not contradict them.
- If a doc needs to change, **update the doc and the decision log** in the same PR.
- Do not create new design docs without checking with the user first.
- New implementation docs (API references, runbooks, eval reports) go in `docs/` as numbered files.

## Build Order (Recommended)

Follow this order to keep risk low and feedback tight:

1. **Project scaffold** — Python venv, Modal CLI, Vercel CLI, dependency manifest
2. **Local ingestion script** — PDF → page-level chunks → Pinecone
3. **Retrieval tool** — `retrieve_documents` with metadata filters
4. **Math object tool** — `create_math_object` with verbalization rules
5. **Memory tool** — `update_memory` for high-signal entries
6. **MiniMax M3 API integration** — single agent, three tools, test in text mode
7. **Pipecat text loop** — WebSocket audio in, text out (skip TTS first)
8. **Deepgram STT integration** — wired into Pipecat
9. **MisoTTS service on Modal** — streaming TTS endpoint
10. **Vercel web frontend** — phone-first PWA, sticky voice button, page-based UI
11. **LangSmith tracing** — instrument the full flow
12. **End-to-end live test** — walk and talk

## Guardrails

These are **non-negotiable for MVP**:

- ❌ Do not build a native mobile app
- ❌ Do not add Google Drive sync until manual ingestion works
- ❌ Do not implement model routing (Grok 4.3 / Fusion) until single-model path is stable
- ❌ Do not build sophisticated context compaction until real sessions show the need
- ❌ Do not use Nous-Research blue for the dark mode (use espresso + brass)
- ❌ Do not read equations literally to TTS (always go through `create_math_object`)
- ❌ Do not violate the 50k retrieved context cap
- ❌ Do not retrieve documents when recent context is sufficient
- ❌ Do not emit "As an AI" disclaimers or emoji in chrome
- ❌ Do not add authentication, multi-user features, or sharing in MVP

## Working Style (Vibe Engineering)

- **Small, verifiable increments.** One component, one tool, one screen at a time.
- **Show your work.** Every tool call should produce a verifiable artifact (running code, passing test, rendered HTML).
- **Reference the docs.** When implementing, cite which doc section you are following.
- **Update the decision log.** Any architectural change goes in `docs/14_Decision_Engineering_Log.md`.
- **Inspect traces.** Use LangSmith to debug retrieval and tool calls.
- **Don't invent architecture.** If the docs do not cover a scenario, ask the user.
- **Match the aesthetic.** The Design Spec v0.2 is the source of truth. If you deviate, document why.

## What This Document Is Not

- **Not a feature spec.** See `docs/01_Project_Overview.md` and `docs/10_MVP_Scope_and_Development_Plan.md`.
- **Not a deployment guide.** See `docs/11_Deployment_and_Hosting.md`.
- **Not a system prompt.** See `docs/07_System_Prompt.md`.
- **Not a design system.** See `docs/15_Design_Spec.md` and `docs/mockups/`.

## Open Questions / Deferred Items

See `docs/12_Open_Questions_and_Future_Ideas.md` for the full list. Highlights:

- Google Drive sync (post-MVP)
- Native mobile app (post-MVP)
- Model routing across Grok 4.3 / MiniMax M3 / OpenRouter Fusion (post-MVP)
- Diagram generation in math objects (post-MVP, post-live-proof)
- Memory editing/deletion UI (low priority)
- Multi-mode memory stores (when Research mode is built)

## Verification Checklist (After Any Change)

- [ ] No new files outside the agreed structure
- [ ] Decision log updated if architecture changed
- [ ] Design spec consulted (and updated if it should change)
- [ ] Tests pass (`pytest`, `vitest`)
- [ ] Lint clean (`ruff`, `eslint`)
- [ ] Commit message follows conventional commits
- [ ] At least one runnable verification (test pass, manual smoke, screenshot)
- [ ] If user-facing: matches the Design Spec v0.2

## Emergency: Lost Context

If this file or the docs are unavailable:

1. **Read `docs/PROJECT_MANIFEST.md`** first.
2. **Then read `docs/00_README.md`** for orientation.
3. **Then read `docs/01_Project_Overview.md`** for the persona and requirements.
4. **Then read `docs/02_System_Architecture.md`** for the system shape.
5. **Then read `docs/15_Design_Spec.md`** before touching any UI.

Do not implement anything without first understanding:
- The persona (attentive, curious, rigorous, witty, challenging, knowledgeable tutor)
- The aesthetic (Cool Kaffeehaus — Viennese warmth + Nous restraint + Greek alignment)
- The core tools (`create_math_object`, `retrieve_documents`, `update_memory`)
- The 50k retrieved context cap
- The page-based UI model

---

*Last updated: 2026-06-14 — Phronesis v0.2 design locked, project ready for implementation*
