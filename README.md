# Azure SDK Code Sample Review Skills

A Copilot CLI / VS Code Copilot Chat plugin that reviews Azure SDK code samples for best practices, credential handling, error patterns, and documentation compliance.

## Supported Languages

| Language | Skill |
|----------|-------|
| Auto-detect | `azure-sdk-sample-review` |
| Python | `azure-sdk-python-sample-review` |
| TypeScript | `azure-sdk-typescript-sample-review` |
| .NET | `azure-sdk-dotnet-sample-review` |
| Java | `azure-sdk-java-sample-review` |
| Go | `azure-sdk-go-sample-review` |
| Rust | `azure-sdk-rust-sample-review` |

## Usage

### Register as a Plugin (consumer repo)

Add to your repo's `.github/copilot/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "azure-sdk-code-sample-skills": {
      "source": {
        "source": "github",
        "repo": "Azure-Samples/azure-sdk-code-sample-skills"
      }
    }
  },
  "enabledPlugins": {
    "azure-sdk-samples@azure-sdk-code-sample-skills": true
  }
}
```

### Copilot CLI

Skills are available immediately once the plugin is registered. Use natural language:

```
copilot "review this Python Azure SDK sample for best practices"
```

### VS Code Copilot Chat

After registering, VS Code will prompt to enable the plugin on first use.

## Plugin Structure

```
plugins/azure-sdk-samples/
├── .github/plugin/plugin.json   ← manifest
└── skills/
    ├── azure-sdk-sample-review/       ← orchestrator (auto-detect language)
    ├── azure-sdk-python-sample-review/
    ├── azure-sdk-typescript-sample-review/
    ├── azure-sdk-dotnet-sample-review/
    ├── azure-sdk-java-sample-review/
    ├── azure-sdk-go-sample-review/
    └── azure-sdk-rust-sample-review/
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

See [LICENSE.md](LICENSE.md).
