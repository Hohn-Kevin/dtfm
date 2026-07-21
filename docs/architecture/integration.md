# Host Integration

## Integration model

DTFM is an engine, not the owning business application. Host applications retain control over users, permissions, domain workflows, presentation, and domain-specific records.

DTFM exposes a typed application boundary suitable for:

- direct Python library use;
- a local worker process for any host stack;
- a command-line interface;
- a self-hosted service adapter;
- background job execution.

Direct library integration is limited to Python hosts. Other runtimes communicate through versioned process-boundary contracts.

## Stable contracts

The public boundary must provide:

- source ingestion and source status;
- processing job creation, cancellation, and inspection;
- document, segment, artifact, assertion, entity, and relationship queries;
- full-text and optional semantic search;
- review queue access and correction submission;
- export of canonical result packages;
- lifecycle and audit events;
- processor and capability discovery.

Public contracts must be versioned and serializable. Pydantic models are the Python representation of those contracts. JSON Schema is the language-neutral schema format, and HTTP-based adapters use OpenAPI descriptions derived from the same contract definitions.

Events and export packages use versioned JSON-compatible envelopes. Internal ORM objects, database sessions, Python-specific runtime objects, vendor SDK objects, and model-specific responses must not cross a process or language boundary.

Contract generation must avoid maintaining independent hand-written schemas that can drift apart. The authoritative contract source and compatibility rules require a dedicated specification before implementation.

## Host-owned extensions

A host may add domain-specific assertions, validators, classifications, and exporters through extension interfaces. These additions must use separate namespaces and may not redefine canonical core meanings silently.

Host-owned domain records remain outside the canonical DTFM model. References between host records and DTFM records use explicit stable identifiers rather than shared ORM entities.

## Event model

Events describe completed facts such as source accepted, processing started, artifact produced, review required, processing completed, and processing failed. Delivery may be in-process initially. Durable queues and remote transports are adapters, not core assumptions.

Event consumers must tolerate duplicate delivery and additive fields. Ordering guarantees, acknowledgement behavior, and replay semantics require explicit adapter specifications.

## Failure isolation

A failed optional processor must not make unrelated extracted results unavailable. Public results must expose completeness and failure information so host applications do not mistake partial processing for complete processing.

## Compatibility

Breaking changes to public models require an accepted ADR, migration notes, and a major version once releases begin. Additive fields should be optional until all supported adapters can provide them.

JSON Schema, OpenAPI, generated clients, and Python models must represent the same public contract version.
