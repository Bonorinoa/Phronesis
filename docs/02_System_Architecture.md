# System Architecture

## High-Level Architecture

Phronesis is a phone-first web application connected to a cloud-hosted voice-agent pipeline.

```
┌─────────────────────────────────────────────────────────────┐
│                    WEB APP (Vercel + AI SDK)                │
│   [Phone / Laptop UI]  ←→  [Audio I/O]  ←→  [Export]       │
└───────────────────────────────┬─────────────────────────────┘
                                │ WebSocket / Streaming
                                ▼
┌─────────────────────────────────────────────────────────────┐
│         VOICE PIPELINE ORCHESTRATOR (Pipecat on Modal)      │
│                                                             │
│   Turn Manager + VAD    ←→   Thinking Pause Handler        │
│            │                           │                    │
│            ▼                           ▼                    │
│       STT Layer                   TTS Layer                 │
│   (Deepgram Nova-3)          (MisoTTS on Modal)             │
└───────────────────────────────┬─────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────┐
│                      REASONING CORE                         │
│                                                             │
│   MiniMax M3  ←→  RAG Engine  ←→  Memory Store             │
│       │                 │              │                    │
│       ▼                 ▼              ▼                    │
│ Custom Tools       Pinecone Docs   Long-term Concepts       │
└─────────────────────────────────────────────────────────────┘
```

## Primary Data Flow

1. User opens phone web app.
2. App warms up backend services with a health check.
3. User speaks.
4. Audio is streamed to Pipecat on Modal.
5. Pipecat sends audio to Deepgram Nova-3.
6. Transcript returns to Pipecat.
7. Pipecat passes transcript + current state to MiniMax M3.
8. MiniMax M3 may call tools:
   - `retrieve_documents`
   - `create_math_object`
   - `update_memory`
9. Retrieved context and tool outputs are injected into final generation.
10. Final spoken response is synthesized by MisoTTS.
11. Audio is streamed back to the phone web app.
12. Session state and traces are logged.

## State Model

The system is intentionally stateful. The main states are:

| State | Meaning |
|---|---|
| `idle` | Session exists but no active turn is happening |
| `waiting_for_user` | System is listening or waiting for input |
| `receiving_audio` | User speech is being captured/streamed |
| `transcribing` | Deepgram is producing transcript |
| `agent_thinking` | MiniMax M3 is deciding what to do |
| `tool_calling` | Agent has requested one or more tools |
| `tool_execution` | Tools are running |
| `response_generation` | Final answer is being produced |
| `tts_synthesis` | MisoTTS is generating speech |
| `playing_response` | Response audio is playing |
| `session_end` | Session ended or exported |

Substates inside `tool_calling` include retrieval, math-object creation, and memory update.

## Context Objects

The context manager orchestrates:

### Static Context
- System instructions
- Current mode
- Tool descriptions
- Retrieval/math/memory guidelines

### Variable Context
- Recent/full chat history
- Retrieved document pages
- Long-term memory snippets
- Current turn state
- Tool outputs

### Control Objects
- Token budgets
- Retrieval follow-up flag
- Session state
- Cost/performance metrics
- Trace identifiers

## Graceful Context Exhaustion

For MVP, no sophisticated compaction is required. If context is exhausted, the system should end gracefully with deterministic messaging:

> Sorry, we ran out of context, but we can continue in a new session. I'll try to remember what we discussed.
