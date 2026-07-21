# ADR 0002: Python and Pydantic baseline

- Status: Accepted
- Date: 2026-07-21

## Context

Document processing depends on mature libraries for parsing, OCR, image handling, natural-language processing, and machine learning. Public boundaries also require strict typed validation, serializable contracts, and language-neutral integration for non-Python hosts.

## Decision

The initial implementation baseline will use Python. Public configuration and data-transfer models will use Pydantic as their Python representation.

JSON Schema is the language-neutral schema representation for public data contracts. HTTP-based adapters use OpenAPI descriptions derived from the same authoritative contract definitions. Events and export packages use versioned JSON-compatible envelopes.

Direct library embedding is supported for Python hosts. Hosts using another runtime integrate through a local worker, command-line, IPC, or service boundary rather than receiving Python runtime objects.

Domain rules must remain separated from framework, ORM, and vendor-specific objects. Public models are versioned contracts and are not direct database entities. Internal Python objects, ORM entities, database sessions, and vendor responses must not cross process or language boundaries.

## Consequences

### Positive

- Broad document-processing ecosystem.
- Strong compatibility with local OCR and machine-learning tools.
- Typed and validated Python-facing models.
- Language-neutral JSON Schema contracts for other runtimes.
- OpenAPI-based client generation for HTTP adapters.
- Shared domain semantics across embedded, worker, and service deployments.

### Negative

- CPU-heavy processors may require native libraries or subprocesses.
- Packaging optional system dependencies requires care.
- Contract generation and compatibility checks must prevent drift between Python models, JSON Schema, and OpenAPI.
- Runtime type validation does not replace static analysis or tests.
- Non-Python hosts require a process or service boundary.

## Rejected alternatives

- Selecting a systems language before processor requirements are known.
- Using untyped dictionaries as the public contract.
- Coupling public contracts directly to database models.
- Treating Pydantic objects as a language-neutral wire format.
- Maintaining unrelated hand-written schemas for each integration adapter.
