# Installation Guide

## Prerequisites

- Python 3.9+
- Git
- An Anthropic API key for Claude

## Step 1: Clone the Repository

```bash
git clone <REPOSITORY_URL>
cd mr_agent
```

## Step 2: Install uv (if not already installed)

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Verify installation:

```bash
uv --version
```

## Step 3: Install Dependencies

```bash
uv sync
```

This installs all project dependencies defined in `pyproject.toml`.

## Step 4: Configure Environment Variables

Create a `.env` file at the project root:

```env
ANTHROPIC_API_KEY=your_claude_api_key
```

Replace `your_claude_api_key` with your actual Claude API key.

**Note**: The `.env` file is git-ignored and should never be committed.

## Step 5: Verify Installation

```bash
uv run main.py --help
```

or

```bash
python main.py --help
```

 🍩 **Note** If you see the help output, the installation is complete.
