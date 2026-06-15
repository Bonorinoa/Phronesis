# Context Management Strategy

## Why This Matters

Context management is the central design challenge for Phronesis. The system must coordinate voice turns, chat history, retrieved documents, memory, tool outputs, and static instructions without becoming slow, confused, or polluted.

## Mental Model

The system prompt is the agent's world model. It should give the LLM enough information to behave well in the world of this application.

We distinguish:

### Static Context
Relatively stable during a session:
- Identity and purpose
- Current mode
- Agent priorities
- Tool descriptions and schemas
- Retrieval/math/memory guidelines
- Output style rules

### Variable Context
Changes during the session:
- User transcript
- Chat history
- Retrieved pages
- Memory snippets
- Current state
- Tool results

### Control Context
Used by the harness:
- Token budgets
- Follow-up retrieval flag
- State machine state
- Trace IDs
- Cost/latency metrics

## Token Budgeting

Initial design:
- Retrieved context hard cap: **50k tokens**
- Chat history: keep as much as possible, potentially full history for MVP
- Overall history cap can be set conservatively later, e.g. 512k tokens

Rationale:
- Single-user app reduces risk of polluted long-term context.
- MiniMax M3 supports very large context.
- Avoid compaction early unless necessary.

## Context Exhaustion

For MVP, do not build sophisticated compaction.

If context becomes exhausted, end gracefully:

> Sorry, we ran out of context, but we can continue in a new session. I'll try to remember what we discussed.

## State Awareness

The agent should know the relevant state:

- Waiting for user input
- Receiving/transcribing input
- Thinking/generating
- Calling tools
- Executing tools
- Synthesizing speech
- Playing response
- Ending/exporting session

## Retrieval Context

Retrieved documents are injected as raw pages with metadata.

They should be clearly separated from:
- Conversation history
- Long-term memory
- Agent instructions

## Memory Context

Memory should be injected separately from RAG.

Memory is not source evidence. It is user/session knowledge and should influence tutoring strategy, not override document evidence.

## Deferred Work

- Sophisticated context compaction
- Importance-weighted history cleanup
- Memory decay
- Multi-mode memory stores
