# Python 3.14 Development Container

A modern Python development environment configured with the latest tooling for productive Python 3.14 development in Visual Studio Code.

## 🎯 Purpose

This dev container is designed for:

- Python 3.14 application development
- Web backend development (FastAPI, Django, Flask)
- Data science and scripting projects
- Testing and automation with pytest
- Jupyter notebook workflows

## 🛠️ Included Tools & Features

### Python Runtime

- **Python 3.14**: Latest Python release with deferred annotations (PEP 649), t-strings (PEP 750), and improved free-threading support
- **pip**: Package installer (latest)
- **uv**: Ultra-fast Python package and project manager

### Code Quality

- **Ruff**: Extremely fast Python linter and formatter (replaces flake8, black, isort, and more)
- **Mypy**: Static type checker for Python
- **pre-commit**: Git hook framework for automated checks on commit

### Testing

- **pytest**: Feature-rich Python testing framework
- **pytest-cov**: Code coverage reporting for pytest

### Interactive

- **IPython**: Enhanced interactive Python shell with rich output and magic commands

## 📦 VS Code Extensions

### Python Development
- **Python**: Core IntelliSense, environment management, and debugging
- **Pylance**: Fast, feature-rich language server with advanced type inference
- **Python Debugger**: Rich debugging experience with breakpoints and variable inspection

### Code Quality
- **Ruff**: Linting and formatting on save with auto-fix support

### Notebooks
- **Jupyter**: Full notebook support with interactive output and variable explorer

### Productivity
- **autoDocstring**: Auto-generate Google, NumPy, or Sphinx-style docstrings
- **Even Better TOML**: `pyproject.toml` syntax highlighting and validation
- **YAML**: YAML syntax support for configuration files
- **GitLens**: Advanced Git integration with blame, history, and comparisons
- **Todo Tree**: Track TODO/FIXME/HACK comments across the codebase
- **Bookmarks**: Mark and navigate important code locations
- **EditorConfig**: Enforce consistent coding styles across editors

## 🚀 Getting Started

### Prerequisites

- [Visual Studio Code](https://code.visualstudio.com/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

### Setup Instructions

1. **Create your project folder**
   ```bash
   mkdir my-python-project
   cd my-python-project
   ```

2. **Add the dev container configuration**
   - Copy the `.devcontainer` folder to your project root

3. **Open in VS Code**
   ```bash
   code .
   ```

4. **Reopen in Container**
   - Press `F1` or `Ctrl+Shift+P` (Windows/Linux) / `Cmd+Shift+P` (Mac)
   - Select: `Dev Containers: Reopen in Container`
   - Wait for the container to build and start

5. **Verify the setup**
   ```bash
   python --version
   ruff --version
   uv --version
   ```

## 💻 Usage Examples

### Create a New Project with uv

```bash
# Initialize a new project
uv init my-project
cd my-project

# Add dependencies
uv add fastapi httpx

# Add dev dependencies
uv add --dev pytest pytest-cov ruff mypy

# Run your script
uv run python main.py
```

### Run Tests

```bash
# Run all tests
pytest

# With coverage report
pytest --cov=. --cov-report=html

# Run a specific test file
pytest tests/test_main.py -v
```

### Linting and Formatting with Ruff

```bash
# Check for lint issues
ruff check .

# Auto-fix issues
ruff check --fix .

# Format code
ruff format .

# Check formatting without changes
ruff format --check .
```

### Type Checking with Mypy

```bash
# Check types in a file
mypy main.py

# Check the entire project
mypy .

# Strict mode
mypy --strict .
```

### Jupyter Notebooks

Port 8888 is forwarded for Jupyter notebook sessions:

```bash
# Start a Jupyter notebook server
jupyter notebook --ip=0.0.0.0 --port=8888 --no-browser
```

Then open `http://localhost:8888` in your browser, or use the Jupyter extension directly in VS Code.

### Python 3.14 New Features

**T-strings (PEP 750):**
```python
name = "world"
greeting = t"Hello, {name}!"  # Returns a Template object, not a plain string
```

**Deferred annotation evaluation (PEP 649):**
```python
# Annotations are now deferred by default — no need for `from __future__ import annotations`
def process(data: list[MyClass]) -> MyClass:
    ...
```

**Free-threading (experimental):**
```bash
# Run without the GIL for true CPU-bound parallelism
python -X nogil script.py
```

## 🏗️ Project Structure

Recommended folder structure for a Python project:

```
my-python-project/
├── .devcontainer/
│   ├── devcontainer.json
│   └── Dockerfile
├── src/
│   └── my_package/
│       ├── __init__.py
│       └── main.py
├── tests/
│   ├── __init__.py
│   └── test_main.py
├── pyproject.toml
└── README.md
```

### Recommended `pyproject.toml`

```toml
[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

[project]
name = "my-project"
version = "0.1.0"
requires-python = ">=3.14"
dependencies = []

[dependency-groups]
dev = [
    "pytest>=8.0",
    "pytest-cov>=5.0",
    "mypy>=1.0",
    "ruff>=0.9",
]

[tool.ruff]
target-version = "py314"
line-length = 88

[tool.ruff.lint]
select = ["E", "F", "UP", "B", "SIM", "I"]

[tool.mypy]
python_version = "3.14"
strict = true

[tool.pytest.ini_options]
testpaths = ["tests"]
```

## 🐛 Troubleshooting

### Container won't build
- Ensure Docker Desktop is running
- Try rebuilding: `Dev Containers: Rebuild Container`
- Verify the base image is accessible: `docker pull mcr.microsoft.com/devcontainers/python:3.14`

### Python interpreter not found in VS Code
- Open the Command Palette: `Ctrl+Shift+P` → `Python: Select Interpreter`
- Choose the interpreter at `/usr/local/bin/python`

### uv not found
- Reinstall: `pip install uv`
- Or use the official installer: `curl -LsSf https://astral.sh/uv/install.sh | sh`

### Jupyter port not accessible
- Ensure port 8888 is forwarded (configured in `devcontainer.json`)
- Check VS Code's Ports panel: `Ctrl+Shift+P` → `Forward a Port`

### Ruff not formatting on save
- Verify Ruff is set as the default formatter: check `editor.defaultFormatter` in settings
- Check the Output panel (Ruff channel) for errors

## 📚 Additional Resources

### Python 3.14
- [What's New in Python 3.14](https://docs.python.org/3.14/whatsnew/3.14.html)
- [Python 3.14 Documentation](https://docs.python.org/3.14/)
- [PEP 649 – Deferred Evaluation of Annotations](https://peps.python.org/pep-0649/)
- [PEP 750 – Template Strings](https://peps.python.org/pep-0750/)

### Tooling
- [uv Documentation](https://docs.astral.sh/uv/)
- [Ruff Documentation](https://docs.astral.sh/ruff/)
- [pytest Documentation](https://docs.pytest.org/)
- [Mypy Documentation](https://mypy.readthedocs.io/)

## 🤝 Contributing

Suggestions for additional tools or improvements are welcome! Consider adding:
- Additional testing frameworks (hypothesis, nox, tox)
- Documentation tools (sphinx, mkdocs)
- Data science tools (numpy, pandas, matplotlib)
- Web framework starters (FastAPI, Django)

## 📄 License

This dev container configuration is available under the MIT License.

---

**Happy Coding!** 🐍
