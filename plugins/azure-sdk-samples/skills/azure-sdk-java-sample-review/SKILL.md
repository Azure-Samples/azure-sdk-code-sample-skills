---
name: azure-sdk-java-sample-review
description: >-
  Reviews Azure SDK Java code samples for best practices, credential handling,
  error patterns, Spring Boot integration, and documentation compliance.
  Trigger: "review Java Azure SDK sample", "check Java sample", "Azure SDK Java
  review".
status: active
tags:
  - review
  - java
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

- "review Java Azure SDK sample"
- "check Java sample for best practices"
- "Azure SDK Java code review"
- Reviewing credential handling in Azure SDK Java samples
- Error pattern analysis for Java Azure SDK samples
- Documentation compliance check for Java Azure SDK samples
- Spring Boot integration review for Azure SDK Java samples

## DO NOT USE FOR

- General Java code review unrelated to Azure SDK samples
- Production application code review
- Azure service configuration

## Context

> **Base template:** Inherits from [azure-sdk-sample-review](../azure-sdk-sample-review/SKILL.md) for shared review patterns (credentials, error handling, documentation, infrastructure). This skill adds Java-specific rules below.

Use this skill when reviewing **Java code samples** for Azure SDKsintended for publication as Microsoft Azure samples. Focuses on:

- **Azure SDK client patterns** (Track 2 `com.azure.*`, client builders, pipeline policies)
- **Authentication** (`DefaultAzureCredential`, managed identities, token management)
- **Service-specific best practices** (Cosmos DB, SQL, Storage, Service Bus, Key Vault, AI services)
- **Sample hygiene** (credentials, build artifacts, dependency audit, .gitignore)
- **Documentation accuracy** (README output, troubleshooting, setup instructions)
- **Infrastructure-as-code** (Bicep/Terraform with AVM modules)
- **azd integration** (azure.yaml structure, hooks, service definitions)
- **Spring Boot / Spring Cloud Azure** integration patterns

---

## Quick Pre-Review Checklist (5-Minute Scan)

- [ ] **pom.xml / build.gradle**: Uses Track 2 Azure SDK packages (`com.azure:*`, not `com.microsoft.azure:*`)
- [ ] **Authentication**: Uses `DefaultAzureCredential` (not connection strings or hardcoded keys)
- [ ] **.gitignore**: Exists and includes `.env`, `target/`, `build/`, `*.class`, `.idea/`
- [ ] **No secrets**: No hardcoded credentials, API keys, or tokens in code
- [ ] **README.md**: Exists with prerequisites, setup steps, and expected output
- [ ] **LICENSE**: MIT license file present (required for Azure Samples)
- [ ] **Security**: No known critical/high CVEs in dependency tree
- [ ] **Java version**: Uses Java 17 or 21 LTS
- [ ] **Error handling**: `catch` blocks present with proper exception hierarchy
- [ ] **Resource cleanup**: Clients properly closed (try-with-resources or finally blocks)
- [ ] **BOM**: Uses `azure-sdk-bom` for version management
- [ ] **No mixed build tools**: Only Maven OR Gradle (not both)
- [ ] **Imports work**: No broken imports, all dependencies declared
- [ ] **Build succeeds**: `mvn compile` or `gradle build` completes without errors
- [ ] **Sample runs**: `mvn exec:java` or `java -jar` executes without crashes

---

## Blocker Issues (Auto-Reject)

These issues always block publication. Samples with any of these must be rejected immediately:

1. **Hardcoded secrets**â€”Any production credentials, API keys, connection strings, or tokens in code
2. **Missing authentication**â€”No auth implementation or uses insecure methods
3. **No error handling**â€”Unchecked exceptions, no try/catch blocks, silent failures
4. **Broken imports**â€”Missing dependencies, incorrect package names, class not found errors
5. **Security vulnerabilities**â€”`mvn dependency-check:check` or Dependabot shows critical/high CVEs
6. **Missing LICENSE**â€”No LICENSE file at ANY level of repo hierarchy (MIT required). âš ï¸ Check repo root before flagging.
7. **.env file committed**â€”Live credentials in version control. âš ï¸ Verify with `git ls-files .env`â€”a .env on disk but in .gitignore is NOT committed.
8. **Track 1 packages**â€”Uses legacy `com.microsoft.azure:*` packages instead of `com.azure:*`

---

## Severity Legend

- **CRITICAL**: Security vulnerability or sample will not run. Must fix before any publication.
- **HIGH**: Major quality issue that will confuse users or cause production failures. Fix before merge.
- **MEDIUM**: Best practice violation. Should fix before publication for maintainability.
- **LOW**: Polish item, nice-to-have improvement.

---

## Detailed Rules


### Language-Specific References (Java code examples)

| # | Section | Reference File |
|---|---------|---------------|
| 1 | Project Setup â€” Java | [references/project-setup.md](references/project-setup.md) |
| 2 | SDK Client Patterns â€” Java | [references/sdk-client-patterns.md](references/sdk-client-patterns.md) |
| 3 | AI Services â€” Java | [references/ai-services.md](references/ai-services.md) |
| 4 | Data Services â€” Java | [references/data-services.md](references/data-services.md) |
| 5 | Messaging â€” Java | [references/messaging.md](references/messaging.md) |
| 6 | Key Vault â€” Java | [references/keyvault.md](references/keyvault.md) |
| 7 | Vector Search â€” Java | [references/vector-search.md](references/vector-search.md) |
| 8 | Error Handling â€” Java | [references/error-handling.md](references/error-handling.md) |
| 9 | Data Management â€” Java | [references/data-management.md](references/data-management.md) |
| 10 | Sample Hygiene â€” Java | [references/sample-hygiene.md](references/sample-hygiene.md) |
| 11 | Documentation â€” Java | [references/documentation.md](references/documentation.md) |
| 12 | Infrastructure â€” Java | [references/infrastructure.md](references/infrastructure.md) |
| 13 | azd â€” Java | [references/azd.md](references/azd.md) |
| 14 | Spring Boot (Java-unique) | [references/spring-boot.md](references/spring-boot.md) |
| 15 | CI/CD & Testing â€” Java | [references/cicd-testing.md](references/cicd-testing.md) |
| 16 | Advanced Configuration (Java-unique) | [references/advanced-config.md](references/advanced-config.md) |

---

## Companion Skills

- **azure-sdk-typescript-sample-review** â€” TypeScript Azure SDK sample review
- **azure-sdk-dotnet-sample-review** â€” .NET 9/10 + Aspire Azure SDK sample review
- **azure-sdk-python-sample-review** â€” Python 3.9+ + async Azure SDK sample review
- **acrolinx-score-improvement** â€” Article quality, readability, style

---

## Summary

This skill enforces **71 rules** (8 CRITICAL, 26 HIGH, 33 MEDIUM, 4 LOW) across Azure SDK Java samples covering authentication, client patterns, data services, AI, messaging, infrastructure, Spring Boot, and documentation. Apply these patterns to ensure samples are secure, accurate, maintainable, and ready for publication.

## References

> **References location:** All reference files for this skill live inside the skill directory at `.github/skills/data-plus-ai-sdk-java-sample-review/`. Paths like `references/file.md` resolve to `.github/skills/data-plus-ai-sdk-java-sample-review/references/file.md`. Paths are relative to the skill folder, not the repo root.

