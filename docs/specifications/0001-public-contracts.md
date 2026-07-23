# Specification 0001: Public Contracts

- Status: Draft
- Phase: 3

## Problem

DTFM must expose the same stable behavior to embedded Python hosts, local workers, command-line tools, and service adapters without leaking implementation-specific objects.

## Requirements

1. Public data contracts are versioned independently from persistence schemas.
2. Pydantic models are the authoritative Python representation.
3. JSON Schema is generated from the authoritative models for language-neutral validation.
4. HTTP adapters expose OpenAPI derived from the same contract definitions.
5. Events and export packages use versioned JSON-compatible envelopes.
6. Internal ORM objects, database sessions, exceptions, vendor SDK objects, and model-native responses never cross public boundaries.
7. Unknown additive fields are tolerated where the consumer contract permits forward compatibility.
8. Breaking changes require a new major contract version, migration notes, and an accepted ADR.

## Envelope fields

Every process-boundary message must include:

- `contract_version`;
- `message_type`;
- `message_id`;
- `created_at`;
- `workspace_id` when applicable;
- `correlation_id` when part of a workflow;
- `payload`.

## Error model

Public errors contain a stable code, human-readable message, retryability flag, optional field path, and correlation identifier. Stack traces and document contents are excluded by default.

## Acceptance criteria

- Equivalent Python and JSON payloads validate against the same contract version.
- Generated schemas are reproducible.
- A non-Python client can ingest a source, inspect a processing run, retrieve assertions, and submit a review decision without Python-specific knowledge.
- Contract tests detect drift between Python models, JSON Schema, and OpenAPI.

## Non-goals

- Selecting a specific HTTP framework.
- Defining every endpoint before the domain specifications are complete.
