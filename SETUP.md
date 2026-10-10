# Setup Guide (using uv)

This project is managed with [uv](https://docs.astral.sh/uv/). Dependencies are declared in `pyproject.toml` and locked in `uv.lock`; Python 3.12 is pinned in `.python-version`.

## 1. Install uv

**Windows (PowerShell):**
```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

**macOS / Linux:**
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Verify:
```powershell
uv --version
```

## 2. Create the virtual environment and install dependencies

From the project folder, one command does both. It downloads Python 3.12 if needed, creates `.venv`, and installs the exact versions from `uv.lock`:

```powershell
uv sync
```

(Equivalent manual steps: `uv venv` then `uv sync`.)

## 3. Configure environment variables

Create a `.env` file in the project root (loaded via `python-dotenv`):

```
XAI_API_KEY=your-key-here
```

> `.env` is not listed in `.gitignore`. Add a line `.env` to it so your key is never committed.

## 4. Run the project

No activation is needed; `uv run` uses the project's `.venv` automatically:

```powershell
uv run main.py
```

To run `app.ipynb`, open it in VS Code and select the `.venv` interpreter as the kernel. If no kernel is available, add Jupyter support as a dev dependency:

```powershell
uv add --dev ipykernel
```

## 5. (Optional) Activate the environment manually

```powershell
.venv\Scripts\Activate.ps1        # PowerShell
source .venv/bin/activate         # macOS / Linux / Git Bash (.venv/Scripts/activate on Windows)
deactivate                        # to leave
```

## Common commands

| Task | Command |
|------|---------|
| Install / sync dependencies | `uv sync` |
| Add a package | `uv add <package>` |
| Add a dev-only package | `uv add --dev <package>` |
| Remove a package | `uv remove <package>` |
| Update the lock file | `uv lock --upgrade` |
| Show installed packages | `uv pip list` |
| Run a script | `uv run <file.py>` |
| Export a requirements.txt | `uv export --no-hashes -o requirements.txt` |
| Delete the venv | `Remove-Item -Recurse -Force .venv` |

## Without uv (fallback)

A `requirements.txt` is included for plain pip:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```
