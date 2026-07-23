# Specification 0014: Security and Resource Limits

- Status: Draft
- Phase: 3

## Problem

Document processing must remain bounded and safe when inputs, processors, models, and adapters are untrusted or compromised.

## Normative terms

The terms MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are interpreted as described in RFC 2119 and RFC 8174.

## Default controls

1. Core processing MUST operate without network access by default.
2. Network, filesystem, external executable, model, and temporary-storage capabilities MUST be declared and authorized explicitly.
3. Embedded scripts and active document content MUST NOT be executed.
4. Archive extraction MUST prevent path traversal, symbolic-link escape, uncontrolled recursion, and decompression bombs.
5. Temporary work MUST use isolated workspace-scoped locations.
6. Logs and errors MUST exclude document content, credentials, and secrets by default.

## Resource policy

Each run MUST receive explicit limits for source bytes, expanded bytes, member count, nesting depth, pages, image dimensions, processor wall time, retry count, temporary storage, and concurrent work. Memory and CPU limits SHOULD be enforced where the deployment adapter supports reliable isolation.

## Processor isolation

Out-of-process execution SHOULD be available for processors with native libraries, external executables, or elevated risk. A processor timeout, crash, or malformed output MUST produce a bounded failure and MUST NOT corrupt canonical state.

## Model-assisted processing

Document instructions are untrusted data. Processors using language models MUST treat prompt injection as a threat, separate system instructions from document content, declare remote data transfer, and never convert model output directly into validated fact without policy-controlled validation.

## Acceptance criteria

- Oversized, deeply nested, and archive-bomb fixtures fail within configured limits.
- A processor cannot use undeclared network access through the supported execution boundary.
- Timeout or crash leaves the run inspectable and canonical state consistent.
- Default logs contain identifiers and diagnostics but no source text.
- Model-generated assertions remain proposed unless validated under an explicit policy.
