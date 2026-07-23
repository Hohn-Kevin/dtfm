# Specification 0006: Review Decisions

- Status: Draft
- Phase: 3

## Problem

Low-confidence, conflicting, invalid, or host-selected results require correction without destroying audit history.

## Review item

A review item references the processing run, affected assertions or artifacts, reason code, severity, creation time, current status, and required capabilities for resolution.

## Reason codes

Initial reason categories include:

- low confidence;
- conflicting results;
- ambiguous normalization;
- validation failure;
- unsupported content;
- processor failure;
- host policy requirement.

## Decision types

- confirm;
- reject;
- correct;
- merge entities;
- separate entities;
- defer;
- mark unresolved.

## Required behavior

1. Decisions are append-only audit events.
2. A decision records actor type, actor identifier supplied by the host, timestamp, reason, affected records, and optional replacement value.
3. DTFM does not own user accounts or authorization; the host authorizes the action before submission.
4. Corrections create new provenance-bearing assertions.
5. Concurrent decisions must detect stale state and may not silently overwrite one another.
6. Automated host decisions are distinguished from human decisions.
7. Review APIs never require exposure of unrelated document content.

## Acceptance criteria

- A host can list unresolved items by reason and severity.
- Confirming or correcting an assertion produces an auditable state transition.
- Stale concurrent updates are rejected or explicitly reconciled.
- Historical decisions remain queryable after reprocessing.
- Host identity data is referenced without transferring ownership of user management to DTFM.
