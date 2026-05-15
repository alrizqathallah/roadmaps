# 🐍 Python Learning Roadmap: Beginner to Advanced

> A comprehensive, structured, and practical guide to mastering Python — with exercises, mini-projects, and large capstone projects at every stage.

---

## How to Use This Roadmap

- Follow stages **in order** — each builds on the last.
- Complete **all exercises** before moving to projects.
- Aim to spend **consistent daily time** (1–2 hours minimum) rather than marathon sessions.
- Use the **recommended tools** listed at each stage.
- Track your progress by checking off each section.

---

## 🛠️ Setup & Environment

Before writing a single line of code, set up a productive environment.

### Tools to Install
- **Python 3.12+** — [python.org](https://python.org)
- **VS Code** with the Python extension (beginner-friendly)
- **PyCharm Community Edition** (great for larger projects)
- **Git & GitHub** — for version control from day one
- **Jupyter Notebook / JupyterLab** — for data science stages

### First Commands to Know
```bash
python --version
python -m venv venv          # Create a virtual environment
source venv/bin/activate     # Activate (Mac/Linux)
venv\Scripts\activate        # Activate (Windows)
pip install <package>
pip freeze > requirements.txt
```

---

## Stage 1 — Foundations (Weeks 1–3)

**Goal:** Understand Python syntax and write simple programs confidently.

### Core Concepts
- Variables and data types (`int`, `float`, `str`, `bool`)
- Type conversion and type checking (`type()`, `isinstance()`)
- Arithmetic, comparison, and logical operators
- String operations: indexing, slicing, formatting (`f-strings`)
- Getting user input with `input()`
- `print()` formatting and escape characters
- Comments and code readability

### Control Flow
- `if`, `elif`, `else` statements
- `while` loops
- `for` loops with `range()`
- `break`, `continue`, `pass`
- Nested loops and conditionals

### Data Structures
- **Lists** — creation, indexing, slicing, methods (`append`, `pop`, `sort`)
- **Tuples** — immutability and use cases
- **Dictionaries** — key-value pairs, methods (`get`, `keys`, `values`, `items`)
- **Sets** — uniqueness, set operations (`union`, `intersection`)

### Functions
- Defining functions with `def`
- Parameters, arguments, and return values
- Default parameters and keyword arguments
- Variable scope: local vs. global
- `*args` and `**kwargs` (introduction)

### Exercises
1. Write a program that converts temperatures (Celsius ↔ Fahrenheit ↔ Kelvin).
2. Create a number guessing game using a `while` loop.
3. Write a function that checks if a string is a palindrome.
4. Build a simple shopping list manager (add, remove, display items).
5. Write a program to count word frequency in a sentence using a dictionary.
6. Create a function to generate the Fibonacci sequence up to `n` terms.
7. Sort a list of student names and scores, display the top 3.

### 🔨 Mini-Projects
**1. Calculator App**
Build a command-line calculator that handles addition, subtraction, multiplication, division, and handles division-by-zero gracefully.

**2. Rock, Paper, Scissors Game**
A CLI game against the computer with a score tracker across multiple rounds.

**3. Mad Libs Generator**
Prompt the user for words (nouns, verbs, adjectives) and insert them into a story template using f-strings.

---

## Stage 2 — Intermediate Python (Weeks 4–7)

**Goal:** Write cleaner, more Pythonic code and handle real-world complexity.

### Functions — Deep Dive
- Lambda functions
- Higher-order functions: `map()`, `filter()`, `zip()`, `enumerate()`
- List, dict, and set comprehensions
- Generator expressions and `yield`
- Decorators (introduction)
- Recursion and base cases

### File Handling
- Reading and writing files (`open()`, `with` statement)
- Working with `.txt`, `.csv`, and `.json` files
- The `pathlib` and `os` modules
- Exception handling: `try`, `except`, `else`, `finally`, `raise`
- Custom exceptions

### Modules & Packages
- Importing standard library modules (`math`, `random`, `datetime`, `collections`)
- Creating your own modules
- Understanding `__name__ == "__main__"`
- Installing and using third-party packages with `pip`

### Object-Oriented Programming (OOP)
- Classes and objects
- `__init__` and instance attributes
- Instance methods, class methods (`@classmethod`), static methods (`@staticmethod`)
- Inheritance and `super()`
- Method overriding
- Encapsulation: name mangling (`_`, `__`)
- Magic/dunder methods: `__str__`, `__repr__`, `__len__`, `__eq__`
- Polymorphism

### Exercises
1. Write a recursive function to solve the Tower of Hanoi.
2. Use list comprehensions to filter and transform a list of dictionaries.
3. Parse a CSV file of student grades and compute averages.
4. Read a JSON config file and apply its settings to a simple program.
5. Build a `BankAccount` class with deposit, withdraw, and transaction history.
6. Implement a `Stack` and `Queue` class using Python lists.
7. Write a decorator that logs the execution time of any function.
8. Create a `Shape` hierarchy: `Circle`, `Rectangle`, `Triangle` with area/perimeter methods.

### 🔨 Mini-Projects
**1. Contact Book CLI App**
Store, search, update, and delete contacts saved to a JSON file. Use OOP with a `Contact` class and a `ContactBook` manager class.

**2. Expense Tracker**
Log daily expenses by category, save to CSV, and display a monthly summary with totals per category.

**3. Password Generator & Vault**
Generate secure passwords with custom rules (length, symbols, digits). Save credentials encrypted to a file using the `secrets` module.

---

## Stage 3 — Working with Data & APIs (Weeks 8–11)

**Goal:** Interact with the web, work with databases, and handle structured data.

### Web & APIs
- HTTP basics: GET, POST, status codes
- The `requests` library: fetching data, passing parameters, headers
- Parsing JSON responses
- REST API concepts
- Rate limiting and error handling for APIs
- Introduction to `httpx` for async requests

### Web Scraping
- HTML structure and the DOM
- `BeautifulSoup4`: parsing HTML, finding elements
- `selenium` for dynamic pages (introduction)
- Ethical scraping: `robots.txt`, rate limiting

### Databases
- SQL fundamentals: `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `JOIN`
- SQLite with Python's built-in `sqlite3`
- Introduction to `SQLAlchemy` ORM
- CRUD operations
- Database schema design

### Data Handling with `pandas`
- DataFrames and Series
- Reading CSV, Excel, JSON into DataFrames
- Filtering, grouping, and aggregating data
- Handling missing data
- Merging and joining DataFrames
- Exporting results

### Exercises
1. Fetch weather data from a public API (e.g., Open-Meteo) and display a 5-day forecast.
2. Scrape a Wikipedia page to extract a structured table.
3. Build a SQLite database for a library: books, authors, and borrowers.
4. Use `pandas` to analyze a CSV dataset — find outliers, compute statistics.
5. Create a script that checks if a set of URLs are reachable and logs the results.

### 🔨 Mini-Projects
**1. News Aggregator CLI**
Fetch top headlines from a news API (e.g., NewsAPI), filter by keyword or category, and display them in a formatted terminal output. Save favorites to a local database.

**2. Stock Price Tracker**
Pull historical stock data from a public API, store in SQLite, and display trends. Alert the user if a stock crosses a threshold.

**3. Movie Database App**
Scrape or use an API (e.g., OMDB) to search movies. Save watchlist to SQLite. Display ratings, genres, and summaries.

---

## Stage 4 — Software Engineering Practices (Weeks 12–14)

**Goal:** Write professional, maintainable, and testable Python code.

### Code Quality
- PEP 8 style guide
- Type hints and annotations (`mypy`)
- Docstrings and documentation (`sphinx`)
- `black` for formatting, `flake8` / `ruff` for linting

### Testing
- Unit testing with `unittest`
- `pytest`: fixtures, parametrize, assertions
- Test-Driven Development (TDD) workflow
- Mocking with `unittest.mock`
- Code coverage with `pytest-cov`

### Advanced Python Concepts
- Context managers (`with`, `__enter__`, `__exit__`)
- Iterators and the iterator protocol
- Generators and `yield from`
- `functools`: `lru_cache`, `partial`, `reduce`
- `dataclasses` and `namedtuple`
- Abstract base classes (`abc` module)
- Protocol types

### Concurrency
- Threading vs. multiprocessing vs. async
- `threading` module: threads, locks
- `multiprocessing` for CPU-bound tasks
- `asyncio`: event loops, `async`/`await`, coroutines
- `aiohttp` for async HTTP requests

### Project Structure & Packaging
- Organizing a Python project (`src/` layout)
- `__init__.py` and package design
- `pyproject.toml` and `setup.cfg`
- Building and publishing to PyPI (overview)
- Virtual environments with `poetry` or `uv`

### Exercises
1. Add type hints to a previous project and run `mypy` on it.
2. Write a full test suite for your `BankAccount` class using `pytest`.
3. Refactor your Expense Tracker to use `dataclasses`.
4. Build an async script that fetches 20 URLs concurrently with `asyncio` and `aiohttp`.
5. Write a context manager for safe file transactions (write to temp, then rename).

### 🔨 Mini-Projects
**1. CLI Task Manager with Tests**
A `todo` CLI tool with add/complete/delete/list commands, persistent JSON storage, full `pytest` coverage, type hints, and clean packaging.

**2. Async Web Scraper**
Scrape multiple pages concurrently with `asyncio` + `aiohttp`, parse results, and store structured data to SQLite.

---

## Stage 5 — Specialization Tracks (Weeks 15–22)

Choose one or more tracks based on your career goals. These run in parallel with continued practice.

---

### Track A — Web Development with Django / FastAPI

#### Concepts
- HTTP request/response cycle in depth
- **FastAPI**: path operations, Pydantic models, dependency injection, async endpoints
- **Django**: MTV architecture, ORM, admin panel, forms, templates
- REST API design principles (versioning, pagination, authentication)
- JWT and OAuth2 authentication
- PostgreSQL with `psycopg2` / `asyncpg`
- Deployment: Docker, Nginx, Gunicorn, cloud platforms

#### Mini-Projects
- **FastAPI**: Build a RESTful bookstore API with CRUD, JWT auth, and PostgreSQL.
- **Django**: Build a blog platform with user auth, posts, comments, and an admin panel.

---

### Track B — Data Science & Machine Learning

#### Concepts
- `numpy`: arrays, broadcasting, linear algebra
- `pandas`: advanced data wrangling
- `matplotlib` & `seaborn`: data visualization
- `scikit-learn`: preprocessing, models, pipelines, evaluation metrics
- Supervised learning: regression, classification
- Unsupervised learning: clustering, dimensionality reduction
- Model evaluation: cross-validation, confusion matrix, ROC-AUC
- Introduction to `PyTorch` or `TensorFlow`

#### Mini-Projects
- **EDA Dashboard**: Analyze a Kaggle dataset end-to-end with visualizations.
- **ML Pipeline**: Train and evaluate a classification model on a real dataset.
- **Neural Network**: Build a digit classifier with PyTorch on MNIST.

---

### Track C — Automation & DevOps

#### Concepts
- `subprocess` for shell commands
- `schedule` and `APScheduler` for task scheduling
- Automating browser tasks with `playwright`
- File system automation with `watchdog`
- Docker with Python apps
- CI/CD pipelines (GitHub Actions)
- Infrastructure as Code basics

#### Mini-Projects
- **File Organizer Bot**: Watch a folder and auto-sort files by extension/date.
- **Report Automation**: Generate weekly PDF/Excel reports from a database on a schedule.
- **CI/CD Pipeline**: Add GitHub Actions to lint, test, and deploy a Python app automatically.

---

## Stage 6 — Capstone Projects (Weeks 23–28)

These are substantial, portfolio-worthy projects that integrate multiple skills.

---

### 🏗️ Capstone 1 — Full-Stack CLI Finance Manager
**Skills:** OOP, file I/O, SQLite, `pandas`, testing, packaging

**Description:** A comprehensive personal finance tool accessible from the terminal.

**Features:**
- Multi-account support (checking, savings, credit)
- Transaction import from CSV (bank exports)
- Budget setting per category with alerts
- Monthly/yearly reports with spending trends
- Data visualization in the terminal using `rich`
- Full `pytest` suite with 80%+ coverage
- Packaged as an installable CLI tool

---

### 🏗️ Capstone 2 — Real-Time Data Dashboard
**Skills:** APIs, async, `pandas`, `FastAPI`, WebSockets, `SQLAlchemy`

**Description:** A web-based dashboard displaying live data (weather, stocks, crypto, or social trends).

**Features:**
- FastAPI backend with WebSocket support for real-time updates
- Async data fetching from multiple APIs
- PostgreSQL storage with time-series data
- Interactive frontend (use a simple HTML/JS template)
- Alerting system (email via `smtplib` or webhook)
- Dockerized for deployment

---

### 🏗️ Capstone 3 — Machine Learning Web App
**Skills:** `scikit-learn`, `FastAPI`, `pandas`, Docker, model serialization

**Description:** Train a predictive ML model and serve it as a REST API with a simple UI.

**Features:**
- End-to-end ML pipeline: data cleaning → feature engineering → model training → evaluation
- Model serialization with `joblib`
- FastAPI endpoints for predictions (`/predict`)
- Input validation with Pydantic
- Simple frontend form for user input
- Containerized with Docker
- Model versioning and logging

---

### 🏗️ Capstone 4 — Automated Research Assistant
**Skills:** `asyncio`, APIs, `LangChain` or direct LLM APIs, SQLite, scheduling

**Description:** A tool that monitors topics of interest, collects articles, summarizes them with an LLM, and delivers daily digests.

**Features:**
- Async scraping of RSS feeds and news APIs
- Summarization using an LLM API (OpenAI / Anthropic)
- Topic filtering and relevance scoring
- SQLite storage with deduplication
- Daily email digest with formatted HTML
- Configurable via a YAML file
- Scheduled with `APScheduler`

---

## 📚 Learning Resources

### Books
| Title | Level | Best For |
|---|---|---|
| *Automate the Boring Stuff with Python* — Al Sweigart | Beginner | Practical automation |
| *Python Crash Course* — Eric Matthes | Beginner | Structured foundation |
| *Fluent Python* — Luciano Ramalho | Advanced | Deep Python mastery |
| *Python Cookbook* — David Beazley | Intermediate/Advanced | Idiomatic patterns |
| *Architecture Patterns with Python* — Percival & Gregory | Advanced | Software design |

### Interactive Platforms
- **Exercism.io** — Peer-reviewed Python exercises
- **LeetCode / HackerRank** — Algorithm and data structure challenges
- **Kaggle** — Data science competitions and notebooks
- **Real Python (realpython.com)** — In-depth tutorials
- **PyMOTW (pymotw.com)** — Standard library deep dives

### Video Courses
- *CS50P* — Harvard's Python course (free, excellent)
- *Python for Everybody* — Dr. Chuck on Coursera (beginner-friendly)
- *Talk Python to Me* — Podcast for ongoing learning

---

## 🗓️ Suggested Weekly Schedule

| Week | Focus |
|---|---|
| 1–3 | Stage 1: Foundations |
| 4–7 | Stage 2: Intermediate Python + OOP |
| 8–11 | Stage 3: Data, APIs, Databases |
| 12–14 | Stage 4: Software Engineering Practices |
| 15–22 | Stage 5: Specialization Track |
| 23–28 | Stage 6: Capstone Projects |

**Daily habit:**
- 30 min — Review concepts / read docs
- 45 min — Write code (exercises or project)
- 15 min — Review, refactor, commit to GitHub

---

## ✅ Progress Checklist

### Stage 1
- [ ] Understand all basic data types and operators
- [ ] Write programs using loops and conditionals
- [ ] Use lists, dicts, sets, and tuples fluently
- [ ] Define and call functions with various argument types
- [ ] Complete all Stage 1 exercises
- [ ] Complete Calculator, Rock-Paper-Scissors, and Mad Libs projects

### Stage 2
- [ ] Use comprehensions and lambdas fluently
- [ ] Handle files and exceptions reliably
- [ ] Build and use custom modules
- [ ] Design OOP programs with inheritance
- [ ] Complete all Stage 2 exercises
- [ ] Complete Contact Book, Expense Tracker, and Password projects

### Stage 3
- [ ] Fetch and parse data from at least 2 real APIs
- [ ] Scrape a website responsibly
- [ ] Design and query a SQLite database
- [ ] Analyze a dataset with `pandas`
- [ ] Complete all Stage 3 mini-projects

### Stage 4
- [ ] Apply type hints across a full project
- [ ] Write tests with `pytest` achieving 80%+ coverage
- [ ] Use async/await in a real project
- [ ] Structure a project for packaging

### Stage 5 & 6
- [ ] Complete chosen specialization track
- [ ] Finish at least 2 capstone projects
- [ ] Publish code to GitHub with READMEs
- [ ] Deploy at least 1 project publicly

---

## 💡 Key Principles for Success

1. **Code every day** — Even 20 minutes of consistent practice beats 4-hour weekend sprints.
2. **Read error messages** — They are your best teachers. Don't skip them.
3. **Build things you care about** — Motivation stays high when projects are personally meaningful.
4. **Read other people's code** — Browse GitHub repos in your area of interest.
5. **Teach what you learn** — Write blog posts, make notes, or explain concepts to others.
6. **Embrace the debugger** — Learn `pdb` or VS Code's debugger early; print-debugging has limits.
7. **Use version control from day one** — Commit every meaningful change to Git.
8. **Embrace failure** — Broken code is not failure; never trying is.

---

*Last updated: 2026 — Python 3.12+ recommended throughout.*