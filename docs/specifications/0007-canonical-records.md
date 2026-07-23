# Specification 0007: Canonical Records

- Status: Draft
- Phase: 3

## Problem

DTFM needs stable record semantics that support both record-oriented inputs and long-form documents without coupling public contracts to one database schema.

## Normative terms

The terms MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are interpreted as described in RFC 2119 and RFC 8174.

## Required record types

The canonical model MUST define versioned records for Source, Acquisition, Document, Segment, Artifact, Assertion, Entity, Relationship, Processing Run, Stage Attempt, Review Item, and Review Decision.

## Identity and scope

1. Every canonical record MUST have a stable identifier and workspace identifier.
2. Identifiers MUST remain stable across serialization, indexing, and export.
3. Database row identifiers MUST NOT be exposed as public identities unless they satisfy the public identifier contract.
4. Workspace boundaries MUST be explicit on every canonical record or inherited through an immutable parent relation.
5. Cross-workspace references MUST be rejected.

## Lifecycle and immutability

1. Source identity, acquisition facts, evidence locations, processor provenance, and historical review decisions MUST be append-only.
2. Correctable business meaning MUST be represented through new records, supersession, or status transitions rather than destructive mutation.
3. Records MAY carry tombstone or retention state without erasing required audit metadata.
4. Derived projections MUST NOT become the only copy of canonical information.

## References

References MUST use typed identifiers. A reference MUST declare the expected record type and MUST fail validation when it targets another workspace, an incompatible type, or a missing mandatory record.

## Schema evolution

Canonical records MUST include a schema version. Migrations MUST preserve source evidence and provenance. A migration MUST NOT depend on a search, vector, or graph index as the sole source of canonical data.

## Acceptance criteria

- A source containing multiple logical documents can be represented without duplicating the source bytes.
- Nested segments can address pages, paragraphs, tables, cells, images, attachments, and record rows.
- Historical assertions and decisions remain inspectable after correction and reprocessing.
- The same public record package validates independently of the selected relational adapter.
- Cross-workspace references are rejected deterministically.
