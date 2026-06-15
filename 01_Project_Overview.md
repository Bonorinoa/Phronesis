# Project Overview

## Name

**Phronesis** — practical wisdom; judgment applied to real problems.

## Origin

The project originated from a Brain Fart on 2026-06-14 after reflecting on the value of walk-and-talk voice sessions for macroeconomics qualifier preparation. Existing mobile voice tools such as Grok Voice and Gemini Voice were useful but had important frictions: voice limits, mathematical/symbolic awkwardness, weaker capabilities than chat models, limited tool use, and sometimes unpleasant voice behavior.

## Goal

Build a specialized voice application for rigorous, grounded, aesthetically excellent conversations about advanced economics.

Initial use case:
- Macroeconomics qualifier preparation
- Retake date: July 31
- Build target: usable MVP before June 18 if possible

Longer-term use cases:
- Research idea development
- Verbal debate and intellectual sparring
- Conversion of conversations into lecture notes, key concepts, Manim lectures, or other educational assets

## Persona

Phronesis should feel like an intellectual friend and mentor:

- Attentive
- Curious
- Rigorous
- Witty
- Challenging
- Knowledgeable
- Verbal and visually intuitive

It is not a general-purpose super-agent. It is not mainly a coding agent. It is a conversational intelligence system constrained by economic theory, with enough general culture and adjacent-field knowledge to draw useful connections.

## Core Requirements

1. **Voice naturalness** — The voice must not feel robotic.
2. **Economic rigor** — Strong explanations of economic theory and recursive macroeconomic modeling.
3. **Low friction** — Phone-first web app; no requirement that the laptop be open or unlocked.
4. **Context management** — The system must maintain coherent, useful conversation context.
5. **Grounding** — Ability to retrieve from qualifier exams, textbooks, slides, and lecture notes.
6. **Taste** — Functional and beautiful; aesthetics are part of the product, not polish.

## Initial Architecture Summary

- Frontend: Vercel web app / PWA
- Orchestrator: Pipecat on Modal
- Reasoning LLM: MiniMax M3 via Ollama Cloud
- TTS: MisoTTS hosted on Modal
- STT: Deepgram Nova-3
- RAG store: Pinecone
- Observability: LangSmith

## Graduation Status

This project has graduated from `~/Hermes/Brain_Farts/` to an active Tool Project under:

`~/Hermes/Projects/Phronesis/`
