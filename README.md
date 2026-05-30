# speechlab

Status: recovery scaffold  
Authority role: audio-first review and spoken-corpus experimentation surface  
Claim level: product/research infrastructure planning; no runtime model commitment

`speechlab` is the SocioProphet lab surface for audio-first human-agent review, spoken corpus handling, listening-mode workflows, transcript provenance, and speech-channel confusability testing.

This repository is not currently the canonical speech model runtime, transcription service, or production audio ingestion plane. It is the place to define how audio-first review should be structured before downstream systems adopt it.

## Start here

- `docs/audio-first-review-runtime-v0.md` — recovery contract for audio-first review/runtime semantics.

## Intended consumers

- `prophet-platform` — workroom listening/review UX and audio-friendly sectioning.
- `alexandrian-academy` — spoken teaching objects and listenable lessons.
- `systems-learning-loops` — review patterns, spoken postmortems, and training loops.
- `ontogenesis` — audio anchors, transcript selectors, provenance, and semantic promotion boundaries.
- `model-governance-ledger` — transcription, summarization, evaluation, drift, and audio-processing receipts.
- `agentplane` — agent review actions, operator readouts, and receipt-backed effectful workflows.

## Non-goals

This scaffold does not select ASR/TTS models, define production storage, ingest private audio, train speech models, or authorize durable memory formation from spoken material.

Any future runtime integration must respect DoNotLearn / DoNotLink, transcript provenance, human review boundaries, and receipt discipline.
