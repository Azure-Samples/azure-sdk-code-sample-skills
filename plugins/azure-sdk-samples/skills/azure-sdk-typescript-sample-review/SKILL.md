---
name: azure-sdk-typescript-sample-review
description: >-
  Reviews Azure SDK TypeScript code samples for best practices, credential
  handling, error patterns, and documentation compliance. Trigger: "review
  TypeScript Azure SDK sample", "check TypeScript sample", "Azure SDK TypeScript
  review".
status: active
tags:
  - review
  - azure
  - sdk
  - typescript
  - sample
  - check
  - best
  - practices
  - code
  - reviewing
category: review
---

## USE FOR

- "review Azure SDK TypeScript sample"
- "check TypeScript sample for best practices"
- "Azure SDK TypeScript code review"
- Reviewing credential handling in Azure SDK TypeScript samples
- Error pattern analysis for TypeScript Azure SDK samples
- Documentation compliance check for TypeScript Azure SDK samples

## DO NOT USE FOR

- General TypeScript code review unrelated to Azure SDK samples (use typescript-review)
- Production application code review
- Azure service configuration

## Context

> **Base template:** Inherits from [azure-sdk-sample-review](../azure-sdk-sample-review/SKILL.md) for shared review patterns (credentials, error handling, documentation, infrastructure). This skill adds TypeScript-specific rules below.

Reviews **TypeScript code samples** for Azure SDKsintended for publication as Microsoft Azure samples. Focuses on:

- **Azure SDK client patterns** (Track 2 `@azure/*` packages, client construction, pipeline options)
- **Authentication** (`DefaultAzureCredential`, managed identities, token management)
- **Service-specific best practices** (Cosmos DB, SQL, Storage, Service Bus, Key Vault, AI services)
- **Sample hygiene** (credentials, build artifacts, dependency audit, .gitignore)
- **Documentation accuracy** (README output, troubleshooting, setup instructions)
- **Infrastructure-as-code** (Bicep/Terraform with AVM modules, API versions, parameter validation)
- **azd integration** (azure.yaml structure, hooks, service definitions)

**Total rules: 63** (10 CRITICAL, 21 HIGH, 26 MEDIUM, 6 LOW)

---

## Severity Legend

- **CRITICAL**: Security vulnerability or sample will not run. Must fix before publication.
- **HIGH**: Major quality issue causing user confusion or production failures. Fix before merge.
- **MEDIUM**: Best practice violation. Fix before publication for maintainability.
- **LOW**: Polish item, nice-to-have improvement.

---

## Quick Pre-Review Checklist (5-Minute Scan)

- [ ] Uses Track 2 Azure SDK packages (`@azure/*`, not `azure-*`)
- [ ] Uses `DefaultAzureCredential` (not connection strings or hardcoded keys)
- [ ] `.gitignore` includes `.env`, `node_modules/`, `dist/`
- [ ] No hardcoded credentials, API keys, or tokens in code
- [ ] README.md exists with prerequisites, setup steps, and expected output
- [ ] LICENSE (MIT) present at some level of repo hierarchy
- [ ] `npm audit` passes with no critical/high vulnerabilities
- [ ] `strict: true` in tsconfig.json
- [ ] `catch` blocks with type-safe error narrowing
- [ ] Resource cleanup (finally blocks or Symbol.asyncDispose)
- [ ] package-lock.json committed, no mixed package managers
- [ ] Build succeeds (`npm run build`) and sample runs (`npm start`)

---

## Blocker Issues (Auto-Reject)

1. **Hardcoded secrets** â€” Any credentials, API keys, connection strings, or tokens in code
2. **Missing authentication** â€” No auth or uses insecure methods
3. **No error handling** â€” Uncaught promises, no try/catch, silent failures
4. **Broken imports** â€” Missing dependencies, incorrect import paths
5. **Security vulnerabilities** â€” `npm audit` shows critical or high CVEs
6. **Missing LICENSE** â€” No LICENSE file at ANY level of repo hierarchy (MIT required). âš ï¸ Check repo root before flagging.
7. **.env file committed** â€” Live credentials in version control. âš ï¸ Verify with `git ls-files .env`.
8. **Track 1 packages** â€” Uses legacy `azure-*` instead of `@azure/*`

---

## Detailed Rules


### Language-Specific References (TypeScript code examples)

| # | Section | Reference File |
|---|---------|---------------|
| 1 | Project Setup â€” TypeScript | [references/project-setup.md](references/project-setup.md) |
| 2 | SDK Client Patterns â€” TypeScript | [references/sdk-client-patterns.md](references/sdk-client-patterns.md) |
| 3 | AI Services â€” TypeScript | [references/ai-services.md](references/ai-services.md) |
| 4 | Data Services â€” TypeScript | [references/data-services.md](references/data-services.md) |
| 5 | Messaging â€” TypeScript | [references/messaging.md](references/messaging.md) |
| 6 | Key Vault â€” TypeScript | [references/keyvault.md](references/keyvault.md) |
| 7 | Vector Search â€” TypeScript | [references/vector-search.md](references/vector-search.md) |
| 8 | Error Handling â€” TypeScript | [references/error-handling.md](references/error-handling.md) |
| 9 | Data Management â€” TypeScript | [references/data-management.md](references/data-management.md) |
| 10 | Sample Hygiene â€” TypeScript | [references/sample-hygiene.md](references/sample-hygiene.md) |
| 11 | Documentation â€” TypeScript | [references/documentation.md](references/documentation.md) |
| 12 | Infrastructure â€” TypeScript | [references/infrastructure.md](references/infrastructure.md) |
| 13 | azd â€” TypeScript | [references/azd.md](references/azd.md) |
| 14 | CI/CD & Testing â€” TypeScript | [references/cicd-testing.md](references/cicd-testing.md) |
| â€” | Comprehensive Checklist | [references/checklist.md](references/checklist.md) |
| â€” | Reference Links | [references/reference-links.md](references/reference-links.md) |

---

## Companion Skills

- **acrolinx-score-improvement** â€” Article quality, readability, style, terminology
- **typescript-review** â€” General TypeScript patterns (not Azure SDK specific)

---

## Summary

63 rules (10 CRITICAL, 21 HIGH, 26 MEDIUM, 6 LOW) covering Azure SDK TypeScript sample review across authentication, data services, AI, messaging, infrastructure, documentation, and hygiene. Apply to ensure samples are secure, accurate, maintainable, and ready for publication.

## References

> **References location:** All reference files for this skill live inside the skill directory at `.github/skills/data-plus-ai-sdk-typescript-sample-review/`. Paths like `references/file.md` resolve to `.github/skills/data-plus-ai-sdk-typescript-sample-review/references/file.md`. Paths are relative to the skill folder, not the repo root.

