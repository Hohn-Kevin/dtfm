# Storage Architecture

## Storage roles

DTFM separates canonical state from rebuildable indexes.

### Source store

Stores or references original bytes according to host policy. Content-addressed storage is preferred when DTFM manages source bytes directly. The host may instead provide an immutable source adapter.

### Relational store

Stores canonical metadata, segments, artifacts, assertions, provenance, processing runs, review decisions, and configuration fingerprints.

The baseline implementation should use SQLite because it is local, transactional, portable, embeddable, and suitable for desktop and self-hosted use. The persistence interfaces must not expose SQLite-specific behavior to the domain model.

### Blob store

Stores large extracted artifacts such as images, OCR intermediates, and model outputs when they are unsuitable for relational rows. Blob identity should be content-addressed where practical.

### Full-text index

Provides lexical search over extracted and normalized text. The baseline may use the relational database's native full-text capabilities when sufficient.

### Semantic index

Stores optional embeddings and nearest-neighbor indexes. It is a replaceable projection, not a canonical database. DTFM must function without it.

## Consistency rules

- Canonical relational writes and processing-state transitions must be transactional.
- Index failures must not corrupt canonical records.
- Specialized indexes must be rebuildable.
- Deleting a source must follow an explicit retention policy and remove or tombstone dependent projections consistently.
- Hashes identify byte equality, not semantic equality.
- Database backups must be possible without external services.

## Multi-tenant and host isolation

The initial architecture is single-installation and local-first. Host applications may maintain multiple isolated workspaces. Workspace boundaries must be represented explicitly so records, indexes, encryption keys, and retention policies cannot be mixed accidentally.

## Encryption

DTFM does not claim transparent encryption merely because data is stored locally. Encryption at rest is a deployment capability that may be supplied by the operating system, encrypted volumes, host applications, or a later storage adapter. Secrets and keys must never be stored in source metadata or logs.
