---
name: azure-sdk-rust-sample-review
description: >-
  Reviews Azure SDK Rust code samples for best practices, credential handling,
  ownership patterns, async runtime usage, error propagation, and documentation
  compliance. Trigger: "review Rust Azure SDK sample", "check Rust sample",
  "Azure SDK Rust review".
status: active
tags:
  - review
  - rust
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

- "review Rust Azure SDK sample"
- "check Rust sample for best practices"
- "Azure SDK Rust code review"
- Reviewing credential handling in Azure SDK Rust samples
- Ownership patterns and async runtime review for Rust Azure SDK samples
- Error propagation and documentation compliance check for Rust Azure SDK samples

## DO NOT USE FOR

- General Rust code review unrelated to Azure SDK samples
- Production application code review
- Azure service configuration

## Context

> **Base template:** Inherits from [azure-sdk-sample-review](../azure-sdk-sample-review/SKILL.md) for shared review patterns (credentials, error handling, documentation, infrastructure). This skill adds Rust-specific rules below.

Use this skill when reviewing **Rust code samples** for Azure SDKsintended for publication as Microsoft Azure samples. Focuses on Azure SDK-specific concerns: `azure_*` crates, `DefaultAzureCredential`, service-specific patterns, sample hygiene, documentation accuracy, infrastructure-as-code, azd integration, and Rust idioms (ownership, borrowing, error propagation, async runtimes, RAII cleanup).

> **âš ï¸ SDK Maturity Note:** The Azure SDK for Rust is still evolving. Many crates are in preview/alpha. This skill focuses on stable patterns (auth, error handling, async, project structure). Always check [crates.io](https://crates.io/search?q=azure_) and the [Azure SDK for Rust GitHub repo](https://github.com/Azure/azure-sdk-for-rust) for latest status.

**Total rules: 66** (9 CRITICAL, 25 HIGH, 29 MEDIUM, 3 LOW)

---

## Severity Legend

- **CRITICAL**: Security vulnerability or sample will not compile/run. Must fix before any publication.
- **HIGH**: Major quality issue that will confuse users or cause production failures. Fix before merge.
- **MEDIUM**: Best practice violation. Should fix before publication for maintainability.
- **LOW**: Polish item, nice-to-have improvement.

---

## Quick Pre-Review Checklist (5-Minute Scan)

- [ ] **Cargo.toml**: Uses `azure_*` crates (not unofficial wrappers)
- [ ] **Authentication**: Uses `DefaultAzureCredential` (not connection strings or hardcoded keys)
- [ ] **.gitignore**: Exists and includes `.env`, `target/`
- [ ] **No secrets**: No hardcoded credentials, API keys, or tokens in code
- [ ] **README.md**: Exists with prerequisites, setup steps, and expected output
- [ ] **LICENSE**: MIT license file present (required for Azure Samples)
- [ ] **Security**: `cargo audit` passes with no critical/high vulnerabilities
- [ ] **Rust Edition**: `edition = "2021"` in Cargo.toml
- [ ] **Error handling**: Uses `Result<T, E>` and `?` operator (no `unwrap()` in main paths)
- [ ] **Resource cleanup**: Clients properly dropped (RAII pattern, no leaks)
- [ ] **Lock file**: Cargo.lock committed (for binary crates)
- [ ] **Clippy**: `cargo clippy` passes with no warnings
- [ ] **Imports work**: `cargo check` succeeds
- [ ] **Build succeeds**: `cargo build` completes without errors
- [ ] **Sample runs**: `cargo run` executes without panics

---

## Blocker Issues (Auto-Reject)

These issues always block publication. Samples with any of these must be rejected immediately:

1. **Hardcoded secrets**â€”Any production credentials, API keys, connection strings, or tokens in code
2. **Missing authentication**â€”No auth implementation or uses insecure methods
3. **No error handling**â€”Uses `unwrap()` or `expect()` in main code paths, no `Result` returns
4. **Broken imports**â€”Missing dependencies, incorrect crate names, `cargo check` fails
5. **Security vulnerabilities**â€”`cargo audit` shows critical or high CVEs
6. **Missing LICENSE**â€”No LICENSE file at ANY level of repo hierarchy (MIT required). âš ï¸ Check repo root before flagging.
7. **.env file committed**â€”Live credentials in version control. âš ï¸ Verify with `git ls-files .env`.
8. **Panics in sample code**â€”Uses `unwrap()`, `expect()`, or `panic!()` in non-test code paths without justification

---

## Detailed Rules


### Language-Specific References (Rust code examples)

| # | Section | Reference File |
|---|---------|---------------|
| 1 | Project Setup â€” Rust | [references/project-setup.md](references/project-setup.md) |
| 2 | SDK Client Patterns â€” Rust | [references/sdk-client-patterns.md](references/sdk-client-patterns.md) |
| 3 | AI Services â€” Rust | [references/ai-services.md](references/ai-services.md) |
| 4 | Data Services â€” Rust | [references/data-services.md](references/data-services.md) |
| 5 | Messaging â€” Rust | [references/messaging.md](references/messaging.md) |
| 6 | Key Vault â€” Rust | [references/keyvault.md](references/keyvault.md) |
| 7 | Vector Search â€” Rust | [references/vector-search.md](references/vector-search.md) |
| 8 | Error Handling â€” Rust | [references/error-handling.md](references/error-handling.md) |
| 9 | Data Management â€” Rust | [references/data-management.md](references/data-management.md) |
| 10 | Sample Hygiene â€” Rust | [references/sample-hygiene.md](references/sample-hygiene.md) |
| 11 | Documentation â€” Rust | [references/documentation.md](references/documentation.md) |
| 12 | Infrastructure â€” Rust | [references/infrastructure.md](references/infrastructure.md) |
| 13 | azd â€” Rust | [references/azd.md](references/azd.md) |
| 14 | Rust Idioms (Rust-unique) | [references/rust-idioms.md](references/rust-idioms.md) |
| â€” | Comprehensive Checklist | [references/checklist.md](references/checklist.md) |

---

## Companion Skills

- **azure-sdk-typescript-sample-review** â€” TypeScript-specific Azure SDK patterns (template this skill was adapted from)
- **azure-sdk-dotnet-sample-review** â€” .NET 9/10 + Aspire Azure SDK patterns
- **azure-sdk-python-sample-review** â€” Python 3.9+ + async Azure SDK patterns

---

## Summary

This skill enforces **66 rules** for Azure SDK Rust sample quality covering: authentication (DefaultAzureCredential, managed identity, token refresh), Rust idioms (ownership, RAII, async/tokio, error propagation), data services (Cosmos DB, Azure SQL, Storage), AI services (OpenAI, embeddings), infrastructure (Bicep/AVM, azd), and documentation accuracy. Apply these patterns to ensure samples are secure, idiomatic, well-documented, and ready for publication.

## References

> **References location:** All reference files for this skill live inside the skill directory at `.github/skills/data-plus-ai-sdk-rust-sample-review/`. Paths like `references/file.md` resolve to `.github/skills/data-plus-ai-sdk-rust-sample-review/references/file.md`. Paths are relative to the skill folder, not the repo root.

