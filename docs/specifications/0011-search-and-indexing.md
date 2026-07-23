# Specification 0011: Search and Indexing

- Status: Draft
- Phase: 3

## Problem

DTFM must provide reliable lexical and structural retrieval while allowing optional semantic search without making any index canonical.

## Normative terms

The terms MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are interpreted as described in RFC 2119 and RFC 8174.

## Index classes

The baseline MUST support relational lookup and full-text search. Semantic vector and relationship indexes MAY be added as replaceable projections.

## Requirements

1. Every indexed item MUST reference canonical record identifiers and workspace scope.
2. Index entries MUST record the canonical checkpoint or revision from which they were built.
3. Consumers MUST be able to detect stale, incomplete, unavailable, or rebuilding indexes.
4. Search results MUST expose source and segment references sufficient to retrieve evidence.
5. Semantic results MUST identify the embedding processor, model, version, configuration, and indexed text representation.
6. Deleting an index MUST NOT delete canonical records.
7. Reindexing MUST be safe to repeat and MUST NOT change canonical identifiers.
8. Workspace filters MUST be enforced before results are returned.

## Ranking and completeness

Ranking scores are adapter-specific and MUST NOT be represented as universal probabilities. Results MUST declare the search mode and MAY expose score explanations. Partial indexing MUST be visible to callers.

## Acceptance criteria

- Full-text search returns matching segments with evidence references.
- A stale projection is reported rather than presented as current silently.
- Removing all semantic-index data does not affect canonical assertions or lexical search.
- Rebuilding an index yields references to the same canonical records.
- Queries cannot return another workspace's records.
