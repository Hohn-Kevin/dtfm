# Security Policy

DTFM processes documents that may contain sensitive or personal information. Security and privacy reports are taken seriously.

## Supported versions

DTFM has not published a stable release. No version is currently supported for production use or guaranteed to receive security updates.

This policy will be updated when the first supported release line is published.

## Reporting a vulnerability

Do not disclose suspected vulnerabilities in public issues, discussions, pull requests, or social media.

Use GitHub's private vulnerability reporting feature for this repository when available. If it is not available, contact the maintainer privately through a contact method listed on the repository owner's GitHub profile.

Include, where possible:

- a clear description of the vulnerability;
- affected components, versions, or commits;
- steps to reproduce;
- proof-of-concept material that does not expose real user data;
- the expected security impact;
- suggested mitigations, if known.

Do not include credentials, personal documents, confidential data, or third-party secrets in a report.

## Response expectations

The maintainer will aim to:

- acknowledge a valid report within 7 calendar days;
- provide an initial assessment within 14 calendar days;
- coordinate remediation and disclosure based on severity and project maturity.

These targets are goals rather than service-level guarantees, especially while the project is maintained by a small team.

## Safe research expectations

Security research should avoid:

- accessing or modifying data that does not belong to you;
- disrupting systems or services;
- social engineering;
- privacy violations;
- publishing details before a coordinated disclosure date.

## Security principles

DTFM development should follow these principles:

- local-first processing by default where technically feasible;
- explicit trust boundaries;
- least-privilege access;
- safe handling of untrusted document input;
- bounded resource consumption;
- dependency and license review;
- no secrets or personal test documents in the repository;
- documented security assumptions and failure modes.

## Sensitive test data

Use synthetic, anonymized, or explicitly licensed fixtures. Real private documents must not be committed, attached to public issues, or uploaded to external AI services without authorization.
