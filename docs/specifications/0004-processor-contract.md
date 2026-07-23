# Specification 0004: Processor Contract

- Status: Draft
- Phase: 3

## Problem

Extractors, OCR engines, normalizers, interpreters, validators, indexers, and exporters need one auditable extension contract.

## Descriptor

Every processor declares:

- stable identifier and semantic version;
- processor category;
- accepted and produced artifact types;
- configuration schema and defaults;
- supported contract versions;
- determinism status;
- filesystem, network, executable, model, and temporary-storage requirements;
- resource estimates and hard limits where known;
- dependency, license, and model provenance;
- supported platforms and capability checks.

## Execution input

A processor receives immutable input references, validated configuration, processing context, cancellation signal, resource policy, and a scoped artifact writer. It must not receive unrestricted database or host-application access.

## Execution output

A processor returns typed artifacts, assertions, diagnostics, metrics, and an outcome status. Every derived output references evidence and records processor identity, version, configuration fingerprint, parent artifacts, creation time, and determinism status.

## Required behavior

1. Importing or discovering a processor must not execute document-processing code.
2. Processors may not silently request undeclared capabilities.
3. Network access is denied unless both declared and allowed by host policy.
4. Temporary files use isolated locations and are cleaned according to policy.
5. Processors represent ambiguity and failure explicitly.
6. Generated assertions are not automatically treated as verified facts.
7. Processor failures use stable error categories and must not leak secrets or document content into default logs.

## Acceptance criteria

- A processor can be inspected before activation.
- The host can reject a processor because of network or executable requirements.
- Two versions of one processor produce distinguishable provenance.
- A processor can be tested with synthetic fixtures without a full host application.
- Undeclared outputs or capabilities fail validation.
