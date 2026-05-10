# python-venv-enforcement

An OpenCode/Claude Code skill that enforces Python virtual environment usage.

Every time the agent writes a Python script with external dependencies, it must create and activate a venv first — no exceptions.

## Features

- Auto-detects Python tasks requiring dependencies
- Forces venv creation before any `pip install`
- Handles Windows execution policy fallback
- Rationalization-proof with explicit counter-arguments
- Works with OpenCode, Claude Code, and other Superpowers-compatible agents

## Installation

Place `SKILL.md` in your agent's skills directory:

**OpenCode:**
```
~/.config/opencode/skills/python-venv-enforcement/SKILL.md
```

**Claude Code:**
```
~/.claude/skills/python-venv-enforcement/SKILL.md
```

## Usage

The skill activates automatically. Just ask your agent to create a Python script — it will handle venv setup before writing code.

## License

MIT
