# Specification 0002: Source Ingestion

- Status: Draft
- Phase: 3

## Problem

DTFM needs a safe, idempotent way to accept files, byte streams, and immutable host references while preserving source identity and original evidence.

## Inputs

- local file path provided by an authorized host;
- byte stream with declared metadata;
- immutable source adapter reference;
- optional workspace and retention policy identifiers.

## Required behavior

1. Treat all inputs as untrusted.
2. Enforce configurable byte, container-member, and processing limits before expensive work.
3. Detect media type from content; extensions are hints only.
4. Compute a cryptographic content hash while reading the source.
5. Record the original filename separately from source identity.
6. Preserve original bytes or an immutable retrievable reference according to host policy.
7. Create an idempotency key from source identity, configuration fingerprint, and requested pipeline profile.
8. Never overwrite an existing source silently.
9. Return a stable source identifier and ingestion status.
10. Emit structured audit events without logging document content.

## Duplicate handling

Byte-identical inputs may reference the same stored blob while retaining distinct acquisition records when host context differs. Hash equality proves byte equality only, not semantic equality.

## Failure cases

- unsupported or unknown format;
- size or member limit exceeded;
- inaccessible host reference;
- hash or storage failure;
- malformed container;
- cancelled ingestion.

Failures must not leave a completed source record. Recoverable intermediate state must be identifiable and cleanable.

## Acceptance criteria

- Repeating the same request does not create conflicting processing jobs.
- Original bytes can be verified against the stored hash.
- A misleading extension does not override detected media type.
- Oversized and archive-bomb inputs are rejected before full expansion.
- Logs contain identifiers and diagnostics, not extracted content.
