---
name: azure-sdk-python-sample-review
description: >-
  Reviews Azure SDK Python code samples for best practices, credential handling,
  async patterns, error handling, and documentation compliance. Trigger: "review
  Python Azure SDK sample", "check Python sample", "Azure SDK Python review".
status: active
tags:
  - review
  - python
  - azure
  - sdk
  - sample
  - check
  - best
  - practices
  - code
  - reviewing
category: review
---

## USE FOR

- "review Python Azure SDK sample"
- "check Python sample for best practices"
- "Azure SDK Python code review"
- Reviewing credential handling in Azure SDK Python samples
- Error pattern and async pattern analysis for Python Azure SDK samples
- Documentation compliance check for Python Azure SDK samples

## DO NOT USE FOR

- General Python code review unrelated to Azure SDK samples
- Production application code review
- Azure service configuration

## Context

> **Base template:** Inherits from [azure-sdk-sample-review](../azure-sdk-sample-review/SKILL.md) for shared review patterns (credentials, error handling, documentation, infrastructure). This skill adds Python-specific rules below.

Reviews **Python code samples** for Azure SDKsintended for publication as Microsoft Azure samples. Focuses on Track 2 `azure-*` packages, `DefaultAzureCredential`, service-specific patterns (Cosmos DB, SQL, Storage, Service Bus, Key Vault, AI), sample hygiene, documentation accuracy, IaC (Bicep/Terraform), azd integration, and async patterns.

**Total rules: 75** (11 CRITICAL, 23 HIGH, 32 MEDIUM, 9 LOW)

## Severity Legend

- **CRITICAL** = security/won't run
- **HIGH** = confuses users
- **MEDIUM** = best practice
- **LOW** = polish

---

## Quick Pre-Review Checklist (5-Minute Scan)

- [ ] Track 2 Azure SDK packages (`azure-*`)
- [ ] `DefaultAzureCredential` (not connection strings/keys)
- [ ] `.gitignore` includes `.env`, `__pycache__/`, `.venv/`
- [ ] No hardcoded credentials in code
- [ ] README.md with prerequisites, setup, expected output
- [ ] MIT LICENSE file present
- [ ] `pip-audit` passes (no critical/high CVEs)
- [ ] Type hints on public functions
- [ ] `try/except` with specific exception types
- [ ] Clients closed (`with`/`async with`)
- [ ] Pinned `requirements.txt` or lock file committed
- [ ] Single package manager (pip OR poetry OR uv)
- [ ] Python 3.10+ required, 3.12/3.13 target

---

## Blocker Issues (Auto-Reject)

1. **Hardcoded secrets** in code
2. **Missing authentication** or insecure auth methods
3. **No error handling** / bare `except:` blocks
4. **Broken imports** / missing dependencies
5. **Critical/high CVEs** in `pip-audit`
6. **Missing LICENSE** at any repo hierarchy level. âš ï¸ Check repo root first.
7. **.env committed** to git. âš ï¸ Verify with `git ls-files .env`.
8. **Track 1 packages** (legacy pre-Track-2 APIs)

---

## Detailed Rules


### Language-Specific References (Python code examples)

| # | Section | Reference File |
|---|---------|---------------|
| 1 | Project Setup â€” Python | [references/project-setup.md](references/project-setup.md) |
| 2 | SDK Client Patterns â€” Python | [references/sdk-client-patterns.md](references/sdk-client-patterns.md) |
| 3 | AI Services â€” Python | [references/ai-services.md](references/ai-services.md) |
| 4 | Data Services â€” Python | [references/data-services.md](references/data-services.md) |
| 5 | Messaging â€” Python | [references/messaging.md](references/messaging.md) |
| 6 | Key Vault â€” Python | [references/keyvault.md](references/keyvault.md) |
| 7 | Vector Search â€” Python | [references/vector-search.md](references/vector-search.md) |
| 8 | Error Handling â€” Python | [references/error-handling.md](references/error-handling.md) |
| 9 | Data Management â€” Python | [references/data-management.md](references/data-management.md) |
| 10 | Sample Hygiene â€” Python | [references/sample-hygiene.md](references/sample-hygiene.md) |
| 11 | Documentation â€” Python | [references/documentation.md](references/documentation.md) |
| 12 | Infrastructure â€” Python | [references/infrastructure.md](references/infrastructure.md) |
| 13 | azd â€” Python | [references/azd.md](references/azd.md) |
| 14 | Async Patterns (Python-unique) | [references/async-patterns.md](references/async-patterns.md) |
| 15 | CI/CD & Testing â€” Python | [references/cicd-testing.md](references/cicd-testing.md) |

---

## Companion Skills

- **azure-sdk-typescript-sample-review** â€” TypeScript equivalent (shared IaC/azd patterns)
- **azure-sdk-dotnet-sample-review** â€” .NET 9/10 + Aspire
- **azure-sdk-java-sample-review** â€” Java 17/21 + Spring Boot
- **azure-sdk-go-sample-review** â€” Go 1.21+
- **acrolinx-score-improvement** â€” Article quality and style

---

## Summary

75 rules covering Azure SDK Python sample quality: authentication, client patterns, service-specific best practices (AI, Data, Messaging, Key Vault, Vector Search), infrastructure-as-code, async patterns, documentation, and CI/CD. Apply to ensure samples are secure, accurate, and publication-ready.

## References

> **References location:** All reference files for this skill live inside the skill directory at `.github/skills/data-plus-ai-sdk-python-sample-review/`. Paths like `references/file.md` resolve to `.github/skills/data-plus-ai-sdk-python-sample-review/references/file.md`. Paths are relative to the skill folder, not the repo root.

