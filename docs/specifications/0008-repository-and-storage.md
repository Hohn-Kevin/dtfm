# Specification 0008: Repository and Storage

- Status: Draft
- Phase: 3

## Problem

DTFM requires transactional canonical persistence while supporting SQLite as the baseline adapter and alternative relational adapters for other deployment shapes.

## Normative terms

The terms MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are interpreted as described in RFC 2119 and RFC 8174.

## Canonical store rules

1. Each workspace MUST have exactly one canonical relational store at a time.
2. SQLite MUST be supported as the baseline adapter.
3. Alternative adapters MAY replace SQLite completely for canonical persistence.
4. A deployment MUST NOT split canonical record types across competing relational stores without a later accepted specification.
5. Host domain records, export projections, search indexes, caches, and analytics tables MUST NOT be treated as canonical DTFM state.

## Repository boundary

Repository interfaces MUST expose domain operations and transaction boundaries without leaking ORM sessions, SQL dialect objects, or adapter-specific row models. Writes that change processing state and canonical outputs atomically MUST share one transaction.

## Blob and source storage

Large artifacts and source bytes MAY use a blob adapter. Blob references MUST be content-verifiable and workspace-scoped. A successful canonical reference MUST NOT point to an uncommitted or inaccessible blob.

## Index consistency

1. Full-text, semantic, and relationship indexes are rebuildable projections.
2. Index failures MUST NOT roll back already valid canonical results unless the requested profile explicitly requires that index.
3. Projection checkpoints MUST make stale or incomplete indexes detectable.
4. Rebuilding an index MUST NOT change canonical identifiers or provenance.

## Backup and migration

The baseline adapter MUST support consistent offline backup. Online backup behavior MAY be adapter-specific. Migrations MUST be ordered, versioned, idempotent when safely repeated, and fail without partially advancing the recorded schema version.

## Acceptance criteria

- The same repository contract passes against SQLite and a test double.
- Transaction failure leaves neither a completed run state nor partially committed canonical outputs.
- A deleted semantic index can be rebuilt from canonical records.
- A workspace cannot read or write records belonging to another workspace.
- Replacing the relational adapter does not change public contract payloads.
