# Specification 0012: Events and Export Packages

- Status: Draft
- Phase: 3

## Problem

Hosts need stable lifecycle notifications and portable result packages without depending on internal Python objects or database schemas.

## Normative terms

The terms MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are interpreted as described in RFC 2119 and RFC 8174.

## Event requirements

1. Events MUST use the public message envelope.
2. Events MUST describe completed facts rather than commands.
3. Event identifiers MUST support duplicate detection.
4. Consumers MUST tolerate duplicate delivery and additive optional fields.
5. Ordering guarantees MUST be declared by each transport adapter.
6. Events MUST NOT include document contents by default.
7. A lifecycle event MUST reference the affected workspace, source, run, stage, or canonical record as applicable.

## Export package requirements

A canonical export package MUST declare contract version, package identifier, workspace scope, creation time, selection criteria, completeness, included record types, source-evidence policy, and checksums.

Exports MUST preserve stable identifiers, typed values, provenance, assertion status, supersession links, and review decisions for included records. An export MUST declare omitted source bytes, redacted fields, unresolved references, and partial processing.

## Import and replay boundary

Export does not automatically imply lossless re-import. A package advertised as portable backup MUST satisfy a separate backup profile and include all required canonical dependencies. Event replay MUST NOT be treated as canonical reconstruction unless an adapter explicitly implements and verifies that profile.

## Acceptance criteria

- A non-Python consumer validates events and exports using generated schemas.
- Duplicate events can be ignored safely by identifier.
- An export makes omissions and partial results explicit.
- Included assertions remain traceable to included or explicitly external evidence references.
- Internal ORM and vendor-specific objects never appear in serialized output.
