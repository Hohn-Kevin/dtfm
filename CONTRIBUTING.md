# Contributing to DTFM

Thank you for considering a contribution to DTFM.

DTFM is currently in an early specification and architecture phase. Contributions should prioritize clarity, traceability, security, and maintainability over implementation speed.

## Before contributing

Please review:

- [README.md](README.md)
- [AI_POLICY.md](AI_POLICY.md)
- [GOVERNANCE.md](GOVERNANCE.md)
- [SECURITY.md](SECURITY.md)
- [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)

## Ways to contribute

Useful contributions currently include:

- problem definitions and use cases;
- requirements and non-goals;
- architecture proposals;
- threat models and privacy analysis;
- test cases and representative edge cases;
- documentation corrections;
- reproducible bug reports;
- implementation work linked to an accepted specification.

Large implementation pull requests without an agreed specification may be closed or asked to be redesigned.

## Specification-first workflow

Substantial changes should follow this order:

1. Open or reference an issue describing the problem.
2. Document scope, requirements, non-goals, and risks.
3. Define expected inputs, outputs, errors, and acceptance criteria.
4. Record significant architecture decisions in an ADR.
5. Add or update tests.
6. Implement the smallest complete change.
7. Update documentation and the changelog when appropriate.

## Issues

Before opening an issue:

- search for existing issues;
- use the appropriate issue template;
- remove private, confidential, or personal data;
- include minimal reproducible examples when reporting defects;
- explain expected and actual behavior.

Security vulnerabilities must follow [SECURITY.md](SECURITY.md) and must not be reported publicly.

## Branches and commits

Use a focused branch name such as:

- `feat/<short-name>`
- `fix/<short-name>`
- `docs/<short-name>`
- `chore/<short-name>`

Commits should be small, coherent, and written in the imperative style. Conventional Commit prefixes are encouraged, for example:

- `feat: add document source abstraction`
- `fix: reject malformed page ranges`
- `docs: define extraction confidence semantics`
- `test: cover encrypted PDF rejection`

Do not mix unrelated refactoring, formatting, and feature work in one commit.

## Pull requests

A pull request should:

- solve one clearly defined problem;
- reference the relevant issue or specification;
- explain design choices and trade-offs;
- include tests or explain why tests are not applicable;
- disclose breaking changes;
- update documentation;
- disclose substantial AI assistance when it materially affected the change;
- contain no secrets, personal documents, or unlicensed material.

Draft pull requests are welcome for early design review.

## AI-assisted contributions

AI-assisted work is accepted under the requirements in [AI_POLICY.md](AI_POLICY.md).

The contributor must be able to explain the change, validate its behavior, verify dependencies and licensing, and take responsibility for the submitted result.

## Testing and quality

Technology-specific commands will be added once the implementation stack is selected. Until then, every contribution must still be reviewable against explicit acceptance criteria.

Generated tests must verify the specification rather than merely mirror the implementation.

## Dependencies

New dependencies require justification. A proposal should cover:

- why the dependency is needed;
- maintained alternatives considered;
- license compatibility;
- security and privacy implications;
- expected update and migration burden.

## Documentation language

Repository documentation and public code identifiers should be written in English unless a document explicitly targets another language.

## Licensing

By submitting a contribution, you agree that it may be distributed under the Apache License 2.0 used by this repository. Only submit work that you have the right to contribute.
