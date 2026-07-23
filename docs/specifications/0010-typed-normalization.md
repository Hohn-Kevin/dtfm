# Specification 0010: Typed Normalization

- Status: Draft
- Phase: 3

## Problem

Raw extracted strings must be converted into typed values without losing their original representation or hiding ambiguity.

## Normative terms

The terms MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are interpreted as described in RFC 2119 and RFC 8174.

## Required value classes

The initial contract MUST support text, integer, arbitrary-precision decimal, boolean, enumeration, date, time, date-time, range, monetary amount, measurement, identifier, structured address, entity reference, and explicit unknown or ambiguous values.

## General rules

1. Every normalized value MUST retain the original lexical representation and evidence reference.
2. Decimal and monetary values MUST NOT use binary floating-point as their canonical representation.
3. Dates and times MUST retain known precision, timezone status, and unresolved components.
4. Locale assumptions MUST be explicit inputs or recorded processor configuration.
5. A normalizer MUST represent multiple plausible values when evidence is ambiguous instead of selecting one silently.
6. Currency MUST NOT be inferred solely from a symbol when multiple currencies are possible.
7. Identifier normalization MUST preserve leading zeros and declare the identifier scheme when known.
8. Units MUST be stored separately from numeric magnitude.

## Confidence and validation

Deterministic parsing MUST be marked separately from heuristic inference. Validation rules MAY reject or downgrade a normalized value but MUST NOT alter the source representation.

## Acceptance criteria

- `1.234,56` can be parsed under an explicit locale without losing the original text.
- A date containing only month and year retains partial precision.
- Ambiguous numeric and date formats produce alternatives or a review item.
- Monetary arithmetic can be performed without binary floating-point rounding.
- Identifiers such as `00123` retain their significant leading zeros.
