---
name: azure-sdk-sample-review
description: Reviews Azure SDK samples for best practices, credentials, errors, and docs. Auto-detects language.
domain: sdk-review
---

## USE FOR

- "review Azure SDK sample"
- "check TypeScript/Python/.NET/Go/Java/Rust sample"
- Reviewing credential handling, error patterns, documentation in Azure SDK samples
- Reviewing quickstart articles for SDK guidance
- "SDK code review", "review sample credentials"

## DO NOT USE FOR

- General code review unrelated to Azure SDK
- Production application code
- Azure service configuration

## Context

Reviews Azure SDK code samples for publication. Supports TypeScript (`@azure/*`), Python (`azure-*`), .NET (`Azure.*`), Go (`azcore`), Java (`com.azure.*`), Rust (`azure_*`), and quickstart articles.

## Language Detection

**TS**: `.ts`, `@azure/*` | **Py**: `.py`, `azure-*` | **.NET**: `.cs`, `Azure.*` | **Go**: `.go`, `azcore` | **Java**: `.java`, `com.azure.*` | **Rust**: `.rs`, `azure_*` | **Quickstart**: `.md`

## Review Architecture â€” 3-Layer Model

Execute review in layer order. Earlier layers produce structured, high-confidence findings; later layers add nuance.

### Layer 1: Pattern-Based Rules (ALWAYS run first)

Load `rules/shared.yaml` + `rules/{language}.yaml`. Apply pattern-matching rules to produce findings. These rules provide structured guidance for the reviewer â€” patterns to look for, anti-patterns to flag, and exceptions to consider.

**Note:** Rules are applied by a reviewer (human or LLM), not executed as a regex engine. Regex patterns serve as detection hints, not literal execution targets.

**Output:** List of rule violations with `{rule_id, severity, location, fix}`

### Layer 2: Version & Deprecation Checks

Check imports/dependencies against:
- `versions/deprecated-packages.yaml` â€” retired packages with replacements
- `versions/track1-packages.yaml` â€” legacy SDK packages (auto-reject)
- External source of truth for current versions: `MicrosoftDocs/azure-dev-docs-pr/articles/includes/{language}-all.md`

**Output:** Deprecated/Track 1 findings with migration guidance

### Layer 3: LLM Judgment (informed by references)

Load `references/shared/` + `references/{language}/`. Apply nuanced review for:
- Architecture and code structure quality
- Documentation completeness
- Naming and readability
- Patterns that rules can't catch (e.g., "is this the right service for this use case?")

**Output:** Advisory findings with recommendations

## Review Approach

1. Detect language from file extensions/imports
2. **Layer 1:** Apply `rules/shared.yaml` + `rules/{language}.yaml` deterministically
3. **Layer 2:** Check `versions/deprecated-packages.yaml` and `versions/track1-packages.yaml`
4. **Layer 3:** Load `references/shared/` + `references/{language}/` for judgment-based review
5. Present findings grouped by severity: blocker > high > medium > low

## Output Format

```markdown
## Review: {filename}

### ðŸš« Blockers (must fix)
| Rule | Location | Issue | Fix |
|------|----------|-------|-----|
| CRED-001 | line 5 | Hardcoded connection string | Use DefaultAzureCredential |

### âš ï¸ High (should fix)
...

### ðŸ’¡ Medium/Low (consider)
...

### âœ… Strengths
...
```

## References

> **References location:** Supporting documents live inside this skill's directory at `.github/skills/azure-sdk-sample-review/`. Paths like `references/file.md` are relative to this skill folder, not the repo root.

| Scope | Path | Purpose |
|-------|------|---------|
| **Rules (deterministic)** | | |
| Shared rules | [rules/shared.yaml](rules/shared.yaml) | Universal pass/fail rules |
| TypeScript rules | [rules/typescript.yaml](rules/typescript.yaml) | TS-specific rules |
| Python rules | [rules/python.yaml](rules/python.yaml) | Python-specific rules |
| .NET rules | [rules/dotnet.yaml](rules/dotnet.yaml) | .NET-specific rules |
| Go rules | [rules/go.yaml](rules/go.yaml) | Go-specific rules |
| Java rules | [rules/java.yaml](rules/java.yaml) | Java-specific rules |
| Rust rules | [rules/rust.yaml](rules/rust.yaml) | Rust-specific rules |
| **Versions** | | |
| Deprecated packages | [versions/deprecated-packages.yaml](versions/deprecated-packages.yaml) | Retired packages with replacements |
| Track 1 packages | [versions/track1-packages.yaml](versions/track1-packages.yaml) | Legacy packages (blockers) |
| Current versions (external) | `MicrosoftDocs/azure-dev-docs-pr/articles/includes/{lang}-all.md` | Canonical package registry |
| **References (LLM judgment)** | | |
| Shared | [references/shared/index.md](references/shared/index.md) | Universal patterns |
| TypeScript | [references/typescript/index.md](references/typescript/index.md) | TS patterns |
| Python | [references/python/index.md](references/python/index.md) | Python patterns |
| .NET | [references/dotnet/index.md](references/dotnet/index.md) | .NET patterns |
| Go | [references/go/index.md](references/go/index.md) | Go patterns |
| Java | [references/java/index.md](references/java/index.md) | Java patterns |
| Rust | [references/rust/index.md](references/rust/index.md) | Rust patterns |
| Quickstart | [references/quickstart/index.md](references/quickstart/index.md) | Article review |

## Example

**User**: "Review this TypeScript sample"  
**Skill**: Detects TypeScript â†’ applies `rules/shared.yaml` + `rules/typescript.yaml` â†’ checks `versions/deprecated-packages.yaml` â†’ loads `references/shared/` + `references/typescript/` â†’ reports findings by severity.

