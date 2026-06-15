# RAG and Ingestion Design

## Core Decision

We will own the ingestion and retrieval logic while using Pinecone as the managed vector store.

This gives control over how economic documents are processed without requiring us to manage vector infrastructure.

## Document Sources

Initial MVP:
- Manual upload or local ingestion from selected PDFs

Deferred:
- Google Drive sync
- Automatic folder watching

Reason for manual MVP:
- Simpler
- Easier quality control
- Avoids Google Drive auth and sync complexity

## Supported Documents

Initial supported type:
- PDF

Primary document classes:
- Past macro qualifier exams
- Lecture notes
- Textbooks such as Stokey-Lucas-Prescott and Sargent-Ljungqvist
- Slide deck PDFs

Some documents may be clean digital PDFs; others may be medium-quality scanned textbook pages.

## Chunking Strategy

Use **full pages** as chunks.

Rationale:
- MiniMax M3 has a very large context window.
- Full pages preserve surrounding context, equations, and argument flow.
- The user prefers too much context over too little.
- Small chunks are less valuable with current long-context models.

## Cleaning Strategy

Keep cleaning light at first.

Allowed:
- Basic text extraction
- Page break normalization
- Removing obvious repeated whitespace
- Capturing page numbers and source metadata

Avoid for MVP:
- Transformative summarization
- Aggressive rewriting
- Heavy OCR cleanup pipelines

## OCR / Math Extraction

MathPix credits are available but advanced OCR is not an MVP blocker.

Recommended path:
1. Start with standard PDF parsing.
2. Evaluate extraction quality on key documents.
3. Selectively apply MathPix to high-value scanned or math-heavy documents.

MathPix cost is one-time ingestion cost, not ongoing inference cost.

## Metadata Schema

### Required / Core

| Field | Values / Notes |
|---|---|
| `document_type` | `qualifier_exam`, `lecture_notes`, `textbook` |
| `source_name` | document title/name |
| `page_number` | page number |

### Domain Metadata

| Field | Values / Notes |
|---|---|
| `model_family` | See list below |
| `topic_tags` | Optional granular tags |
| `year` | Useful for exams |

### Model Families

- `overlapping_generations`
- `deterministic_recursive`
- `asset_pricing`
- `search_theory`
- `competitive_equilibrium`
- `recursive_contracts`

## Retrieval Architecture

- Agent decides when to retrieve.
- Default one query per turn.
- One follow-up retrieval allowed if initial results are insufficient.
- Agent can choose metadata filters.
- Tool enforces hard 50k token cap.
- Results return raw pages, not summaries.

## Reranking

Reranking is expected to help and should be included when practical.

## Query Rewriting

Avoid separate query rewriting in MVP. The agent generates the retrieval query directly, so prompt/tool design should steer query quality.
