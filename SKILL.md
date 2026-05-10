---
name: python-venv-enforcement
description: Use when writing new Python scripts that import third-party libraries, creating Python projects, installing pip packages, or running Python code that requires external dependencies
---

# Python Virtual Environment Enforcement

## Overview

Every new Python script or project **MUST** use a virtual environment before writing any code or installing any dependency. No exceptions.

## When to Use

This skill applies whenever you are about to:

- Create a new `.py` file that imports third-party libraries
- `pip install` any package
- Run a Python script that has external dependencies
- Start a new Python project

**Skip ONLY when:** running a single stdlib-only one-liner via `python -c "..."` or `python -m http.server`-style built-in modules. If in doubt, use venv.

## Procedure

```
Step 1: Check venv → Step 2: Create if missing → Step 3: Activate → Step 4: pip install → Step 5: Write/run code
```

### 1. Check
```bash
# Linux/macOS
test -d venv || python3 -m venv venv

# Windows PowerShell
if (-not (Test-Path venv)) { python -m venv venv }
```

### 2. Activate before ANY pip or python command
```bash
# Linux/macOS
source venv/bin/activate

# Windows PowerShell (preferred)
venv\Scripts\Activate.ps1

# Windows fallback — when execution policy blocks .ps1
venv\Scripts\python.exe -m pip install <package>
venv\Scripts\python.exe script.py
```

If `Activate.ps1` is blocked (ExecutionPolicy Restricted), use the direct python.exe path as fallback. The key principle is using the venv's interpreter, not the global one.

### 3. Install dependencies ONLY after activation
```bash
pip install -r requirements.txt
# or
python -m pip install <package>
```

### 4. Write and run code with venv active
```bash
python script.py
```

### 5. Ensure .gitignore excludes venv
If a `.gitignore` exists in the project, add `venv/` if not already present.

## Rationalization Table

| Excuse | Reality |
|--------|---------|
| "It's just a quick script" | Quick scripts accumulate dependencies and pollute global site-packages. |
| "I'll add venv later" | Later never happens. Create it first. |
| "This only uses one library" | One library pulls transitive dependencies. Isolate always. |
| "I already have it installed globally" | Global installs break across Python versions and projects. |
| "The user didn't ask for venv" | Users want working, isolated code. Venv is infrastructure, not feature work. |
| "I'm on Windows, venv activation is annoying" | `venv\Scripts\Activate.ps1` works. If blocked by execution policy, use `venv\Scripts\python.exe` directly. |
| "venv already exists, nothing to do" | Still must activate it before pip install or running code. |

## Red Flags — STOP and use venv

- Writing `.py` file with `import` statements at the top
- Running `pip install` before activating venv
- "Let me just test this quickly" without venv
- Copying code from another project without checking for venv

**All of these mean: stop, create/activate venv, then proceed.**

## Common Mistakes

- **Creating venv but forgetting to activate** — pip install still goes global
- **Using `pip` instead of `python -m pip`** — may use wrong pip binary
- **Activating but not running pip install** — script will fail with ImportError
- **Skipping .gitignore update** — venv gets committed to git
