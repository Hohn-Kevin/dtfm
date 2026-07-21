# DTFM

> Open-source semantic document analysis engine.

DTFM is an early-stage project for extracting, structuring, and analyzing meaning from documents while keeping processing transparent, auditable, and suitable for local-first use.

## Project status

DTFM is currently in the **foundation and specification phase**. The architecture, supported formats, implementation language, public APIs, and compatibility guarantees have not yet been finalized.

Do not use the project for production workloads at this stage.

## Goals

DTFM aims to provide:

- a modular document-processing pipeline;
- structured extraction from heterogeneous documents;
- semantic analysis with traceable results;
- local-first processing as a primary deployment model;
- extensible parsers, analyzers, and exporters;
- documented behavior that can be tested independently of a particular AI model.

## Non-goals

At the current stage, DTFM does not promise:

- production stability;
- a hosted service;
- support for every document type;
- perfect extraction or interpretation;
- legal, financial, medical, or regulatory advice based on analyzed documents.

## Development approach

DTFM follows a **specification-first, AI-assisted** workflow:

1. Define the problem and scope.
2. Document requirements and non-goals.
3. Define interfaces, expected behavior, and failure cases.
4. Define tests and acceptance criteria.
5. Implement the specification.
6. Review, verify, and document the result.

AI assistance is permitted, but contributors remain responsible for every submitted change. See [AI_POLICY.md](AI_POLICY.md).

## Documentation

Project documentation is organized under [`docs/`](docs/):

- [`architecture/`](docs/architecture/) for system design;
- [`algorithms/`](docs/algorithms/) for documented algorithms and heuristics;
- [`specifications/`](docs/specifications/) for normative requirements;
- [`decisions/`](docs/decisions/) for architecture decision records;
- [`roadmap/`](docs/roadmap/) for planned milestones.

## Contributing

The project is not yet accepting broad implementation contributions because the core architecture has not been defined. Discussion, review, threat modeling, requirements, test cases, and documentation improvements are welcome.

Read [CONTRIBUTING.md](CONTRIBUTING.md) before opening an issue or pull request.

## Security

Do not report security vulnerabilities in public issues. Follow the process in [SECURITY.md](SECURITY.md).

## Governance

Project roles, decision-making, and maintainer responsibilities are documented in [GOVERNANCE.md](GOVERNANCE.md).

## License

DTFM is licensed under the [Apache License 2.0](LICENSE).

Unless explicitly stated otherwise, contributions submitted to this repository are provided under the same license.
