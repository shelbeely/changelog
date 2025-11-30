**Changelog** is an agent-agnostic tool that uses `git` to determine the new commits since the last release in a git repository folder and generates a nicely formatted markdown changelog [like this one](https://github.com/evilsocket/nerve/releases/tag/v1.3.0).

This agent works with multiple frameworks and CLI tools:

**Agent Frameworks:**
- **[Nerve](https://github.com/evilsocket/nerve)** - The original agent framework
- **[LangChain](https://github.com/langchain-ai/langchain)** - Popular LLM framework with broad model support
- **[OpenAI Agents SDK](https://github.com/openai/openai-agents-python)** - OpenAI's native agent framework

**CLI Tools:**
- **[Cline CLI](https://docs.cline.bot/cline-cli/overview)** - Autonomous coding agent
- **[OpenAI Codex CLI](https://github.com/openai/codex)** - OpenAI's local coding agent
- **Jules** - Google's AI coding agent
- Any other CLI-based AI tool

**Automation:**
- **GitHub Actions** - Automated changelog generation on releases

---

## Nerve (Original)

Install with (requires nerve >= 1.4.x):

```bash
# this will download and install (or update) to ~/.nerve/agents
nerve install evilsocket/changelog 
```

Run from inside a git repository folder with:

```bash
# use with -q to only print the changelog markdown and disable logs
nerve run changelog -q
```

In action:

[![asciicast](https://asciinema.org/a/710433.svg)](https://asciinema.org/a/710433)

---

## LangChain

See [langchain/README.md](langchain/README.md) for detailed documentation.

### Quick Start

```bash
cd langchain
pip install -r requirements.txt
pip install langchain-openai  # or your preferred provider
```

```python
from langchain_openai import ChatOpenAI
from changelog_agent import run_changelog_agent

llm = ChatOpenAI(model="gpt-4")
changelog = run_changelog_agent(llm)
print(changelog)
```

Supports any LangChain-compatible LLM (OpenAI, Anthropic, Google, local models, etc.)

---

## OpenAI Agents SDK

See [openai/README.md](openai/README.md) for detailed documentation.

### Quick Start

```bash
cd openai
pip install -r requirements.txt
export OPENAI_API_KEY="your-key-here"
```

```python
from changelog_agent import run_changelog_agent

changelog = run_changelog_agent()
print(changelog)
```

---

## CLI Tools (Jules, Cline, Codex, etc.)

See [cli/README.md](cli/README.md) for detailed documentation.

Standalone CLI tools that work with any AI coding agent.

### Quick Start

```bash
cd cli

# Using Python
python changelog_cli.py --generate | codex
python changelog_cli.py --generate | cline
python changelog_cli.py --generate | jules

# Using Shell script
./changelog.sh --generate | your-ai-cli
```

### Available Commands

```bash
# Get commits since last release
python changelog_cli.py --commits

# Generate full prompt for AI agents
python changelog_cli.py --generate

# Print only the system prompt
python changelog_cli.py --prompt-only
```

No dependencies required - just Python 3.6+ or Bash!

---

## GitHub Actions

Automate changelog generation in your CI/CD pipeline.

### Setup

1. Copy `.github/workflows/generate-changelog.yml` to your repository
2. Add your API key as a repository secret:
   - `OPENAI_API_KEY` for OpenAI
   - `ANTHROPIC_API_KEY` for Anthropic/Cline

### Usage

The workflow can be triggered:
- **Automatically** on new releases - updates the release notes
- **Manually** via workflow dispatch - choose your AI provider

```yaml
# Trigger manually with provider selection
workflow_dispatch:
  inputs:
    provider:
      type: choice
      options:
        - openai
        - anthropic
        - cline
        - codex
```

### Supported Providers

- **OpenAI API** (default) - Uses GPT-4o via API
- **Anthropic API** - Uses Claude via API
- **Cline CLI** - Uses Cline with your configured provider
- **Codex CLI** - Uses OpenAI Codex CLI locally

---

## How It Works

All implementations share the same core functionality:

1. **get_new_commits** - Fetches commits since the last git tag
2. **create_changelog** - Generates formatted markdown changelog

The agent analyzes commits, categorizes them (features, fixes, etc.), and produces a clean changelog with emojis for important changes.