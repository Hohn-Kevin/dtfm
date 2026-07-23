# Specification 0009: Extraction and Segmentation

- Status: Draft
- Phase: 3

## Problem

DTFM must recover text, layout, tables, images, metadata, attachments, and record structure while retaining precise evidence locations.

## Normative terms

The terms MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are interpreted as described in RFC 2119 and RFC 8174.

## Extraction order

1. Native extraction SHOULD be attempted before OCR when trustworthy native content is available.
2. OCR MAY supplement or replace native extraction for selected regions.
3. Conflicting native and OCR results MUST remain distinguishable.
4. File extensions MUST NOT override content-based format detection.

## Segment model

A segment MUST declare its type, parent when nested, stable identifier within the processing result, ordering, and evidence locator. Locators MAY use byte ranges, page numbers, text offsets, bounding polygons, table coordinates, record fields, archive-member paths, or format-specific structured data.

## Source fidelity

Extracted text MUST preserve an original form. Normalized text MAY be stored separately. Processors MUST NOT silently rewrite source text, page order, table structure, or attachment identity.

## Containers and attachments

Archive members and embedded attachments MUST be processed under inherited depth, member-count, byte, and time limits. Member paths MUST be normalized and MUST NOT escape isolated storage.

## Partial extraction

Unsupported regions, malformed pages, and failed attachments MUST produce explicit diagnostics. A processor MAY return partial output when the result declares missing regions and completeness status.

## Acceptance criteria

- Text can be traced to page and region or an equivalent source locator.
- A table preserves row, column, span, and cell relationships when the source exposes them.
- OCR output is distinguishable from native text and carries processor provenance.
- A failed attachment does not erase successfully extracted parent content.
- Unsafe archive paths and depth-limit violations are rejected.
