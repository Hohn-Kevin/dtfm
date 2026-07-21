# AI-Assisted Development Policy

DTFM permits and expects the responsible use of artificial intelligence in development.

AI assistance does not reduce the quality, security, licensing, or review standards applied to a contribution.

## Core principles

1. Contributors remain responsible for every submitted change.
2. AI-generated output must be understood before it is committed.
3. Generated code must be tested, reviewed, and adapted to the project conventions.
4. Unknown or unverifiable code provenance is not acceptable.
5. Secrets, personal data, confidential documents, and proprietary source code must not be submitted to external AI services without authorization.
6. Architectural decisions must be documented independently of the tool that produced the implementation.

## Contribution requirements

Contributors using AI assistance should:

- verify that the change solves the documented problem;
- review generated code for correctness, security, maintainability, and unnecessary complexity;
- add or update tests;
- verify dependencies and licenses;
- disclose substantial AI assistance in the pull request when it materially affected the implementation;
- avoid presenting generated assumptions as established project decisions.

## Prohibited practices

The following are not acceptable:

- committing code that the contributor cannot explain;
- copying generated code without reviewing its license implications;
- using generated tests that only confirm the generated implementation rather than the specification;
- uploading private user documents, credentials, keys, or sensitive datasets to an external model;
- using AI output as a substitute for security review.

## Project workflow

DTFM follows a specification-first workflow:

1. Define the problem.
2. Document requirements and non-goals.
3. Define interfaces and expected behavior.
4. Define test cases and failure conditions.
5. Implement the specification.
6. Review and verify the result.

The same rules apply whether the implementation is written manually or with AI assistance.
