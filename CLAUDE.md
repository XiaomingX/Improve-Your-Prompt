# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Improve-Your-Prompt is a meta-prompting tool that uses intelligent language models to generate or improve prompts. The core technique involves using a high-intelligence model to optimize prompts for better, more effective results.

The project is written in Python and uses OpenAI's API to implement a two-step prompt optimization process:
1. Generate an optimal "agent description" (system prompt) based on the user's question
2. Use that generated system prompt to answer the user's question more effectively

## Development Setup

This project uses [uv](https://github.com/astral-sh/uv) for dependency management and requires Python 3.11+.

### Install dependencies
```bash
uv sync
```

### Run the application
```bash
# Using uv
uv run python src/main.py

# Or activate virtual environment first
source .venv/bin/activate  # macOS/Linux
# .venv\Scripts\activate  # Windows
python src/main.py
```

## Architecture

### Core Components

**src/main.py** - Single-file application containing:
- `fetchSystemPrompt(question)`: Generates an optimal agent description (system prompt) for a given question using few-shot learning with 3 examples
- `get_answer(question)`: Uses the generated system prompt to answer the user's question
- `main()`: Entry point that demonstrates the two-step process

### Two-Step Process

1. **Meta-Prompting Step**: Given a user question, the system uses a few-shot prompt with examples to generate a detailed "agent description" that defines the most capable and suitable persona to answer that specific question.

2. **Answer Generation Step**: The generated agent description is used as the system prompt, with the original question as the user message, to produce a higher-quality answer.

### API Configuration

The application uses OpenAI's API (currently configured for `gpt-4o-mini`). The API key must be set via the `OPENAI_API_KEY` environment variable or directly in the code (line 37 in main.py).

## Key Concepts

- **Meta-Prompting**: Using an LLM to generate optimized prompts for another LLM call
- **Agent Description**: A detailed second-person description of an expert persona tailored to answer a specific question
- **Few-Shot Learning**: The system uses 3 example instruction-description pairs to teach the model how to generate appropriate agent descriptions
