# OpenAI Agents SDK Changelog Agent

This is an OpenAI Agents SDK implementation of the Changelog agent.

## Installation

```bash
pip install -r requirements.txt
```

## Usage

```python
from changelog_agent import create_changelog_agent, run_changelog_agent
from agents import Runner

# Option 1: Quick synchronous run
changelog = run_changelog_agent()
print(changelog)

# Option 2: Async run
import asyncio
from changelog_agent import run_changelog_agent_async

changelog = asyncio.run(run_changelog_agent_async())
print(changelog)

# Option 3: Create agent for more control
agent = create_changelog_agent(model="gpt-4o")
result = Runner.run_sync(agent, "Generate a changelog for this repository")
print(result.final_output)
```

## Using Different Models

```python
# Use a different OpenAI model
changelog = run_changelog_agent(model="gpt-4-turbo")

# Or when creating the agent
agent = create_changelog_agent(model="gpt-4o-mini")
```

## Command Line Usage

```bash
# Set your API key
export OPENAI_API_KEY="your-key-here"

# Run from inside a git repository
python changelog_agent.py
```

## Pre-fetched Commits

If you already have the commits, you can pass them directly:

```python
commits = """abc1234 Added new feature
def5678 Fixed critical bug
ghi9012 Updated documentation"""

changelog = run_changelog_agent(commits=commits)
```
