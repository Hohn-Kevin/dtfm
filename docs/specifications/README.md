# Specifications

Specifications define the normative behavior of DTFM.

## Phase 3 drafts

- [0001: Public contracts](0001-public-contracts.md)
- [0002: Source ingestion](0002-source-ingestion.md)
- [0003: Processing runs](0003-processing-runs.md)
- [0004: Processor contract](0004-processor-contract.md)
- [0005: Provenance and assertions](0005-provenance-and-assertions.md)
- [0006: Review decisions](0006-review-decisions.md)
- [0007: Canonical records](0007-canonical-records.md)
- [0008: Repository and storage](0008-repository-and-storage.md)
- [0009: Extraction and segmentation](0009-extraction-and-segmentation.md)
- [0010: Typed normalization](0010-typed-normalization.md)
- [0011: Search and indexing](0011-search-and-indexing.md)
- [0012: Events and export packages](0012-events-and-export-packages.md)
- [0013: Retention and deletion](0013-retention-and-deletion.md)
- [0014: Security and resource limits](0014-security-and-resource-limits.md)

These drafts define the implementation boundary for the first engine baseline. They are not accepted until reviewed together for consistency, testability, and complete cross-references.

## Required structure

A specification should include:

- problem statement;
- scope and non-goals;
- terminology;
- functional requirements;
- inputs, outputs, and errors;
- security and privacy requirements;
- performance and resource constraints;
- compatibility expectations;
- acceptance criteria and test cases;
- unresolved questions.

Use the terms **MUST**, **MUST NOT**, **SHOULD**, **SHOULD NOT**, and **MAY** deliberately. Specifications using normative language should adopt the RFC 2119 and RFC 8174 interpretation explicitly.

## Acceptance process

A draft may become accepted only when:

1. its requirements do not contradict accepted architecture or another accepted specification;
2. identifiers, states, errors, and public payloads are defined precisely enough to implement;
3. security, privacy, failure, and partial-success behavior are addressed;
4. acceptance criteria can be converted into automated or reproducible tests;
5. unresolved questions that block implementation are closed or deliberately deferred;
6. substantial changes have received maintainer review under `AI_POLICY.md`.

Implementation should begin only after the relevant specification is accepted or explicitly approved as a bounded implementation experiment.
