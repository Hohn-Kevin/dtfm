# Extensibility Architecture

## Extension types

DTFM supports replaceable components for:

- source adapters;
- format detectors;
- extractors and OCR engines;
- normalizers;
- interpreters and classifiers;
- validators;
- lexical and semantic indexers;
- exporters;
- review policies.

## Registration

Extensions register through explicit typed descriptors. Discovery must not execute arbitrary code merely because a file exists in a directory. The initial implementation may use application-controlled registration; dynamic plugin loading requires a later security-focused ADR.

## Isolation and permissions

Each extension declares required capabilities, including filesystem access, network access, external executables, models, and temporary storage. The host decides whether those capabilities are allowed.

## Namespaces

Core artifact and assertion types use the `dtfm` namespace. Third-party and host-defined types use reverse-domain or otherwise collision-resistant namespaces. Extensions must not silently replace core semantics.

## Compatibility

Extensions declare supported core API versions and their own semantic version. Processor identity and version are persisted with every output so results can be reproduced or invalidated after upgrades.

## Quality requirements

An extension must provide:

- a configuration schema;
- declared inputs and outputs;
- deterministic status;
- failure behavior;
- resource and permission requirements;
- tests using synthetic data;
- license and dependency information;
- documentation of known limitations.
