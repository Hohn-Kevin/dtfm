# Specification 0013: Retention and Deletion

- Status: Draft
- Phase: 3

## Problem

DTFM must apply explicit retention and deletion policies across source bytes, canonical records, temporary data, and rebuildable projections without leaving misleading orphan results.

## Normative terms

The terms MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are interpreted as described in RFC 2119 and RFC 8174.

## Policy requirements

1. Retention policy MUST be supplied or selected explicitly for each workspace and acquisition.
2. DTFM MUST distinguish deletion of source bytes, derived artifacts, canonical metadata, temporary files, and projections.
3. Deletion MUST be scoped to one workspace.
4. Legal or host-defined holds MAY block deletion and MUST produce an auditable outcome.
5. A deletion request MUST be idempotent.
6. Temporary artifacts MUST have bounded lifetime and cleanup state.

## Referential behavior

Deleting evidence MUST NOT leave dependent assertions appearing fully evidenced. Affected records MUST be deleted, tombstoned, redacted, or marked evidence-unavailable according to the selected policy. Historical identifiers MAY remain as tombstones when required for audit integrity.

## Projection cleanup

Search, semantic, relationship, cache, and export projections MUST be removed or invalidated after canonical deletion. Projection cleanup failures MUST remain visible and retryable.

## Verification

Deletion outcomes MUST record scope, policy, affected record counts, blocked items, failed adapters, and completion status without logging deleted content.

## Acceptance criteria

- Repeating a completed deletion request has no additional destructive effect.
- Deleting one workspace does not affect another workspace.
- Removed source bytes cannot still be returned through a stale search or blob reference.
- Assertions with removed evidence are not presented as normally verified.
- Failed projection cleanup is detectable and can be retried.
