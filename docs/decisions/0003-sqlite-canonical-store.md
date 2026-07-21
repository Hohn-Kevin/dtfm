# ADR 0003: SQLite canonical relational store

- Status: Accepted
- Date: 2026-07-21

## Context

The engine needs transactional local persistence for provenance, processing state, structured facts, review history, and searchable metadata. It must embed cleanly into desktop and self-hosted applications without requiring a separate database server.

## Decision

SQLite will be the baseline canonical relational store.

Specialized full-text, vector, graph, or blob stores are projections or adapters. They must not become the only location of canonical assertions, provenance, or review decisions.

Persistence is accessed through repository interfaces so a future server-grade adapter can be introduced without changing domain contracts.

## Consequences

### Positive

- Zero-service local installation.
- Transactional and portable storage.
- Straightforward backup and workspace isolation.
- Good fit for embedded and single-organization deployments.

### Negative

- Write concurrency is bounded.
- Large distributed installations may require another adapter.
- Careful migration and transaction design remain necessary.

## Rejected alternatives

- Requiring a database server for baseline use.
- Treating a vector database as the canonical source of truth.
- Persisting only generated JSON files without transactional integrity.
