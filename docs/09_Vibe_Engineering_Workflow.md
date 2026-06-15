# Vibe Engineering Workflow

## Purpose

This document defines how Phronesis should be built using coding agents while preserving design intent, traceability, and quality.

## Working Style

- Build in small, verifiable increments.
- Keep design documents updated as decisions change.
- Use traces and logs to guide iteration.
- Prefer working artifacts over speculative plans.
- Do not let coding agents invent architecture without reference to this knowledge base.

## Recommended Development Loop

1. Select a small implementation target.
2. Write or update the relevant design note.
3. Ask coding agent to implement only that slice.
4. Run tests or manual verification.
5. Inspect logs/traces.
6. Record decisions or surprises in `14_Decision_Engineering_Log.md`.
7. Commit or checkpoint.

## Coding Agent Instructions

When delegating to Codex or another coding agent:
- Provide the relevant document paths.
- Give a narrow task.
- Require it to read project docs before editing.
- Require verification output.
- Require notes on deviations from design.

## Human / Hermes Role

Hermes should act as:
- Product/system design partner
- Documentation maintainer
- Test planner
- Reviewer of coding-agent outputs
- Trace interpreter

## Coding Agent Role

Coding agents should act as:
- Implementers of scoped tasks
- Test runners
- Refactoring assistants
- Error investigators

## Engineering Log Discipline

The live engineering log should record:
- Decisions
- Failed attempts
- Surprising behavior
- Tool quirks
- Changes in scope
- Performance/cost observations

## Suggested Initial Build Order

1. Project scaffold
2. Local ingestion script
3. Pinecone schema and retrieval tool
4. Math object tool
5. MiniMax M3 API integration
6. Basic Pipecat text loop
7. Deepgram STT integration
8. MisoTTS service on Modal
9. Vercel web frontend
10. LangSmith tracing
11. End-to-end voice test

## Guardrails

- Do not build a native mobile app for MVP.
- Do not add Google Drive sync before manual ingestion works.
- Do not over-engineer memory before basic tutor sessions work.
- Do not implement model routing in MVP.
