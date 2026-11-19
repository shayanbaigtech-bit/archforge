# ArchForge technical design

**Development Status: In Progress** — implementation plan.

## Scope and approach

Capture requirements as structured constraints, select from a small catalog of vetted AWS patterns, and generate a diagram plus Terraform draft. Validation and human review gate every output; no automatic deployment is planned for the MVP.

### Input and intermediate model
Inputs include workload type, region, traffic band, data classification, availability target, and budget ceiling. The validated intermediate model lists AWS resources, connections, constraints, and the reason each pattern was chosen.

### Generation boundary
The MVP supports one bounded reference workload, such as a public API with a database. Modules come from a versioned local catalog. A language model may extract candidate requirements, but cannot invent Terraform resources outside the catalog.

### Validation
Run format, init without backend, validate, security scanning, and custom assertions for encryption, network exposure, and multi-AZ needs. Show failed constraints beside the generated design. Cost is an estimate with explicit usage assumptions.

### Evaluation
Use a fixed requirements suite. Measure valid Terraform rate, constraint satisfaction, security findings, and reviewer corrections. Compare generated output with the same reference architecture built manually.

## Quality and operating requirements

Treat all generated infrastructure as untrusted until reviewed. Use no live cloud credentials in the design pipeline, pin module versions, and require explicit approval before any future apply action.

The first implementation should include structured logs, explicit failure handling, bounded retries where external services are involved, and a reproducible local run path. Proposed services and models may change after the baseline is measured.
