# Privacy and Security Architecture

## Default trust model

Documents are untrusted input. External processors, optional models, plugins, and host adapters are separate trust boundaries. Local execution reduces exposure but does not make processing inherently safe.

## Privacy defaults

- Network access is disabled for core processing by default.
- A processor that requires network access must declare it explicitly.
- Remote processing requires host opt-in for each configured processor class.
- Logs must contain identifiers and diagnostics, not document contents by default.
- Examples, fixtures, and bug reports must use synthetic or properly anonymized data.
- Data retention and deletion are explicit host policies.

## Threats to address

The architecture must account for:

- malformed and adversarial files;
- decompression bombs and oversized containers;
- parser vulnerabilities;
- path traversal and unsafe archive extraction;
- embedded scripts and active content;
- prompt injection inside documents passed to language models;
- data leakage through logs, telemetry, caches, crash reports, and remote APIs;
- malicious or compromised plugins;
- model output being mistaken for verified fact;
- cross-workspace data exposure.

## Required controls

- configurable file, page, member, time, and memory limits;
- isolated temporary directories;
- no execution of embedded document content;
- strict media detection and safe archive handling;
- explicit processor permissions;
- structured redaction-aware logging;
- provenance and confidence on generated assertions;
- validation before host applications treat output as trusted;
- deterministic deletion of temporary artifacts where supported;
- dependency and model provenance tracking.

## Remote processors

Remote processors are adapters and must never be required for baseline operation. Their configuration must define endpoint, data categories sent, authentication method, retention assumptions, timeout, retry policy, and fallback behavior.

## Security posture

DTFM will not claim that an extracted or interpreted result is safe merely because processing completed successfully. Successful parsing means the processor returned a result; trust is established through validation, provenance, review, and host policy.
