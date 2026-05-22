---
name: azure-sdk-dotnet-sample-review
description: >-
  Reviews Azure SDK .NET code samples for best practices, credential handling,
  error patterns, Aspire orchestration, and documentation compliance. Trigger:
  "review .NET Azure SDK sample", "check dotnet sample", "Azure SDK .NET
  review".
status: active
tags:
  - review
  - net
  - azure
  - sdk
  - sample
  - check
  - dotnet
  - best
  - practices
  - code
category: review
---

## USE FOR

- "review .NET Azure SDK sample"
- "check dotnet sample for best practices"
- "Azure SDK .NET code review"
- Reviewing credential handling in Azure SDK .NET samples
- Error pattern analysis for .NET Azure SDK samples
- Documentation compliance check for .NET Azure SDK samples
- Aspire orchestration review for Azure SDK .NET samples

## DO NOT USE FOR

- General .NET code review unrelated to Azure SDK samples
- Production application code review
- Azure service configuration

## Context

> **Base template:** Inherits from [azure-sdk-sample-review](../azure-sdk-sample-review/SKILL.md) for shared review patterns (credentials, error handling, documentation, infrastructure). This skill adds .NET-specific rules below.

Reviews **.NET code samples** for Azure SDKs intended for publication as Microsoft Azure samples. Covers: Azure SDK client patterns (Track 2 `Azure.*`), authentication (`DefaultAzureCredential`), service-specific best practices, .NET Aspire orchestration, sample hygiene, documentation accuracy, infrastructure-as-code, and azd integration.

**Total rules: 71** (9 CRITICAL, 25 HIGH, 33 MEDIUM, 4 LOW)

---

## Quick Pre-Review Checklist (5-Minute Scan)

- [ ] **.csproj**: Track 2 packages (`Azure.*`, exception: `Microsoft.Azure.Cosmos`)
- [ ] **Auth**: `DefaultAzureCredential` (not connection strings/hardcoded keys)
- [ ] **.gitignore**: Includes `bin/`, `obj/`, `.env`, `appsettings.Development.json`
- [ ] **No secrets**: No hardcoded credentials, API keys, or tokens
- [ ] **README.md**: Prerequisites, setup steps, expected output
- [ ] **LICENSE**: MIT license present
- [ ] **Security**: No critical/high CVEs (`dotnet list package --vulnerable`)
- [ ] **Nullable**: `<Nullable>enable</Nullable>`
- [ ] **Error handling**: Proper exception types, troubleshooting hints
- [ ] **Cleanup**: `await using` / `IAsyncDisposable`
- [ ] **Lock file**: `packages.lock.json` committed when enabled
- [ ] **Target**: `net8.0`, `net9.0`, or `net10.0`
- [ ] **Builds**: `dotnet build` succeeds

---

## Blocker Issues (Auto-Reject)

1. **Hardcoded secrets** â€” credentials, API keys, connection strings in code
2. **Missing authentication** â€” no auth or insecure methods
3. **No error handling** â€” unhandled exceptions, silent failures
4. **Broken references** â€” missing NuGet packages, build errors
5. **Security vulnerabilities** â€” critical/high CVEs
6. **Missing LICENSE** â€” no MIT LICENSE at any repo level
7. **Secrets committed** â€” live credentials tracked in git
8. **Track 1 packages** â€” legacy `Microsoft.Azure.*` (exception: `Microsoft.Azure.Cosmos` v3.x is current)

---

## Severity Legend

- **CRITICAL**: Security vulnerability or sample won't run. Block publication.
- **HIGH**: Major quality issue causing confusion or production failures. Fix before merge.
- **MEDIUM**: Best practice violation. Fix before publication.
- **LOW**: Polish item. Address during review cycles.

---

## Detailed Rules


### Language-Specific References (.NET code examples)

| # | Section | Reference File |
|---|---------|---------------|
| 1 | Project Setup â€” .NET | [references/project-setup.md](references/project-setup.md) |
| 2 | SDK Client Patterns â€” .NET | [references/sdk-client-patterns.md](references/sdk-client-patterns.md) |
| 3 | AI Services â€” .NET | [references/ai-services.md](references/ai-services.md) |
| 4 | Data Services â€” .NET | [references/data-services.md](references/data-services.md) |
| 5 | Messaging â€” .NET | [references/messaging.md](references/messaging.md) |
| 6 | Key Vault â€” .NET | [references/keyvault.md](references/keyvault.md) |
| 7 | Vector Search â€” .NET | [references/vector-search.md](references/vector-search.md) |
| 8 | Error Handling â€” .NET | [references/error-handling.md](references/error-handling.md) |
| 9 | Data Management â€” .NET | [references/data-management.md](references/data-management.md) |
| 10 | Sample Hygiene â€” .NET | [references/sample-hygiene.md](references/sample-hygiene.md) |
| 11 | Documentation â€” .NET | [references/documentation.md](references/documentation.md) |
| 12 | Infrastructure â€” .NET | [references/infrastructure.md](references/infrastructure.md) |
| 13 | azd â€” .NET | [references/azd.md](references/azd.md) |
| 14 | .NET Aspire, DI & Functions (.NET-unique) | [references/aspire-di-functions.md](references/aspire-di-functions.md) |
| 15 | CI/CD & Testing â€” .NET | [references/cicd-testing.md](references/cicd-testing.md) |

---

## Companion Skills

- **azure-sdk-typescript-sample-review** â€” TypeScript Azure SDK sample review
- **azure-sdk-java-sample-review** â€” Java 17/21 + Spring Boot
- **azure-sdk-python-sample-review** â€” Python 3.9+ async
- **acrolinx-score-improvement** â€” Article quality and style

---

## Summary

Applies 71 rules across project setup, Azure SDK clients, AI/data/messaging services, Aspire orchestration, infrastructure, and documentation to ensure .NET samples are secure, accurate, and publication-ready.

## References

> **References location:** All reference files for this skill live inside the skill directory at `.github/skills/data-plus-ai-sdk-dotnet-sample-review/`. Paths like `references/file.md` resolve to `.github/skills/data-plus-ai-sdk-dotnet-sample-review/references/file.md`. Paths are relative to the skill folder, not the repo root.

