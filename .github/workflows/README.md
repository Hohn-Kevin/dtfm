# GitHub Actions workflows

Automated workflows will be added after the implementation stack and required quality gates are defined.

A workflow must:

- use least-privilege permissions;
- pin third-party actions to reviewed versions or immutable commit SHAs where appropriate;
- avoid exposing secrets to untrusted pull requests;
- document required secrets and permissions;
- fail clearly and reproducibly;
- remain limited to checks relevant to the repository.

No placeholder CI workflow is enabled because the project does not yet have an implementation or selected toolchain to validate.
