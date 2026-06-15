# Component Design

## 1. Web App

**Host:** Vercel  
**Form:** Mobile-first web app / PWA

Responsibilities:
- Capture microphone audio
- Play response audio
- Display math objects and relevant visual/text context
- Show session state: listening, thinking, retrieving, speaking
- Provide upload/export controls
- Trigger backend health checks on startup to warm services

Design requirements:
- Beautiful, calm, minimal, tasteful
- Works on phone without laptop dependency
- Usable while walking

## 2. Voice Pipeline Orchestrator

**Framework:** Pipecat  
**Host:** Modal

Responsibilities:
- Manage voice session state
- Route audio to STT
- Route transcript to LLM
- Execute tools
- Route final response to TTS
- Stream generated audio back to client
- Log traces to LangSmith

## 3. Speech-to-Text

**Service:** Deepgram Nova-3

Responsibilities:
- Real-time transcription
- High-quality technical/economic speech recognition

Quality is prioritized over control for this component.

## 4. Reasoning Core

**Model:** MiniMax M3 via Ollama Cloud

Responsibilities:
- Answer questions
- Decide when to retrieve documents
- Use math object tool for equations/symbols
- Store important memories
- Maintain tutor persona and economic rigor

## 5. Text-to-Speech

**Model:** MisoTTS  
**Host:** Modal GPU

Responsibilities:
- Convert final spoken response text into natural voice
- Preserve non-robotic, intelligent conversational feel

MisoTTS is TTS only. It does not understand math; math verbalization must happen upstream through tools and prompts.

## 6. RAG Store

**Service:** Pinecone

Responsibilities:
- Store page-level chunks from PDFs
- Store metadata
- Return relevant raw pages within token budgets

## 7. Memory System

Initial memory is a single shared store.

Responsibilities:
- Store tutor-relevant memories: pain points, breakthroughs, recurring confusion, performance indicators
- Retrieve memory snippets for future sessions

Extraction is agent-driven.

## 8. Observability

**Tool:** LangSmith

Responsibilities:
- Trace tool calls
- Inspect retrieval decisions
- Track latency, tokens, and cost
- Support vibe engineering and debugging with coding agents

## 9. Export/Synthesis

Responsibilities:
- Export transcript and key concepts
- Prepare handoff to Hermes for educational asset creation
- Future: generate Manim lectures, notes, and public-good artifacts
