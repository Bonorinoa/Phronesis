# Deployment and Hosting Plan

## Infrastructure Overview

| Component | Host / Service |
|---|---|
| Frontend | Vercel |
| Voice orchestrator | Modal |
| TTS | MisoTTS on Modal GPU |
| STT | Deepgram Nova-3 |
| LLM | MiniMax M3 via Ollama Cloud |
| Vector DB | Pinecone |
| Observability | LangSmith |

## Modal

Modal provides cloud GPUs and serverless Python infrastructure.

Use cases in this project:
- Pipecat orchestrator
- MisoTTS service
- Potential ingestion jobs later

Relevant concepts:
- `scaledown_window` to reduce cold starts
- GPU classes such as A10G/L4
- Modal secrets for API keys
- Health-check endpoints for frontend warmup

## Vercel

Vercel hosts the web app.

Responsibilities:
- PWA frontend
- Audio capture/playback
- Session state UI
- Warmup/health-check calls

## Pinecone

Stores page-level document chunks and long-term concepts.

## Deepgram

Provides real-time speech-to-text.

## Ollama Cloud

Serves MiniMax M3.

## Cost Expectations

Rough monthly personal-use range:
- Modal: likely within $30 free tier initially
- Pinecone: likely free/low-cost for MVP
- Deepgram: low usage-based cost
- Ollama Cloud: low token cost for MiniMax M3

## Required Secrets

Likely environment variables:
- `MODAL_TOKEN_ID`
- `MODAL_TOKEN_SECRET`
- `DEEPGRAM_API_KEY`
- `PINECONE_API_KEY`
- `OLLAMA_API_KEY` or equivalent Ollama Cloud credential
- `LANGSMITH_API_KEY`

Exact names to be finalized during implementation.
