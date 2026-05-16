# 🐍 Python Learning Roadmap: Beginner to Advanced
### Industry-Focused · Practical · Implementable

> **How to use this roadmap:** Follow phases sequentially. Complete all exercises and mini-projects before moving on. Each phase builds directly on the previous. Estimated hours are guidelines — prioritize understanding over speed.

---

## 📍 Phase 0 — Environment Setup & Orientation
**Duration:** 1–2 days | **Goal:** Get a working environment and understand the Python ecosystem

### Setup Checklist
- Install Python 3.12+ from [python.org](https://python.org)
- Install VS Code + Python extension (or PyCharm Community)
- Learn to use the terminal/command prompt
- Understand `pip` (Python's package manager)
- Create your first virtual environment: `python -m venv .venv`

### Key Concepts
- What is Python? Where is it used in industry? (Web, Data, AI/ML, Automation, DevOps)
- Interpreted vs compiled languages
- Python's ecosystem: standard library vs third-party packages
- The REPL (interactive shell): `python` or `ipython`

---

## 🟢 Phase 1 — Python Fundamentals
**Duration:** 3–5 weeks | **Goal:** Write correct, readable Python from scratch

### 1.1 Core Syntax & Data Types
- Variables and assignment
- Primitive types: `int`, `float`, `str`, `bool`, `NoneType`
- Type checking with `type()` and `isinstance()`
- String formatting: f-strings, `.format()`, multiline strings
- Basic input/output: `print()`, `input()`

### 1.2 Control Flow
- `if`, `elif`, `else`
- `for` loops (iterating over sequences)
- `while` loops and `break`/`continue`
- List comprehensions (introduce early, use often)
- `match`/`case` (Python 3.10+ structural pattern matching)

### 1.3 Data Structures
| Structure | Use Case | Key Operations |
|-----------|----------|----------------|
| `list` | Ordered, mutable sequences | append, sort, slice, pop |
| `tuple` | Immutable sequences, unpacking | indexing, unpacking |
| `dict` | Key-value mappings | get, update, items, defaultdict |
| `set` | Unique collections, membership tests | union, intersection, difference |

### 1.4 Functions
- Defining functions with `def`
- Parameters: positional, keyword, `*args`, `**kwargs`, defaults
- Return values and `None`
- Variable scope: local vs global
- Lambda functions
- Docstrings and type hints (introduce from the start)

### 1.5 Error Handling
- `try`, `except`, `else`, `finally`
- Common exceptions: `ValueError`, `TypeError`, `KeyError`, `FileNotFoundError`
- Raising exceptions with `raise`

### 📝 Exercises (Phase 1)
1. **Temperature Converter** — convert between Celsius, Fahrenheit, Kelvin using functions
2. **Word Frequency Counter** — count word occurrences in a string using a `dict`
3. **FizzBuzz Pro** — extend classic FizzBuzz with configurable rules via a `dict`
4. **List Sorter** — implement bubble sort manually, then compare with `sorted()`
5. **Simple Calculator REPL** — loop-based calculator with error handling for invalid input

### 🔨 Mini-Project 1: Contact Book CLI
Build a command-line contact manager using a `dict` of dicts. Features:
- Add, view, search, and delete contacts
- Save to and load from a `.txt` file
- Input validation with helpful error messages
- Clean, menu-driven interface

---

## 🟡 Phase 2 — Intermediate Python
**Duration:** 5–7 weeks | **Goal:** Write modular, organized, Pythonic code

### 2.1 Object-Oriented Programming (OOP)
- Classes and instances
- `__init__`, `__str__`, `__repr__`, and other dunder methods
- Instance vs class vs static methods
- Inheritance and `super()`
- Composition over inheritance (real-world pattern)
- `@property` and `@setter` decorators
- Abstract base classes with `abc`

### 2.2 Modules & Packages
- `import`, `from ... import`, aliasing
- Creating your own modules and packages (`__init__.py`)
- Python standard library deep dive:
  - `os`, `pathlib` — file system operations
  - `sys` — system interactions
  - `datetime`, `time` — date and time handling
  - `json`, `csv` — data serialization
  - `re` — regular expressions
  - `collections` — `Counter`, `defaultdict`, `namedtuple`, `deque`
  - `itertools`, `functools` — functional programming tools

### 2.3 File I/O & Data Handling
- Reading and writing files (text and binary)
- Context managers (`with` statement)
- Working with CSV files using `csv` module
- Working with JSON data
- Parsing and writing to files safely

### 2.4 Decorators & Closures
- First-class functions and closures
- Writing simple decorators
- Stacking decorators
- `functools.wraps` — preserving function metadata
- Practical decorators: timing, logging, retry logic

### 2.5 Generators & Iterators
- The iterator protocol (`__iter__`, `__next__`)
- Generator functions with `yield`
- Generator expressions
- `itertools` for lazy computation
- Why generators matter for memory efficiency

### 2.6 Comprehensions & Functional Tools
- List, dict, and set comprehensions
- Nested comprehensions
- `map()`, `filter()`, `zip()`, `enumerate()`
- `functools.reduce()`

### 2.7 Virtual Environments & Dependency Management
- `venv` and activating environments
- `pip freeze` and `requirements.txt`
- Introduction to `pyproject.toml`
- Pinning dependencies for reproducibility

### 📝 Exercises (Phase 2)
1. **OOP Bank Account** — implement `BankAccount` class with transactions, overdraft protection, and history
2. **Regex Email Validator** — validate and extract emails from a block of text
3. **File Organizer Script** — sort files in a directory into subfolders by extension using `pathlib`
4. **Decorator Stack** — write `@timer`, `@logger`, and `@retry(n)` decorators and apply all three to a function
5. **Lazy Number Stream** — build a generator that yields prime numbers indefinitely

### 🔨 Mini-Project 2: CSV Data Analyzer
Load a real-world CSV dataset (e.g., sales data, weather, or employee records). Features:
- Parse and validate the CSV using the `csv` module
- Compute statistics: average, min, max, totals, grouped aggregates
- Filter rows by criteria (CLI flags)
- Export results to a new CSV and a JSON summary
- Clean OOP design with separate `DataLoader`, `Analyzer`, and `Reporter` classes

---

## 🟠 Phase 3 — Professional Python Practices
**Duration:** 4–6 weeks | **Goal:** Write production-quality, maintainable code like a professional

### 3.1 Testing
- Why testing matters in industry
- `unittest` — built-in testing framework
- `pytest` — industry standard (fixtures, parametrize, plugins)
- Test-driven development (TDD) workflow
- Mocking with `unittest.mock`
- Code coverage with `pytest-cov`
- Testing patterns: unit, integration, end-to-end

### 3.2 Type Hints & Static Analysis
- Type hints: `int`, `str`, `list[int]`, `dict[str, Any]`, `Optional`, `Union`
- `typing` module: `TypeVar`, `Generic`, `Protocol`, `Callable`
- Python 3.10+ union syntax: `int | str`
- Running `mypy` for static type checking
- Using `Pydantic` for runtime data validation (industry standard)

### 3.3 Logging & Debugging
- `logging` module: levels, handlers, formatters
- Structured logging for production systems
- Using `pdb` and `breakpoint()` for debugging
- Profiling with `cProfile` and `line_profiler`
- Reading tracebacks confidently

### 3.4 Configuration & Environment
- `python-dotenv` for `.env` files
- `argparse` for command-line interfaces
- `configparser` for `.ini` files
- 12-factor app configuration principles

### 3.5 Code Quality & Standards
- PEP 8 style guide
- Formatting with `ruff` or `black`
- Linting with `ruff` or `flake8`
- Pre-commit hooks for automated checks
- Code review best practices

### 3.6 Documentation
- Writing effective docstrings (Google style, NumPy style)
- `Sphinx` for generating documentation
- `README.md` best practices
- Inline comments: when to use and when not to

### 📝 Exercises (Phase 3)
1. **Test Suite for Phase 2 Projects** — write full `pytest` test suites for your bank account and CSV analyzer
2. **Typed Refactor** — add complete type hints to a previous project and verify with `mypy`
3. **CLI Tool with argparse** — build a flexible CLI wrapper around your file organizer
4. **Logging Pipeline** — add structured logging to a project with file and console handlers
5. **Mock API Test** — test a function that makes HTTP calls by mocking `requests` responses

### 🔨 Mini-Project 3: Task Manager API (without a framework)
Build a JSON-based REST-like task manager using only Python's `http.server`:
- CRUD operations for tasks (stored in JSON)
- Request routing by method and path
- Input validation using type hints and `Pydantic`
- Full `pytest` test suite with mocks
- Logging of all requests and errors
- CLI for starting the server with configurable port

---

## 🔴 Phase 4 — Specialized Tracks
**Duration:** 6–10 weeks | **Choose your path based on your target industry role**

> ⚠️ Pick **one primary track** to focus on. Explore others after. Each track concludes with a capstone project.

---

### 🌐 Track A: Web Development
**Stack:** FastAPI, SQLAlchemy, PostgreSQL, Docker

#### Topics
- HTTP fundamentals: methods, status codes, headers, JSON
- **FastAPI** — modern, async web framework with automatic docs
  - Path parameters, query params, request bodies
  - Dependency injection
  - Background tasks
  - Middleware
- **SQLAlchemy** — ORM for database interaction
  - Models and relationships (one-to-many, many-to-many)
  - Migrations with `Alembic`
  - Async SQLAlchemy
- Authentication: JWT tokens, OAuth2 patterns
- **Pydantic** for request/response schemas
- REST API design principles and best practices
- Docker basics: containerizing your application
- Environment-based configuration

#### 🔨 Capstone Project A: Full-Stack REST API — "DevBoard"
A project and task management API (like a lightweight Jira):
- User registration and JWT authentication
- Projects with teams, tasks with priorities and due dates
- Filtering, pagination, and sorting on all list endpoints
- Background task: email notification simulation on task assignment
- Full test suite: unit + integration tests with a test database
- Dockerized with `docker-compose` (app + PostgreSQL)
- OpenAPI documentation auto-generated by FastAPI

---

### 📊 Track B: Data Engineering & Analytics
**Stack:** pandas, NumPy, SQLAlchemy, Airflow (concepts), Polars

#### Topics
- **NumPy** — arrays, broadcasting, vectorized operations
- **pandas** — DataFrames, Series, indexing, groupby, merge/join, reshaping
- Data cleaning: missing values, duplicates, outliers, type coercion
- **Polars** — high-performance modern alternative to pandas
- SQL with Python: `sqlite3`, `SQLAlchemy`, writing efficient queries
- Data pipelines: ETL (Extract, Transform, Load) patterns
- **Matplotlib** and **Seaborn** — data visualization
- **Plotly** — interactive charts
- Working with APIs to ingest data
- Data validation with **Great Expectations** (concepts)
- Introduction to **Apache Airflow** concepts for orchestration

#### 🔨 Capstone Project B: End-to-End Data Pipeline — "SalesInsight"
Automated sales analytics pipeline from raw data to dashboard:
- Ingest raw CSV sales data from multiple sources
- Clean, validate, and transform using pandas/Polars
- Load into a SQLite or PostgreSQL database
- Run automated analytics: trends, top products, regional breakdowns, cohort analysis
- Generate a static HTML report with Plotly charts
- Schedule pipeline runs with a simple cron or Airflow DAG
- Unit-tested transformation functions

---

### 🤖 Track C: AI / Machine Learning Engineering
**Stack:** scikit-learn, PyTorch, FastAPI, Hugging Face

#### Topics
- Machine learning fundamentals (supervised, unsupervised, evaluation)
- **scikit-learn** — preprocessing, pipelines, cross-validation, model selection
- Core algorithms: linear/logistic regression, decision trees, random forests, SVMs, k-means
- **PyTorch** basics — tensors, autograd, neural network fundamentals
- Fine-tuning with **Hugging Face Transformers**
- Model evaluation: accuracy, precision, recall, F1, ROC-AUC, confusion matrix
- Feature engineering and selection
- Saving and loading models (`pickle`, `joblib`, ONNX)
- Serving ML models with **FastAPI**
- Responsible AI: bias, explainability (SHAP concepts)

#### 🔨 Capstone Project C: ML-Powered API — "SentimentEngine"
End-to-end sentiment analysis service:
- Train a custom classifier on a real dataset (e.g., IMDB, Yelp reviews)
- Fine-tune a pre-trained Hugging Face model for improved accuracy
- Compare both approaches with a rigorous evaluation report
- Serve predictions via a FastAPI endpoint with confidence scores
- Batch prediction endpoint for large input files
- Model versioning and experiment tracking concepts
- Dockerized deployment

---

### ⚙️ Track D: Automation & DevOps
**Stack:** subprocess, Fabric, Ansible concepts, CI/CD, Docker

#### Topics
- **subprocess** — running shell commands from Python
- **paramiko** — SSH automation
- **Fabric** — remote server automation
- File system automation with `pathlib`, `shutil`, `watchdog`
- Web scraping: `requests`, `BeautifulSoup`, `Playwright`
- Scheduling: `schedule`, `APScheduler`, cron
- **GitHub Actions** — writing CI/CD pipelines in YAML
- Docker and Docker Compose for application packaging
- Secrets management in automated environments
- Writing idempotent automation scripts

#### 🔨 Capstone Project D: Automated DevOps Toolkit — "OpsPilot"
A CLI toolkit for automating common developer operations:
- Environment setup automation: create venv, install deps, check versions
- Automated backup: compress and archive project directories with versioning
- Web scraper: monitor a webpage for changes and send an alert
- GitHub Actions workflow: auto-test and lint on pull requests
- Health check script: ping services and generate a status report
- Fully tested, documented, and packaged as a distributable CLI tool

---

## 🔵 Phase 5 — Advanced Python Internals
**Duration:** 4–6 weeks | **Goal:** Understand Python deeply and write high-performance code

### 5.1 Concurrency & Parallelism
- The GIL (Global Interpreter Lock) — what it is and what it means
- **Threading** — I/O-bound tasks, `ThreadPoolExecutor`
- **Multiprocessing** — CPU-bound tasks, `ProcessPoolExecutor`, shared memory
- **asyncio** — event loop, `async`/`await`, coroutines, tasks
- `aiohttp` for async HTTP, `asyncpg` for async database access
- Choosing the right concurrency model for the job

### 5.2 Memory & Performance
- Python's memory model: reference counting, garbage collection
- `sys.getsizeof()`, `tracemalloc` for memory profiling
- `__slots__` for memory-efficient classes
- Lazy evaluation and generators for large data
- Profiling with `cProfile`, `line_profiler`, `py-spy`
- Optimization strategies: vectorization, caching with `functools.lru_cache`

### 5.3 Metaprogramming
- `__getattr__`, `__setattr__`, `__delattr__`
- Metaclasses and `__class_getitem__`
- Descriptors (`__get__`, `__set__`, `__delete__`)
- `dataclasses` and `attrs` — declarative class generation
- Dynamic class creation with `type()`
- `ast` module — inspecting and modifying Python source trees

### 5.4 Packaging & Distribution
- `pyproject.toml` — modern project configuration
- Building packages with `build` and `setuptools`
- Publishing to PyPI (test instance)
- Semantic versioning
- `tox` for testing across Python versions
- Writing a proper `README`, `LICENSE`, `CHANGELOG`

### 5.5 Security Best Practices
- Input sanitization and injection prevention
- Handling secrets securely (never hardcode, use env vars/vaults)
- SQL injection prevention (parameterized queries)
- Dependency vulnerability scanning with `pip-audit` or `safety`
- Understanding common CVEs in Python packages

### 📝 Exercises (Phase 5)
1. **Async Web Scraper** — scrape 100 URLs concurrently using `asyncio` + `aiohttp`, compare to sequential
2. **Memory Profiler** — compare memory usage of a list vs generator for 1M records using `tracemalloc`
3. **Custom Descriptor** — implement a `Validated` descriptor that enforces type and range constraints
4. **Thread-Safe Counter** — implement a counter shared across 100 threads using locks
5. **Package Release** — take any mini-project and publish it to TestPyPI with proper metadata

### 🔨 Final Capstone: Production-Grade Python Application
Build a fully production-ready application of your choosing that combines multiple skills:

**Requirements (all must be met):**
- [ ] Follows a clean architecture (layered or hexagonal)
- [ ] Full OOP design with correct use of inheritance and composition
- [ ] Complete type hints verified by `mypy`
- [ ] `pytest` test suite with >80% coverage
- [ ] Async where appropriate (API calls, I/O)
- [ ] Structured logging throughout
- [ ] Configuration via environment variables
- [ ] Dockerized with `docker-compose`
- [ ] CI/CD via GitHub Actions (lint, type-check, test)
- [ ] Published documentation
- [ ] Proper `pyproject.toml` and README

**Suggested ideas:** URL shortener service, personal finance tracker API, real-time chat using WebSockets, automated code review bot, custom monitoring dashboard.

---

## 📚 Curated Resources

### Books
| Title | Level | Focus |
|-------|-------|-------|
| *Python Crash Course* — Eric Matthes | Beginner | Core fundamentals |
| *Fluent Python* — Luciano Ramalho | Intermediate–Advanced | Idiomatic Python |
| *Effective Python* — Brett Slatkin | Intermediate | Best practices (90 items) |
| *Architecture Patterns with Python* — Percival & Gregory | Advanced | Software design |
| *High Performance Python* — Gorelick & Ozsvald | Advanced | Optimization |

### Online Platforms
- **Real Python** (realpython.com) — practical, industry-focused tutorials
- **Python Docs** (docs.python.org) — always the authoritative reference
- **TestDriven.io** — test-driven and DevOps-focused Python
- **Full Stack Python** — curated guide by topic

### Practice
- **Exercism.io** — mentored coding exercises
- **LeetCode** (Easy/Medium in Python) — algorithmic thinking
- **Advent of Code** — annual challenges, great for problem-solving

---

## 🗓️ Recommended Study Schedule

| Phase | Commitment | Timeline |
|-------|-----------|----------|
| Phase 0: Setup | 1–2 hrs/day | Week 1 |
| Phase 1: Fundamentals | 1–2 hrs/day | Weeks 2–5 |
| Phase 2: Intermediate | 1.5–2 hrs/day | Weeks 6–12 |
| Phase 3: Professional Practices | 1.5–2 hrs/day | Weeks 13–18 |
| Phase 4: Specialization Track | 2 hrs/day | Weeks 19–28 |
| Phase 5: Advanced Internals | 2 hrs/day | Weeks 29–36 |

> 💡 **Tip:** Consistency beats intensity. 90 minutes daily outperforms 8-hour weekend sessions.

---

## ✅ Progress Tracker

Use this checklist to mark your progress:

- [ ] Phase 0 complete — environment running, first script written
- [ ] Phase 1 complete — Contact Book CLI project done
- [ ] Phase 2 complete — CSV Data Analyzer project done
- [ ] Phase 3 complete — Task Manager API project done
- [ ] Phase 4 Track chosen: ___________
- [ ] Phase 4 Capstone complete
- [ ] Phase 5 complete — Final production-grade project shipped

---

*Roadmap version 1.0 · Python 3.12+ · Updated May 2026*