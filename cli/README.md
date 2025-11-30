# CLI Changelog Tools

Standalone CLI tools for generating changelogs that work with any AI coding agent.

These tools are designed to integrate with CLI-based AI agents like:

- **[Cline CLI](https://docs.cline.bot/cline-cli/overview)** - Autonomous coding agent
- **[OpenAI Codex CLI](https://github.com/openai/codex)** - OpenAI's local coding agent
- **Jules** - Google's AI coding agent
- Any other CLI-based AI tool that accepts prompts via stdin or command arguments

## Available Tools

### Python CLI (`changelog_cli.py`)

```bash
# Get commits since last release
python changelog_cli.py --commits

# Generate full prompt for AI agents
python changelog_cli.py --generate

# Print only the system prompt
python changelog_cli.py --prompt-only
```

### Shell Script (`changelog.sh`)

```bash
# Make executable (first time only)
chmod +x changelog.sh

# Get commits since last release
./changelog.sh --commits

# Generate full prompt for AI agents
./changelog.sh --generate

# Print only the system prompt
./changelog.sh --prompt-only
```

## Cline CLI Integration

[Cline CLI](https://docs.cline.bot/cline-cli/overview) is an AI-powered CLI tool that can process prompts and generate code/content.

### Installation

```bash
# Install Cline CLI (requires Node.js 18+)
npm install -g cline

# Authenticate with your preferred provider
cline auth
```

### Usage

```bash
# Generate changelog using Cline (pipes prompt to cline)
python changelog_cli.py --generate | cline

# With specific output format
python changelog_cli.py --generate | cline -o text

# Save output to file
python changelog_cli.py --generate | cline -o text > CHANGELOG.md

# Using shell script
./changelog.sh --generate | cline -o text
```

### CI/CD Integration

Cline CLI works great in CI/CD pipelines. See the GitHub Actions workflow in `.github/workflows/generate-changelog.yml` for a complete example.

## OpenAI Codex CLI Integration

[OpenAI Codex CLI](https://github.com/openai/codex) is a coding agent from OpenAI that runs locally on your computer.

### Installation

```bash
# Install via npm
npm install -g @openai/codex

# Or via Homebrew (macOS)
brew install --cask codex
```

### Usage

```bash
# Interactive mode with prompt
codex "$(python changelog_cli.py --generate)"

# Non-interactive automation mode
codex exec "$(python changelog_cli.py --generate)"

# Using shell script
codex "$(./changelog.sh --generate)"
```

## Other CLI Integrations

### With Jules

```bash
# Generate changelog using Jules
./changelog.sh --generate | jules

# Or as a command argument
jules "$(./changelog.sh --generate)"
```

### Generic AI CLI Integration

```bash
# Works with any CLI that accepts prompts via stdin
./changelog.sh --generate | your-ai-cli

# Or via command line argument
your-ai-cli "$(python changelog_cli.py --generate)"
```

## How It Works

1. **`--commits`**: Uses `git log` to fetch all commits since the last tagged release
2. **`--generate`**: Creates a complete prompt including:
   - System instructions for changelog formatting
   - The list of commits to analyze
   - Request to generate the changelog
3. The AI agent processes the prompt and outputs a formatted markdown changelog

## Requirements

- Git repository with at least one tag
- Python 3.6+ (for Python version) or Bash (for shell version)
- No external dependencies required!
