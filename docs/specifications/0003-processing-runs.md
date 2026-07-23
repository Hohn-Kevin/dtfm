# Specification 0003: Processing Runs

- Status: Draft
- Phase: 3

## Problem

Processing must be restartable, inspectable, bounded, and reproducible across multiple processors and partial failures.

## Run identity

A processing run records source identifier, workspace, pipeline profile, contract version, configuration fingerprint, processor identities and versions, requested stages, timestamps, and parent run when reprocessing.

## States

- `queued`
- `running`
- `partially_completed`
- `completed`
- `failed`
- `cancelled`

State transitions are append-only audit events and canonical state changes are transactional.

## Required behavior

1. A run is idempotent for identical source, configuration, processor versions, and requested stages.
2. Each stage records start, completion, skip, cancellation, or failure.
3. Optional-stage failure does not invalidate unrelated successful artifacts.
4. Required-stage failure prevents a completed status.
5. Cancellation is cooperative and leaves completed canonical writes valid.
6. Retries create traceable attempts and do not duplicate successful outputs.
7. Resource limits and timeouts are captured in the run configuration.
8. Reprocessing never overwrites prior provenance-bearing outputs invisibly.

## Completeness

Public results include requested stages, completed stages, failed stages, skipped stages, and unresolved review requirements so consumers can distinguish complete from partial output.

## Acceptance criteria

- Interrupted work can resume or retry without corrupting canonical state.
- A failed optional embedding processor does not hide successfully extracted text.
- Identical completed runs can be reused according to host policy.
- Changed processor versions produce a distinct run and provenance chain.
- Consumers can determine whether a result is complete for the requested profile.
