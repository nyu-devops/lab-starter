# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This repository is a minimal starter for a Python/Flask project used in the NYU DevOps lab. It contains a `requirements.txt` with pinned dependencies, and a `setup.cfg` for flake8.

## Development Setup

The recommended workflow is to use VS Code with the Remote Containers extension. Clone the repo, open it in VS Code, and accept the prompt to reopen in a container. The container mounts the repository at `/app` and starts a Bash prompt there.

### Prerequisites (outside the container)

- Git
- Docker Desktop
- VS Code
- Remote Containers extension

Follow the steps in `README.md` for installation on macOS or Windows.

## Common Commands

| Task | Command | Notes |
|------|---------|-------|
| Install dependencies | `pip install -r requirements.txt` | Runs inside the container. |
| Run tests | `pytest` | Executes all tests. |
| Run a single test | `pytest path/to/test.py::test_name` | Replace with the actual test path and name. |
| Run tests with coverage | `coverage run -m pytest && coverage report` | Generates a coverage report in the terminal. |
| Lint | `flake8 .` | Uses the config in `setup.cfg`. |
| Static analysis | `pylint .` | |
| Format code | `black .` | |
| Check formatting | `black --check .` | |
| Run the Flask app (if present) | `FLASK_APP=app.py flask run` | Adjust `FLASK_APP` to your entry point. |
| Open the HTTPie CLI | `httpie` | Use for manual API testing. |

## Dependency Highlights

- `Werkzeug==3.0.1` – pinned to avoid breaking changes with Flask.
- `Flask==3.0.1` – the web framework used in the lab.
- `python-dotenv==0.21.1` – loads `.env` files.
- `pytest`, `pytest-pspec`, `pytest-cov` – testing framework and coverage.
- `coverage==7.3.2` – generates coverage reports.
- `pylint==3.0.2`, `flake8==6.1.0`, `black==23.10.1` – code quality tools.

## Docker / Remote Containers

- The container is automatically built by the Remote Containers extension.
- The container mounts the repo to `/app`. All commands should be run from `/app`.
- To stop the container: `docker stop <container-id>` and `docker rm <container-id>`.

## Environment Variables

The project supports `.env` files via `python-dotenv`. Place environment variables in a `.env` file at the repository root or in `/app` inside the container.

## Notes

- No build step is required; the project is interpreted at runtime.
- The repository contains no application code yet; add Python modules under `/app` and tests under `/app/tests`.
