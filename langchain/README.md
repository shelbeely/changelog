# LangChain Changelog Agent

This is a LangChain implementation of the Changelog agent.

## Installation

```bash
pip install -r requirements.txt

# Install your preferred LLM provider
pip install langchain-openai  # For OpenAI
# or
pip install langchain-anthropic  # For Anthropic
# or
pip install langchain-google-genai  # For Google
```

## Usage

```python
from langchain_openai import ChatOpenAI
from changelog_agent import create_changelog_agent, run_changelog_agent

# Create an LLM instance
llm = ChatOpenAI(model="gpt-4")

# Option 1: Quick run (commits since last release)
changelog = run_changelog_agent(llm)
print(changelog)

# Option 2: Generate changelog for entire git history (retroactive)
changelog = run_changelog_agent(llm, full_history=True)
print(changelog)

# Option 3: Create agent for more control
agent = create_changelog_agent(llm)
result = agent.invoke({"input": "Generate a changelog for this repository"})
print(result["output"])
```

## Using with Other LLM Providers

```python
# With Anthropic
from langchain_anthropic import ChatAnthropic
llm = ChatAnthropic(model="claude-3-opus-20240229")
changelog = run_changelog_agent(llm)

# With Google
from langchain_google_genai import ChatGoogleGenerativeAI
llm = ChatGoogleGenerativeAI(model="gemini-pro")
changelog = run_changelog_agent(llm)
```

## Retroactive Changelog Generation

To generate a changelog for your entire git history:

```python
# Generate a comprehensive changelog from all commits
changelog = run_changelog_agent(llm, full_history=True)
```

## Command Line Usage

```bash
# Set your API key
export OPENAI_API_KEY="your-key-here"

# Run from inside a git repository
python changelog_agent.py
```
