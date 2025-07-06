#howto 

## 🧱 1. **Choose the Type of Project**

Start by defining what you're building. For example:

|Project Type|Common Tools|
|---|---|
|CLI Tool|`argparse`, `click`, `typer`|
|Web App|`Flask`, `FastAPI`, `Django`|
|Data Science|`jupyter`, `pandas`, `scikit`|
|Library/SDK|`setuptools`, `poetry`, `twine`|
|Microservice|`FastAPI`, `uvicorn`, `Docker`|

## 🗂️ 2. **Create a Clean Folder Structure**

A common structure for Python projects looks like this:
```
my_project/
├── src/
│   └── my_project/          ← Your main package code
│       ├── __init__.py
│       ├── core.py
│       └── utils.py
├── tests/                   ← Unit and integration tests
│   └── test_core.py
├── pyproject.toml           ← Build system & dependency manager        |                                (recommended)
├── README.md                ← Description, usage, instructions
├── .gitignore
├── requirements.txt         ← List of dependencies (optional with      |                              poetry)
└── setup.py                 ← Only for setuptools-based packaging
```


## 🐍 3. **Use a Virtual Environment**

Virtual environments isolate dependencies.

```
python -m venv .venv
source .venv/bin/activate  # Linux/macOS
.venv\Scripts\activate     # Windows
```


Alternatively, you can use `poetry`  OR  `Conda`:

```
poetry init
poetry shell
```

## 📦 4. **Use `pyproject.toml` for Modern Project Configuration**

`pyproject.toml` is the new standard for declaring build systems, dependencies, and configurations.

Example for a `poetry` project:

```
[tool.poetry]
name = "my-project"
version = "0.1.0"
description = "A task management tool"
authors = ["Your Name <you@example.com>"]

[tool.poetry.dependencies]
python = "^3.10"
click = "^8.1.0"

[tool.poetry.dev-dependencies]
pytest = "^7.0"

[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"
```

## 🔧 5. **Set Up Linters and Formatters**

Helps catch bugs and keep code consistent.

- **`black`** – automatic code formatting
    
- **`flake8`** – linting and style guide
    
- **`mypy`** – static type checker

``` 
pip install black flake8 mypy
black src/
flake8 src/
mypy src/
```

## 🧪 6. **Write and Run Tests**

Use `pytest` for simple and readable test cases.

```
pip install pytest
pytest tests/
```

Example:

```
# tests/test_core.py
from my_project.core import add

def test_add():
    assert add(2, 3) == 5
```

## 🧰 7. **Optional but Recommended**

| Tool / Feature     | Purpose                         |
| ------------------ | ------------------------------- |
| `.env` + `dotenv`  | Manage environment variables    |
| `Dockerfile`       | Containerize the app            |
| `pre-commit` hooks | Run checks before commits       |
| CI/CD config       | Automate testing and deployment |
| Type hints         | Improve readability and tooling |

