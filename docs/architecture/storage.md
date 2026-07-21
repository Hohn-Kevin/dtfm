# Storage Architecture

## Storage roles

DTFM separates canonical state from rebuildable indexes.

### Source store

Stores or references original bytes according to host policy. Content-addressed storage is preferred when DTFM manages source bytes directly. The host may instead provide an immutable source adapter.

### Relational store

Stores canonical metadata, segments, artifacts, assertions, provenance, processing runs, review decisions, and configuration fingerprints.

SQLite is the baseline relational store adapter because it is local, transactional, portable, embeddable, and suitable for desktop and self-hosted use. It is not mandatory for every deployment.

Persistence interfaces must not expose SQLite-specific behavior to the domain model. A compatible relational adapter may replace SQLite completely for an installation when its transaction, migration, integrity, and isolation guarantees satisfy the same contracts.

Each DTFM installation or workspace has exactly one authoritative canonical relational store. Running SQLite beside another canonical adapter as an independent second source of truth is not supported.

Host-owned business records remain outside the canonical DTFM store unless a future accepted specification explicitly defines otherwise. Hosts reference DTFM records through stable identifiers and may maintain rebuildable projections for their own workflows.

### Blob store

Stores large extracted artifacts such as images, OCR intermediates, and model outputs when they are unsuitable for relational rows. Blob identity should be content-addressed where practical.

### Full-text index

Provides lexical search over extracted and normalized text. The baseline may use the relational database's native full-text capabilities when sufficient.

### Semantic index

Stores optional embeddings and nearest-neighbor indexes. It is a replaceable projection, not a canonical database. DTFM must function without it.

## Canonical ownership

Canonical DTFM state includes provenance, processing history, review decisions, and the current status of assertions and artifacts. Export packages, host-side tables, caches, full-text indexes, vector indexes, and generated reports are projections unless an accepted specification states otherwise.

A projection must not accept independent changes that silently contradict canonical DTFM state. Corrections enter through the review or integration contracts and create provenance-bearing canonical records.

## Consistency rules

- Canonical relational writes and processing-state transitions must be transactional.
- Index failures must not corrupt canonical records.
- Specialized indexes and host projections must be rebuildable or explicitly marked as externally owned.
- Deleting a source must follow an explicit retention policy and remove or tombstone dependent projections consistently.
- Hashes identify byte equality, not semantic equality.
- Database backups must be possible without external services.
- Adapter changes require an explicit migration path and verification before the new store becomes authoritative.

## Multi-tenant and host isolation

The initial architecture is single-installation and local-first. Host applications may maintain multiple isolated workspaces. Workspace boundaries must be represented explicitly so records, indexes, encryption keys, and retention policies cannot be mixed accidentally.

## Encryption

DTFM does not claim transparent encryption merely because data is stored locally. Encryption at rest is a deployment capability that may be supplied by the operating system, encrypted volumes, host applications, or a later storage adapter. Secrets and keys must never be stored in source metadata or logs.
