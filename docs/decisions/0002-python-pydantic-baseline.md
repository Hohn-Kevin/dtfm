# ADR 0002: Python and Pydantic baseline

- Status: Accepted
- Date: 2026-07-21

## Context

Document processing depends on mature libraries for parsing, OCR, image handling, natural-language processing, and machine learning. Public boundaries also require strict typed validation and serializable contracts.

## Decision

The initial implementation baseline will use Python. Public configuration and data-transfer models will use Pydantic.

Domain rules must remain separated from framework, ORM, and vendor-specific objects. Public models are versioned contracts and are not direct database entities.

## Consequences

### Positive

- Broad document-processing ecosystem.
- Strong compatibility with local OCR and machine-learning tools.
- Typed, validated, serializable integration models.
- Shared implementation patterns across embedded, worker, and service deployments.

### Negative

- CPU-heavy processors may require native libraries or subprocesses.
- Packaging optional system dependencies requires care.
- Runtime type validation does not replace static analysis or tests.

## Rejected alternatives

- Selecting a systems language before processor requirements are known.
- Using untyped dictionaries as the public contract.
- Coupling public contracts directly to database models.
