# ADR 0001: Local-first core processing

- Status: Accepted
- Date: 2026-07-21

## Context

DTFM is intended for privacy-sensitive documents and must remain useful inside desktop and self-hosted applications. Requiring a hosted service would create an unnecessary trust dependency and prevent offline operation.

## Decision

Core ingestion, extraction, normalization, validation, canonical persistence, and lexical search must operate locally without mandatory network access.

Remote OCR, language models, embeddings, or other processors may be provided only as optional adapters that require explicit host configuration and declare what data leaves the local environment.

## Consequences

### Positive

- Documents can remain within the user's controlled environment.
- Baseline operation works offline.
- Host applications can make clear privacy guarantees about the core.
- Remote providers remain replaceable.

### Negative

- Local installation may require larger optional dependencies.
- Performance depends on available local resources.
- Some advanced processors may be unavailable without optional remote adapters.

## Rejected alternatives

- Mandatory cloud processing.
- A cloud-first core with an incomplete offline mode.
