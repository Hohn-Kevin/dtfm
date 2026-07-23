# Specification 0005: Provenance and Assertions

- Status: Draft
- Phase: 3

## Problem

Derived information must remain explainable, reviewable, and reproducible without modifying the original evidence.

## Assertion requirements

An assertion contains:

- stable identifier;
- namespaced predicate;
- typed value or entity reference;
- one or more evidence references;
- processor provenance;
- confidence or deterministic status;
- lifecycle status;
- creation time;
- optional superseded assertion reference.

## Evidence references

Evidence identifies the source, logical document, segment, and location within that segment. Location may use text offsets, page coordinates, table coordinates, record fields, or another format-specific locator.

## Status values

- `proposed`
- `validated`
- `rejected`
- `corrected`
- `superseded`
- `conflicted`

Generated output begins as proposed unless a deterministic validator with an accepted policy establishes another status.

## Rules

1. An assertion without evidence is invalid unless explicitly identified as host-supplied metadata.
2. Confidence values identify processor certainty and are not universal probabilities unless the processor documents calibration.
3. Conflicting assertions may coexist.
4. Corrections create new assertions and review decisions rather than mutating historical values.
5. Supersession preserves the complete chain.
6. Canonical exports include provenance sufficient to explain each result.
7. Deleting source evidence follows retention policy and must not leave apparently verified orphan assertions.

## Acceptance criteria

- Every extracted or interpreted value can be traced to a source location.
- A correction leaves the original assertion and review history inspectable.
- Conflicting processor outputs remain distinguishable.
- Reprocessing with a new processor version does not erase previous results.
- Consumers can filter by lifecycle status and completeness.
