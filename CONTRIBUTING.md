# Contributing to WestQuant Open

Thank you for your interest in contributing to WestQuant Open! This document describes how to get started.

## Ways to contribute

- **Report bugs** — Open an issue on the relevant repo
- **Suggest features** — Start a discussion in [GitHub Discussions](https://github.com/orgs/WestQuantOpen/discussions)
- **Submit pull requests** — Fix bugs, add features, improve docs
- **Improve documentation** — Typos, clarity, examples
- **Write tests** — Help us improve coverage

## Getting started

1. Fork the repo you want to contribute to
2. Clone your fork:
   ```bash
   git clone https://github.com/YOUR_USERNAME/westquant.git
   cd westquant
   ```
3. Create a virtual environment:
   ```bash
   python -m venv .venv
   source .venv/bin/activate
   pip install -e ".[test]"
   ```
4. Create a branch:
   ```bash
   git checkout -b fix/my-bugfix
   ```
5. Make your changes and run tests:
   ```bash
   python -m pytest tests/ -v
   ```
6. Commit and push:
   ```bash
   git add .
   git commit -m "Fix: description of the fix"
   git push origin fix/my-bugfix
   ```
7. Open a pull request

## Code style

- Python 3.10+
- Follow existing patterns in the codebase
- Keep functions focused and well-documented
- Add tests for new functionality
- Run `python -m pytest tests/ -v` before submitting

## Pull request guidelines

- Keep PRs focused — one feature or fix per PR
- Write a clear description of what changed and why
- Link any related issues
- Ensure all tests pass

## Release process

We release monthly on the last Friday of each month. See [RELEASE_SCHEDULE.md](RELEASE_SCHEDULE.md).

## Questions?

- Open a [discussion](https://github.com/orgs/WestQuantOpen/discussions)
- Email: david@vesterlundventures.se
