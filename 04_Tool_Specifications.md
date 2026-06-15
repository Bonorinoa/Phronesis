# Tool Specifications

## Tool Philosophy

Phronesis relies on a small number of high-quality tools with clear usage guidelines. The agent decides when to call tools, while the engineering harness ensures reliability, observability, and predictable outputs.

Parallel tool calls are allowed, with a practical MVP cap of approximately two concurrent tool calls per turn.

---

## 1. `create_math_object`

### Purpose

Convert mathematical expressions or symbols into:
1. A precise, natural spoken version for TTS
2. A clean display version for the UI

### When to Use

Use whenever the agent wants to express:
- Equations
- Derivatives
- Integrals
- Recursive laws of motion
- Bellman equations
- Equilibrium conditions
- Mathematical symbols or notation

### Inputs

| Field | Type | Required | Description |
|---|---|---:|---|
| `math_content` | string | yes | Raw equation, symbol, or expression |
| `context` | string | no | Surrounding explanation or intended meaning |
| `source` | string | no | `lecture_notes`, `textbook`, `qualifier_exam`, `generated`, `external` |

### Outputs

| Field | Type | Description |
|---|---|---|
| `spoken_text` | string | Precise natural-language verbalization |
| `display_text` | string | Clean LaTeX/display version |

### Example

Input:

```json
{
  "math_content": "dY/dK = f'(K)",
  "context": "marginal product condition in a production function",
  "source": "generated"
}
```

Output:

```json
{
  "spoken_text": "the derivative of output with respect to capital equals the marginal product of capital",
  "display_text": "$\\frac{dY}{dK} = f'(K)$"
}
```

### Notes

- Precision is preferred over concision.
- The tool should not rewrite the whole response.
- Diagrams are deferred until after the live proof of work.

---

## 2. `retrieve_documents`

### Purpose

Retrieve relevant raw pages from the document collection in Pinecone.

### When to Use

Use when the answer requires grounding in:
- Past qualifier exams
- Lecture notes
- Textbooks
- Specific sources or pages
- Specific economic model families

Do not use if recent context or general knowledge is sufficient.

### Retrieval Strategy

- Default to one high-quality query.
- Use metadata filters when useful.
- Allow one follow-up retrieval if the first result is insufficient or ambiguous.
- Enforce hard token cap.

### Inputs

| Field | Type | Required | Description |
|---|---|---:|---|
| `query` | string | yes | Agent-generated search query |
| `filters` | object | no | Metadata filters chosen by the agent |
| `max_tokens` | integer | no | Hard cap; default 50,000 |
| `follow_up` | boolean | no | Whether this is a second retrieval in the same turn |

### Outputs

| Field | Type | Description |
|---|---|---|
| `results` | list | Raw pages with text and metadata |
| `total_tokens` | integer | Number of tokens returned |

### Metadata Fields

- `document_type`: `qualifier_exam`, `lecture_notes`, `textbook`
- `model_family`: `overlapping_generations`, `deterministic_recursive`, `asset_pricing`, `search_theory`, `competitive_equilibrium`, `recursive_contracts`
- `topic_tags`: list of granular tags
- `source_name`: document/source title
- `year`: exam or document year if known
- `page_number`: page number

---

## 3. `update_memory`

### Purpose

Store high-signal information for future sessions.

### When to Use

Use when the conversation reveals:
- A recurring pain point
- A correction or misconception
- A breakthrough
- A useful learning preference
- Progress on a model family
- An explicit request to remember something

### Inputs

| Field | Type | Required | Description |
|---|---|---:|---|
| `memory_text` | string | yes | Concise memory entry |
| `importance` | string | no | `low`, `medium`, `high` |
| `memory_type` | string | no | `pain_point`, `breakthrough`, `preference`, `progress`, `concept` |
| `model_family` | string | no | Relevant economic model family |
| `source_turn_id` | string | no | Trace/session reference |

### Outputs

| Field | Type | Description |
|---|---|---|
| `memory_id` | string | Stored memory identifier |
| `status` | string | Success/failure |

### Notes

- Extraction is agent-driven.
- Start with one shared memory system.
- Edit/delete functionality is low priority for MVP.
