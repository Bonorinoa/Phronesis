# MVP Scope and Development Plan

## MVP Objective

Create a working phone-first web application that supports grounded voice tutoring for macroeconomics qualifier preparation.

## MVP Must-Haves

- Phone-accessible web app
- Voice input and output
- Deepgram transcription
- MiniMax M3 reasoning
- MisoTTS voice generation
- Pinecone retrieval from manually ingested PDFs
- Math object tool
- Basic memory update tool
- LangSmith tracing
- Session export or transcript capture

## MVP Nice-to-Haves

- Polished UI microinteractions
- Health-check warmup UI
- Selective MathPix ingestion
- Better retrieval reranking
- Session summaries

## Explicitly Out of Scope for MVP

- Native mobile app
- Google Drive automatic sync
- Model routing
- Diagram generation
- Sophisticated memory frameworks
- Full context compaction
- Public sharing features

## Milestone Plan

### Milestone 1: Knowledge Base and Design
- Complete this document suite
- Graduate Brain Fart into Tool Project

### Milestone 2: Data/RAG Foundation
- Build ingestion script
- Process initial qualifier exams and notes
- Validate page-level retrieval

### Milestone 3: Agent Core
- Integrate MiniMax M3
- Implement `retrieve_documents`
- Implement `create_math_object`
- Implement `update_memory`

### Milestone 4: Voice Pipeline
- Add Deepgram STT
- Add MisoTTS on Modal
- Wire through Pipecat

### Milestone 5: Web App
- Build Vercel frontend
- Connect to backend
- Add session states and audio I/O

### Milestone 6: Observability and Testing
- Add LangSmith traces
- Run functional tests
- Run live walk-and-talk test

## Success Criteria

A successful MVP allows the user to open a phone web app, speak about a macro qualifier topic, receive a natural spoken response grounded in documents when appropriate, and inspect traces when something goes wrong.
