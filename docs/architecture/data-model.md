# Canonical Data Model

## Design requirements

The canonical model must support both record-oriented inputs and long-form documents. It must preserve source fidelity while allowing typed, searchable projections.

## Core entities

### Source

Represents the immutable identity of an input.

Required properties include a stable source identifier, content hash, media type, size, acquisition metadata, original filename when available, and retention status.

### Document

Represents the logical document discovered in a source. A container may yield multiple documents and multiple sources may later be recognized as versions of one logical document.

### Segment

Represents an addressable region such as a page, paragraph, text span, table, cell, image, attachment, or record row. Segments may be nested and must retain source coordinates or equivalent location information.

### Artifact

Represents output from a processor. Artifacts include extracted text, OCR output, normalized values, images, tables, embeddings, and validation results.

### Assertion

Represents a derived claim about a document or segment. An assertion contains a predicate, typed value or entity reference, evidence references, provenance, confidence, and status.

### Entity

Represents a normalized concept discovered across documents, such as an organization, person, location, account-like identifier, product, event, or document-defined subject. Entity resolution must preserve uncertainty and aliases.

### Relationship

Connects documents, entities, segments, or assertions with a typed relation and evidence.

### Processing Run

Records the source, configuration, processors, versions, timestamps, outcome, errors, and generated artifacts for one execution.

### Review Decision

Records a human or host-system decision to confirm, reject, correct, merge, or supersede an assertion. Decisions are append-only audit events.

## Value representation

Typed values must support at least:

- text with original and normalized forms;
- integers and arbitrary-precision decimals;
- dates, times, and ranges with precision metadata;
- monetary values with currency;
- booleans and enumerations;
- identifiers with scheme information;
- measurements with units;
- structured addresses;
- references to entities, segments, and assertions;
- unknown, ambiguous, and conflicting values.

## Provenance

Provenance is mandatory for derived artifacts and assertions. It includes processor identity, processor version, configuration fingerprint, parent artifacts, evidence locations, creation time, and determinism status.

## Evolution

Persistent records require explicit schema versions. Migrations must be reversible where practical, preserve original evidence, and never depend on a specialized search index as the only copy of canonical information.
