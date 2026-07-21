# Processing Pipeline

## Pipeline stages

### 1. Ingest

The ingest stage accepts a file, byte stream, or host-provided source reference. It validates limits, computes a content hash, records source metadata, and creates an idempotent processing job.

### 2. Detect

The detection stage determines the media type, container format, encoding, and available native content. File extensions are hints, not authoritative evidence.

### 3. Extract

One or more extractors produce artifacts such as:

- text spans;
- page and region coordinates;
- table cells and structure;
- embedded images;
- document metadata;
- attachments or container members.

Native extraction is preferred. OCR is a fallback or supplemental processor, not an unconditional first step.

### 4. Normalize

Normalization converts raw strings into canonical typed values without discarding the original representation. Examples include dates, decimal numbers, currencies, identifiers, addresses, names, and normalized whitespace.

Normalization must be locale-aware and must represent ambiguity rather than guessing silently.

### 5. Interpret

Interpreters derive domain-neutral entities, relationships, classifications, and facts. Multiple interpretations may coexist when evidence is ambiguous or processors disagree.

### 6. Validate

Validators apply structural constraints, consistency checks, and deterministic rules. They may accept, reject, downgrade, or flag derived results but must not rewrite source evidence.

### 7. Index

Indexers produce:

- relational lookup data;
- full-text search data;
- optional semantic vectors;
- optional relationship indexes.

Specialized indexes are projections and may be rebuilt from canonical records.

### 8. Review

Review queues contain low-confidence values, conflicts, unsupported formats, failed processors, and host-defined validation cases. Human corrections create new provenance-bearing assertions and never alter historical evidence invisibly.

### 9. Export and notify

The integration layer exposes stable result objects and emits lifecycle events. Host applications decide how results are presented, combined with domain data, or stored outside the engine.

## Execution properties

The pipeline must be:

- idempotent for identical source, configuration, and processor versions;
- restartable after interruption;
- observable through structured events and logs;
- bounded by configurable resource limits;
- capable of partial success;
- explicit about skipped and failed stages;
- safe to reprocess when processors or specifications change.

## Processor contract

Every processor declares:

- a stable identifier and semantic version;
- accepted artifact types;
- produced artifact types;
- configuration schema;
- determinism status;
- resource requirements;
- external network requirements;
- licensing and model metadata where applicable.
