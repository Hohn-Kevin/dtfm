# DTFM Documentation

This directory contains the durable technical record of DTFM.

## Structure

- `architecture/`: system boundaries, components, data flow, and trust boundaries.
- `algorithms/`: algorithms, heuristics, complexity, assumptions, and evaluation criteria.
- `specifications/`: normative behavior, interfaces, requirements, and acceptance criteria.
- `decisions/`: Architecture Decision Records.
- `roadmap/`: milestones and planning documents that do not override specifications.

## Authority

When documents conflict, use the following order unless explicitly stated otherwise:

1. accepted specifications;
2. accepted Architecture Decision Records;
3. architecture documentation;
4. implementation documentation;
5. roadmap documents.

The implementation must not silently redefine a specification. Differences must be resolved by changing either the implementation or the documented decision through review.

## Writing requirements

Documentation should distinguish clearly between:

- facts and assumptions;
- normative requirements and examples;
- current behavior and planned behavior;
- security boundaries and trusted components;
- accepted decisions and open questions.

Use synthetic examples and never commit private documents or personal data.
