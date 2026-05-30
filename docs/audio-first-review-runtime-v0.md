# Audio-First Review Runtime v0

Status: draft recovery contract  
Authority repo: `SocioProphet/speechlab`  
Claim level: product/research infrastructure planning; no runtime model commitment  
Scope: audio-first review, spoken corpus handling, transcript provenance, listening-mode UX, and speech-channel confusability testing

## Purpose

This document recovers `speechlab` as the audio-first review and spoken-corpus experimentation surface for the SocioProphet estate.

The recovered idea is not simply speech-to-text. The important surface is the full loop:

```text
audio event -> transcript/provenance -> sectioned review object -> human/agent review -> correction -> receipt -> teaching or memory decision
```

This contract defines the semantics needed before downstream product or agent systems ingest, summarize, teach from, or remember spoken material.

## Core problem

Audio is a high-bandwidth human interface, but it is also fragile:

- transcripts can mishear domain terms;
- long responses are hard to listen to;
- section boundaries matter;
- corrections can be more important than the first transcript;
- spoken material can contain private or ephemeral context;
- audio summaries can silently become memory;
- agent readouts can sound authoritative even when evidence is weak.

Speechlab exists to make that loop explicit and receipted.

## Core objects

### AudioEvent

A captured or streamed audio segment with source, time, speaker scope, consent/policy scope, and retention boundary.

### TranscriptArtifact

A text representation of audio with model/tool provenance, timestamps where available, confidence where available, and correction state.

### AudioAnchor

A selector into an audio file or stream, such as time range, speaker turn, segment id, or transcript span linked back to audio.

### ReviewSection

A chunked, listenable review object. Sections should be sized for human listening, not just written-document completeness.

### CorrectionEvent

A user, reviewer, or agent correction to a transcript, summary, pronunciation, named entity, term boundary, or interpretation.

### ConfusabilityFixture

A test case for terms or phrases that are likely to be misheard, merged, split, normalized incorrectly, or semantically confused.

### SpokenTeachingObject

A listenable lesson, workroom card, drill, or Academy object derived from reviewed audio or transcript material.

### AudioReviewReceipt

A receipt recording source audio, transcript artifact, review sections, corrections, policy decisions, memory decisions, and downstream teaching/adoption state.

## Required invariants

1. Audio capture is not transcription permission.
2. Transcription is not durable-memory permission.
3. Transcript text is not automatically evidence.
4. A summary is not a source artifact.
5. A correction event must supersede or qualify the transcript it corrects.
6. Spoken teaching objects require reviewed source and claim boundaries.
7. Long-form review should be sectioned for listening.
8. Confusable terms must be testable fixtures when they affect meaning.
9. Audio-derived memories must respect DoNotLearn and DoNotLink.
10. Every effectful use emits a receipt or declares why no durable effect occurred.

## Audio-first review loop

### 1. Capture or reference

The system records or references audio under an explicit scope.

Required fields:

- source reference;
- speaker or participant scope where known;
- consent/policy scope;
- retention boundary;
- privacy boundary;
- capture time or source artifact time.

### 2. Transcribe

The audio is transcribed by a model, tool, or human.

Required fields:

- transcription method;
- model/tool version where available;
- source audio reference;
- confidence or quality note where available;
- timestamp alignment where available;
- known gaps.

### 3. Section

The transcript or generated review is split into listenable sections.

Sectioning should optimize for spoken review:

- short enough to replay;
- semantically coherent;
- stable section identifiers;
- clear continuation boundaries;
- no hidden deletion of caveats.

### 4. Review

A human or agent reviews the transcript/sections.

Review may produce corrections, claim boundaries, topic labels, teaching candidates, or memory decisions.

### 5. Correct

Corrections must be explicit objects, not silent edits.

Correction examples:

- “mascot” corrected to “mass gap”;
- project name correction;
- acronym correction;
- speaker attribution correction;
- section boundary correction;
- claim-boundary correction.

### 6. Decide memory / teaching / action

A reviewed transcript may lead to memory, teaching, workroom note, issue, action, or archive-only disposition.

This step requires policy and receipt semantics.

### 7. Receipt

The receipt records what happened and what downstream effects were permitted.

## Confusability testing

Speechlab should maintain fixtures for high-risk speech confusions.

Examples:

| Confusion type | Example | Risk |
| --- | --- | --- |
| Domain term substitution | `mass gap` -> `mascot` | corrupts mathematical meaning |
| Repo/project name drift | `SocioProphet` -> `social profit` | corrupts authority references |
| Acronym splitting | `PFK` -> `P F K` or unrelated phrase | breaks retrieval and indexing |
| Homophone drift | `cite` / `site` / `sight` | corrupts action intent |
| Boundary loss | separate instructions merged into one | creates unsafe action scope |
| Tone overread | frustration interpreted as permission to skip review | creates governance failure |

Confusability fixtures should be used for ASR evaluation, correction UX, agent review behavior, and workroom memory safety.

## Privacy and memory boundaries

Audio-derived artifacts are subject to DoNotLearn and DoNotLink.

DoNotLearn examples:

- do not train on private workroom audio;
- do not create durable summaries without permission;
- do not add transcript fragments to vector memory without admission;
- do not convert corrections into model/profile updates unless admitted.

DoNotLink examples:

- do not link voices across workrooms without permission;
- do not use speaker identity to bridge private contexts;
- do not create cross-topic identity edges from audio participation;
- do not expose latent-neighbor or voiceprint-style linkages.

## Downstream consumers

| Consumer | Safe use |
| --- | --- |
| `prophet-platform` | Audio-first workroom review, listenable sectioning, correction UX, memory decisions. |
| `alexandrian-academy` | Spoken teaching objects and listenable lessons after review. |
| `systems-learning-loops` | Spoken postmortems, review patterns, and correction-derived learning receipts. |
| `ontogenesis` | Audio anchors, transcript selectors, semantic promotion, and privacy constraints. |
| `model-governance-ledger` | ASR/TTS evaluation, drift, inference receipts, correction receipts, and memory-admission records. |
| `agentplane` | Review actions, readout actions, and receipt-backed effectful workflows. |
| `slash-topics` | Topic-pack surfaces for audio review and spoken evidence boundaries. |

## Promotion discipline

No audio pipeline becomes implementation-ready until it has:

1. source/capture scope;
2. transcript provenance;
3. sectioning policy;
4. correction model;
5. privacy/memory decision path;
6. receipt format;
7. confusability fixtures;
8. downstream authority surface;
9. review gate.

## Non-goals

This document does not select speech models, define a storage system, create a transcription API, authorize audio ingestion, or define production UI.

It also does not permit durable memory formation from spoken material. That requires separate policy admission and receipt semantics.

## Claim boundary

This is a recovery and placement artifact. It defines what speechlab should own before downstream systems build runtime behavior. It does not claim ASR quality, privacy compliance, product readiness, or model suitability.
