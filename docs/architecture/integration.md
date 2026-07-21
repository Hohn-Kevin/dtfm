# Host Integration

## Integration model

DTFM is an engine, not the owning business application. Host applications retain control over users, permissions, domain workflows, presentation, and domain-specific records.

DTFM exposes a typed application boundary suitable for:

- direct library use;
- a local worker process;
- a command-line interface;
- a self-hosted service adapter;
- background job execution.

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

Contracts should use versioned, serializable models. Internal ORM objects, database sessions, vendor SDK objects, and model-specific responses must not cross the public boundary.

## Host-owned extensions

A host may add domain-specific assertions, validators, classifications, and exporters through extension interfaces. These additions must use separate namespaces and may not redefine canonical core meanings silently.

## Event model

Events describe completed facts such as source accepted, processing started, artifact produced, review required, processing completed, and processing failed. Delivery may be in-process initially. Durable queues and remote transports are adapters, not core assumptions.

## Failure isolation

A failed optional processor must not make unrelated extracted results unavailable. Public results must expose completeness and failure information so host applications do not mistake partial processing for complete processing.

## Compatibility

Breaking changes to public models require an accepted ADR, migration notes, and a major version once releases begin. Additive fields should be optional until all supported adapters can provide them.
