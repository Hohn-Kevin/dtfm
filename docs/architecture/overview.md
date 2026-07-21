# Architecture Overview

## Purpose

DTFM is a local-first, embeddable document understanding engine. It converts heterogeneous source files into structured, traceable, searchable information while preserving the original source and the provenance of every derived result.

The engine is designed for reuse inside larger desktop, server, and self-hosted applications. It must remain useful as a standalone library and must not require a hosted service.

## Architectural goals

DTFM must:

- process documents locally by default;
- preserve original inputs without silent modification;
- separate extraction, normalization, interpretation, indexing, and review;
- expose stable typed interfaces for host applications;
- support deterministic rules and optional machine-assisted processors;
- record provenance, confidence, processor version, and processing time;
- allow individual stages to be replaced without rewriting the complete pipeline;
- support structured records, long-form documents, tables, images, and mixed-content files;
- operate with a lightweight relational core and optional specialized indexes;
- remain suitable for privacy-sensitive and auditable workflows.

## Non-goals

DTFM is not:

- a document-management user interface;
- a financial application;
- a cloud storage service;
- a general-purpose workflow platform;
- an autonomous decision maker;
- a source of legal, financial, medical, or regulatory conclusions;
- dependent on a particular OCR, embedding, language-model, or vector-database vendor.

## Logical layers

1. **Source layer** stores immutable source identity and metadata.
2. **Acquisition layer** validates inputs and creates processing jobs.
3. **Extraction layer** recovers text, layout, tables, images, and metadata.
4. **Normalization layer** converts extracted material into canonical typed values.
5. **Interpretation layer** identifies entities, relationships, classifications, and domain-neutral facts.
6. **Indexing layer** creates lexical, structural, and optional semantic indexes.
7. **Review layer** exposes uncertainty, conflicts, and corrections.
8. **Integration layer** provides APIs, events, and export contracts for host applications.

## Core architectural rule

Every derived value must be traceable to:

- its source document;
- its location within that source;
- the processor and version that produced it;
- the inputs and configuration used;
- an explicit confidence or deterministic status;
- any later correction or superseding result.

The original source and the derivation history are the audit foundation. Derived data may be regenerated; source evidence must not be overwritten.
