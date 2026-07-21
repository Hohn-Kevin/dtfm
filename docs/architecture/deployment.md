# Deployment Architecture

## Supported shapes

DTFM is designed to support three deployment shapes without changing the domain model:

1. **Embedded library** inside a host application.
2. **Local worker process** with a typed IPC or local API boundary.
3. **Self-hosted service** for a trusted private network or single organization.

The embedded and local-worker shapes are first-class. A public multi-tenant cloud service is not a baseline requirement.

## Runtime baseline

The planned baseline runtime is Python with typed models and validation through Pydantic. This aligns with document-processing ecosystems while keeping public contracts explicit and serializable.

SQLite is the baseline relational store. Specialized vector storage remains optional and replaceable.

These choices are architectural defaults, not permission to expose framework-specific objects through public interfaces.

## Concurrency

Processing jobs may run asynchronously, but concurrency must be bounded. The host controls worker count, memory limits, timeouts, and cancellation. Database writes remain transactional and processing stages must tolerate retries.

## Packaging

The core should be distributable as a Python package. Optional capabilities such as OCR backends, specific file formats, embeddings, or service adapters should use extras or separate packages to avoid forcing large dependencies on every installation.

## Configuration

Configuration is layered in this order:

1. secure host-provided runtime values;
2. workspace configuration;
3. processor configuration;
4. documented defaults.

Secrets must not be stored in normal project configuration files or serialized processing records.

## Portability

The baseline should work on current Windows and Linux environments. Platform-specific processors must declare limitations and provide a clear capability check rather than failing deep inside a job.
