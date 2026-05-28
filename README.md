# MR Validator Agent

[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Spec-Driven Development](https://img.shields.io/badge/spec--driven-development-informational.svg)](https://github.com/github/spec-kit)

> **Automated MR validation as a third reviewer** — Complementing GitLab's existing validators with AI-powered code quality checks.

---

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Spec Kit Workflow](#spec-kit-workflow)
- [Development](#development)
- [Contributing](#contributing)
- [License](#license)

---

## Features

✨ **Core Capabilities**

- 🔍 **Extract & Analyze**: Retrieve committed changes from numbered MRs with full context
- 📝 **Docstring Validation**: Enforce French documentation for code and tests
- 🏗️ **Design Pattern Verification**: Ensure architectural patterns are correctly applied
- 🤖 **AI-Powered Review**: Leverage Claude Code as an intelligent third reviewer

---

## Tech Stack

| Component | Technology |
|-----------|-----------|
| **Language** | Python 3.9+ |
| **Package Manager** | `uv` |
| **Development Workflow** | Spec Kit (Spec → Plan → Tasks → Implement) |
| **Version Control** | GitHub |
| **AI Engine** | Claude Code (via Anthropic API) |

---

## Getting Started

### Prerequisites

- Python 3.9+
- Git
- An Anthropic API key for Claude

### Installation

1. **Clone the repository** and install dependencies:
   ```bash
   git clone <REPOSITORY_URL>
   cd mr_agent
   ```

2. **See [INSTALL.md](INSTALL.md)** for detailed setup instructions including:
   - Creating a virtual environment with `uv venv`
   - Installing dependencies with `uv sync`
   - Configuring your `.env` file with API keys

3. **Verify installation**:
   ```bash
   uv run main.py --help
   ```

---

## Usage

### Basic MR Validation

Validate a specific Merge Request:

```bash
# Validate MR #123
uv run main.py --mr 123

# Validate with detailed output
uv run main.py --mr 123 --verbose

# Validate and generate report
uv run main.py --mr 123 --output report.json
```

### Output

The agent validates and reports on:
- ✅ Docstring presence and language (French)
- ✅ Design pattern compliance
- ✅ Code quality metrics
- ✅ Review recommendations

---

## Project Structure

```text
mr_agent/
├── src/
│   ├── agents/           # AI agent implementation
│   ├── validators/       # Validation logic
│   ├── parsers/          # MR change parsing
│   └── __main__.py       # Entry point
├── tests/
│   ├── unit/             # Unit tests
│   └── integration/      # Integration tests
├── docs/
│   └── images/           # Documentation images
├── .specify/             # Spec Kit configuration
├── INSTALL.md            # Detailed installation guide
├── README.md             # This file
├── pyproject.toml        # Python dependencies
├── .env.example          # Environment variables template
└── .gitignore            # Git ignore rules
```

---

## Spec Kit Workflow

This project follows **Spec-Driven Development** using GitHub's Spec Kit framework.

### The Development Cycle

```
Spec → Plan → Tasks → Implement
```

### Initialize Spec Kit

```bash
# One-time setup
uvx --from git+https://github.com/github/spec-kit.git specify init mr_agent

# Create a new feature spec
uvx specify specify --name "Feature Name"
```

### Workflow Visualization

![Spec Kit Workflow](docs/images/github_spec-kit.git%20specify.png)

**Learn more**: [Spec Kit Documentation](https://github.com/github/spec-kit)

---

## Development

### Run Tests

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=src
```

### Format & Lint Code

```bash
# Format with Ruff
ruff format

# Lint code
ruff check

# Fix lint issues automatically
ruff check --fix
```

### Local Development Loop

```bash
# 1. Create a feature branch
git checkout -b feature/my-feature

# 2. Make changes and test
pytest

# 3. Format and lint
ruff format && ruff check --fix

# 4. Commit
git commit -m "feature: description"

# 5. Push and create PR
git push origin feature/my-feature
```

---

## Contributing

We welcome contributions! Here's how to get started:

1. **Fork** the repository
2. **Create a feature branch**:
   ```bash
   git checkout -b feature/description
   ```
3. **Make your changes** and ensure tests pass:
   ```bash
   pytest && ruff format && ruff check
   ```
4. **Commit** with clear messages:
   ```bash
   git commit -m "feature: add new validator"
   ```
5. **Push** and open a Pull Request:
   ```bash
   git push origin feature/description
   ```

### Development Guidelines

- Follow the constitution principles (see `.specify/memory/constitution.md`)
- Write tests before implementation (TDD)
- Ensure all docstrings are in French
- Run the full test suite before submitting PRs

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| `uv` command not found | See [INSTALL.md](INSTALL.md#troubleshooting) |
| Missing `ANTHROPIC_API_KEY` | Add it to `.env` (copy from `.env.example`) |
| Tests fail | Run `pytest -v` for detailed output |
| Virtual environment issues | Run `uv venv --python 3.11` to create a fresh one |

---

## License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## Questions?

- 📖 **Setup help**: See [INSTALL.md](INSTALL.md)
- 🔧 **Development workflow**: Check [Spec Kit docs](https://github.com/github/spec-kit)
- 🐛 **Found a bug?**: Open an [Issue](https://github.com/frsauvage/mr_agent/issues)
- 💡 **Have an idea?**: Start a [Discussion](https://github.com/frsauvage/mr_agent/discussions)

---

**Made with ❤️ by the team**
