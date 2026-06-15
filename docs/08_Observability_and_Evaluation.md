# Observability and Evaluation Plan

## Observability Goal

Observability exists primarily to support debugging and vibe engineering with coding agents. It is also useful for improving the deployed agentic system.

## Tool Choice

**LangSmith** is the initial observability tool.

Rationale:
- Good trace inspection
- Strong support for tool calls and agent workflows
- Useful for coding-agent-assisted development
- Supports token/cost/latency monitoring

## What to Trace

MVP traces should capture:
- Session ID
- Turn ID
- Current state
- Transcript input
- LLM model call
- Tool calls and arguments
- Retrieval filters and results metadata
- Follow-up retrieval flag
- Math object calls
- Memory updates
- TTS latency
- STT latency
- Total turn latency
- Token usage
- Estimated cost

## Evaluation Philosophy

Use established RAG evaluation strategies where possible. Keep custom evals lightweight early.

## Priority Ranking

1. Functional Correctness
2. Context Management
3. Verbal Intelligence
4. Cost & Efficiency
5. Reasoning Quality
6. User Experience

## Initial Evaluation Approach

### Functional Correctness
- Do tools execute when expected?
- Are schemas respected?
- Does retrieval return relevant raw pages?
- Does math tool return both spoken and display fields?

### Context Management
- Does the agent avoid unnecessary retrieval?
- Does it use memory appropriately?
- Does it maintain coherence across turns?

### Verbal Intelligence
- Does spoken math sound natural and precise?
- Does the agent explain concepts like a strong tutor?

### Cost & Efficiency
- Track cost per session
- Track tokens per turn
- Track retrieval frequency
- Track TTS GPU usage

### Reasoning Quality
- Lightweight manual review on qualifier-style questions

### User Experience
- Qualitative session feedback

## Deferred Details

Exact metrics, eval sets, and dashboards will be defined during implementation.
