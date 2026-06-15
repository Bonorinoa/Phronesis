# Phronesis

**Phronesis** is a phone-first voice study companion for rigorous conversations about economic theory and recursive macroeconomic modeling.

The aim is not to build a generic super-agent. Phronesis should feel like an unusually good intellectual friend or mentor: attentive, curious, rigorous, witty, challenging, and knowledgeable. The initial domain is macroeconomics qualifier preparation; the longer-term ambition is a tasteful conversational system for advanced technical learning and research ideation.

## Current Status

**Design-ready / implementation-pending.**

The first design pass is complete. The project knowledge base lives in [`docs/`](./docs/) and should be treated as the canonical anchor for coding agents and future implementation work.

## MVP Direction

The MVP should let the user open a phone web app, speak about a macroeconomics topic, and receive a natural spoken response that is grounded in uploaded documents when needed.

### Core Stack

| Layer | Choice |
|---|---|
| Frontend | Vercel web app / PWA |
| Voice orchestration | Pipecat on Modal |
| Reasoning model | MiniMax M3 via Ollama Cloud |
| Text-to-speech | MisoTTS on Modal |
| Speech-to-text | Deepgram Nova-3 |
| Retrieval / memory | Pinecone |
| Observability | LangSmith |

## High-Level Roadmap to MVP

### 1. Project Grounding

- Maintain the design docs in [`docs/`](./docs/)
- Create `AGENTS.md` after discussing coding-agent conventions
- Keep the decision/engineering log updated

### 2. Data and Retrieval Foundation

- Build local PDF ingestion for qualifier exams, lecture notes, and textbooks
- Use full-page chunks with lightweight cleaning
- Store page-level chunks and metadata in Pinecone
- Implement and test the `retrieve_documents` tool

### 3. Agent Core

- Integrate MiniMax M3 via Ollama Cloud
- Implement the core tools:
  - `retrieve_documents`
  - `create_math_object`
  - `update_memory`
- Add initial system prompt and context manager

### 4. Voice Pipeline

- Implement Pipecat orchestration on Modal
- Add Deepgram Nova-3 for STT
- Host MisoTTS on Modal for natural voice output
- Verify end-to-end text → speech → response flow

### 5. Web App

- Build a minimal, beautiful Vercel PWA
- Support voice input/output
- Display session state: listening, thinking, retrieving, speaking
- Display math objects visually while speaking them naturally

### 6. Observability and Live Testing

- Add LangSmith traces
- Track tool calls, retrieval decisions, latency, token usage, and cost
- Run live study sessions
- Iterate based on traces and actual use

## Documentation Map

Start here:

- [`docs/PROJECT_MANIFEST.md`](./docs/PROJECT_MANIFEST.md)
- [`docs/01_Project_Overview.md`](./docs/01_Project_Overview.md)
- [`docs/02_System_Architecture.md`](./docs/02_System_Architecture.md)
- [`docs/04_Tool_Specifications.md`](./docs/04_Tool_Specifications.md)
- [`docs/05_RAG_and_Ingestion.md`](./docs/05_RAG_and_Ingestion.md)
- [`docs/09_Vibe_Engineering_Workflow.md`](./docs/09_Vibe_Engineering_Workflow.md)
- [`docs/14_Decision_Engineering_Log.md`](./docs/14_Decision_Engineering_Log.md)

## Guardrails

- No native mobile app for MVP.
- No Google Drive sync until manual ingestion works.
- No model routing until the single-model path is stable.
- No sophisticated context compaction until real sessions show it is necessary.
- `AGENTS.md` is intentionally absent until coding-agent conventions are discussed.
