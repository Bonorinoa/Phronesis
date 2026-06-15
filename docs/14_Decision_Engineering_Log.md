# Decision and Engineering Log

This is a live document. Update it whenever project direction, implementation details, or important lessons change.

## 2026-06-14 — Brain Fart Graduated

The initial idea began as a Brain Fart about building a specialized voice application for macroeconomics qualifier preparation. It has now graduated into the active Tool Project **Phronesis**.

Rationale:
- Strong personal resonance
- Clear time-bound use case (macro qualifier retake)
- Generalizable beyond exam prep
- Requires real system design and implementation

## 2026-06-14 — Name Selected: Phronesis

The name **Phronesis** was chosen for its meaning: practical wisdom and judgment applied to real situations.

It fits the desired persona: attentive, curious, rigorous, witty, challenging, and knowledgeable.

## 2026-06-14 — Core Stack Decisions

| Component | Decision |
|---|---|
| Frontend | Vercel web app / PWA |
| Orchestrator | Pipecat on Modal |
| LLM | MiniMax M3 via Ollama Cloud |
| TTS | MisoTTS on Modal |
| STT | Deepgram Nova-3 |
| RAG | Pinecone |
| Observability | LangSmith |

## 2026-06-14 — Retrieval Strategy

Decision:
- Own ingestion and retrieval logic.
- Use Pinecone as vector DB.
- Full-page chunks.
- Agent decides when to retrieve.
- One retrieval query plus optional follow-up.
- Hard 50k token cap for retrieved context.

Rationale:
- Long-context LLM makes larger chunks sensible.
- Metadata can do significant retrieval work.
- Simpler than parallel multi-query retrieval.

## 2026-06-14 — Math Handling Strategy

Decision:
- Implement `create_math_object` tool.
- Always verbalize math for speech.
- Always display math visually/textually.

Rationale:
- TTS models do not understand math.
- The LLM/tool layer must transform math into precise natural speech.

## 2026-06-14 — Memory Strategy

Decision:
- Agent-driven extraction.
- Start with a single shared memory.
- Store high-signal pain points, breakthroughs, preferences, and progress.

Rationale:
- Avoid over-engineering.
- Mode-specific memory can come later.

## 2026-06-14 — Git Repository Initialized and Pushed

Decision:
- Initialized `~/Hermes/Projects/Phronesis` as a local git repository.
- User manually created GitHub remote at `https://github.com/Bonorinoa/Phronesis.git`.
- Added project-readiness files: `.gitignore`, `.env.example`, `README.md`, `CHANGELOG.md`, and `docs/README.md`.
- Merged remote initial commit containing `LICENSE` and `.gitignore`.
- Preserved the remote `LICENSE`.
- Moved canonical design documents into `docs/`.
- Rewrote root `README.md` as a forward-looking project overview and MVP roadmap.

Rationale:
- The folder is now ready for version-controlled implementation.
- Root docs are kept clean while `docs/` contains the canonical design anchor suite.
- `AGENTS.md` remains intentionally absent until coding-agent conventions are discussed.

## Open Engineering Notes

- Need to test MisoTTS on Modal latency and quality.
- Need to test MiniMax M3 tool use with our custom tools.
- Need to validate Deepgram on economics terminology.
- Need to decide exact PDF parser and embedding model during implementation.
- Need to design `AGENTS.md` before handing the repo to coding agents.
