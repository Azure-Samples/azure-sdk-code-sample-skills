---
name: azure-sdk-go-sample-review
description: >-
  Reviews Azure SDK Go code samples for best practices, credential handling,
  idiomatic error handling, context propagation, and documentation compliance.
  Trigger: "review Go Azure SDK sample", "check Go sample", "Azure SDK Go
  review".
status: active
tags:
  - review
  - azure
  - sdk
  - sample
  - check
  - best
  - practices
  - code
  - reviewing
  - credential
category: review
---

## USE FOR

- "review Go Azure SDK sample"
- "check Go sample for best practices"
- "Azure SDK Go code review"
- Reviewing credential handling in Azure SDK Go samples
- Idiomatic error handling and context propagation review for Go Azure SDK samples
- Documentation compliance check for Go Azure SDK samples

## DO NOT USE FOR

- General Go code review unrelated to Azure SDK samples
- Production application code review
- Azure service configuration

## Context

> **Base template:** Inherits from [azure-sdk-sample-review](../azure-sdk-sample-review/SKILL.md) for shared review patterns (credentials, error handling, documentation, infrastructure). This skill adds Go-specific rules below.

Use this skill when reviewing **Go code samples** for Azure SDKs intended for publication as Microsoft Azure samples. Focuses on:

- **Azure SDK client patterns** (`github.com/Azure/azure-sdk-for-go/sdk/*`)
- **Authentication** (`azidentity.NewDefaultAzureCredential`, managed identities)
- **Service-specific best practices** (Cosmos DB, SQL, Storage, Service Bus, Key Vault, AI services)
- **Sample hygiene** (credentials, .gitignore, dependency audit)
- **Documentation accuracy** (README output, troubleshooting, setup instructions)
- **Infrastructure-as-code** (Bicep/Terraform with AVM modules)
- **azd integration** (azure.yaml structure, hooks)
- **Go idioms** (error handling, context propagation, interfaces, goroutine safety)

**Total rules: 75** (11 CRITICAL, 24 HIGH, 32 MEDIUM, 8 LOW)

## Severity Legend

- **CRITICAL**: Security vulnerability or sample will not run. Must fix before any publication.
- **HIGH**: Major quality issue. Fix before merge.
- **MEDIUM**: Best practice violation. Should fix before publication.
- **LOW**: Polish item, nice-to-have improvement.

---

## Quick Pre-Review Checklist (5-Minute Scan)

- [ ] **go.mod**: Uses `github.com/Azure/azure-sdk-for-go/sdk/*` packages (not legacy `services/*`)
- [ ] **Authentication**: Uses `azidentity.NewDefaultAzureCredential` (not connection strings)
- [ ] **.gitignore**: Exists and includes `.env`, `.env.*`, vendor/, binaries
- [ ] **No secrets**: No hardcoded credentials, API keys, or tokens in code
- [ ] **README.md**: Exists with prerequisites, setup steps, and expected output
- [ ] **LICENSE**: MIT license file present (required for Azure Samples)
- [ ] **Security**: `govulncheck ./...` passes with no known vulnerabilities
- [ ] **Go version**: go.mod specifies Go 1.22+
- [ ] **Error handling**: Every error return is checked (`if err != nil`)
- [ ] **Resource cleanup**: Clients properly closed with `defer` statements
- [ ] **go.sum**: Committed (not .gitignored)
- [ ] **Builds**: `go build ./...` and `go vet ./...` pass

---

## Blocker Issues (Auto-Reject)

These issues always block publication:

1. **Hardcoded secrets**â€”Any production credentials, API keys, connection strings, or tokens in code
2. **Missing authentication**â€”No auth implementation or uses insecure methods
3. **No error handling**â€”Unchecked error returns, discarded errors with `_`
4. **Broken imports**â€”Missing dependencies, incorrect import paths
5. **Security vulnerabilities**â€”`govulncheck` shows known CVEs
6. **Missing LICENSE**â€”No LICENSE file at ANY level of repo hierarchy (MIT required). âš ï¸ Check repo root before flagging.
7. **.env file committed**â€”Live credentials in version control. âš ï¸ Verify with `git ls-files .env`
8. **Legacy SDK packages**â€”Uses `github.com/Azure/azure-sdk-for-go/services/*` instead of `sdk/*`

---

## Detailed Rules


### Language-Specific References (Go code examples)

| # | Section | Reference File |
|---|---------|---------------|
| 1 | Project Setup â€” Go | [references/project-setup.md](references/project-setup.md) |
| 2 | SDK Client Patterns â€” Go | [references/sdk-client-patterns.md](references/sdk-client-patterns.md) |
| 3 | AI Services â€” Go | [references/ai-services.md](references/ai-services.md) |
| 4 | Data Services â€” Go | [references/data-services.md](references/data-services.md) |
| 5 | Messaging â€” Go | [references/messaging.md](references/messaging.md) |
| 6 | Key Vault â€” Go | [references/keyvault.md](references/keyvault.md) |
| 7 | Vector Search â€” Go | [references/vector-search.md](references/vector-search.md) |
| 8 | Error Handling â€” Go | [references/error-handling.md](references/error-handling.md) |
| 9 | Data Management â€” Go | [references/data-management.md](references/data-management.md) |
| 10 | Sample Hygiene â€” Go | [references/sample-hygiene.md](references/sample-hygiene.md) |
| 11 | Documentation â€” Go | [references/documentation.md](references/documentation.md) |
| 12 | azd â€” Go | [references/azd.md](references/azd.md) |
| 13 | CI/CD & Testing â€” Go | [references/cicd-testing.md](references/cicd-testing.md) |
| 14 | Go Idioms (Go-unique) | [references/go-idioms.md](references/go-idioms.md) |
| â€” | Comprehensive Checklist & Links | [references/checklist-and-references.md](references/checklist-and-references.md) |

---

## Companion Skills

- **azure-sdk-typescript-sample-review** â€” TypeScript Azure SDK sample review patterns
- **azure-sdk-dotnet-sample-review** â€” .NET 9/10 + Aspire patterns
- **azure-sdk-java-sample-review** â€” Java 17/21 + Spring Boot patterns
- **azure-sdk-python-sample-review** â€” Python 3.9+ + async patterns
- **azure-sdk-rust-sample-review** â€” Rust 2021 edition patterns
- **acrolinx-score-improvement** â€” Article quality, readability, style

---

## Summary

This skill reviews **Azure SDK Go samples** for security, idiomatic Go patterns, Azure SDK best practices, and documentation compliance. 75 rules across 15 categories ensure samples are secure, idiomatic, maintainable, and ready for publication in the Azure Samples organization.

## References

> **References location:** All reference files for this skill live inside the skill directory at `.github/skills/data-plus-ai-sdk-go-sample-review/`. Paths like `references/file.md` resolve to `.github/skills/data-plus-ai-sdk-go-sample-review/references/file.md`. Paths are relative to the skill folder, not the repo root.

