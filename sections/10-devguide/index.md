---
title: Developer guide
has_children: false
nav_order: 11
---

# Developer Guide

This section explains how a new person can join the development of the `unibo-dtm-se-2025-MoneyMate/artifact` project and start contributing.

---

## 1. Organization & Communication

- **Repository**: [unibo-dtm-se-2025-MoneyMate/artifact](https://github.com/unibo-dtm-se-2025-MoneyMate/artifact)
- **Issues**:
  - Use **GitHub Issues** to report bugs, request features, or ask technical questions.
  - Before opening a new issue, search existing ones to avoid duplicates.
- **Discussion**:
  - Use comments on **Issues** and **Pull Requests** for design and code discussion.
  - Use the official course/team channels (e.g. forum/Teams) only for non-technical or organizational matters.

---

## 2. Internal Conventions

### 2.1 Branches

- **Release branch**: `main`  
  Contains only stable code, already tested.

- **Integration branch**: `developer`  
  All new functionality, bugfix and chore are integrated here berfore any pull request to the 'main'.

- **Topic branches** (created from `developer`, not `main`):
  - `feature/<short-description>`
  - `fix/<short-description>`
  - `chore/<short-description>`

### 2.2 Commits

- Use **Conventional Commits** (enables automated versioning and changelog):

  ```text
  type(scope): short description
  ```

  Examples:
  - `feat(expenses): add date filter`
  - `fix(users): prevent duplicate usernames`
  - `docs: describe MoneyMate architecture`


---

## 3. Development Environment (Windows)

### 3.1 Setup

On **Windows**:

```bat
git clone https://github.com/unibo-dtm-se-2025-MoneyMate/artifact.git
cd artifact

python -m venv .venv
.\.venv\Scripts\activate

pip install -r requirements.txt
pip install -r requirements-dev.txt  REM for pytest and dev tools
```

### 3.2 Running Tests

The project uses **pytest**. From the project root on Windows:

```bat
pytest
```

Run tests locally before pushing or opening a PR.

---

## 4. Development Workflow

### 4.1 Implementing a Change

1. Update `main`:

   ```bat
   git checkout main
   git pull origin main
   ```

2. Create a branch:

   ```bat
   git checkout -b feature/add-balance-endpoint
   REM or
   git checkout -b fix/login-bug
   ```

3. Make changes and add/update tests.
4. Run tests:

   ```bat
   pytest
   ```

5. Commit using Conventional Commits:

   ```bat
   git add .
   git commit -m "feat(api): add balance endpoint"
   ```

6. Push:

   ```bat
   git push origin feature/add-balance-endpoint
   ```

### 4.2 Creating a Pull Request

- On GitHub, open a **Pull Request** from your branch to `main`.
- In the description:
  - summarize the change
  - mention related issue(s), e.g. `Closes #12`.
- Wait for review, address comments, and merge once CI is green and approvals are given.

---

## 5. Tools & IDE Usage

### 5.1 Recommended Tools (Windows)

- **IDE/Editor**: VS Code, PyCharm, or similar.
- **Command line**:
  - `git status` – show changes
  - `git log --oneline --graph` – view history
  - `pytest` – run tests

### 5.2 Minimal VS Code Setup (Windows)

1. Open the `artifact` folder in VS Code.
2. Select interpreter:  
   Command Palette → “Python: Select Interpreter” → choose `.venv\Scripts\python.exe`.
3. Configure `pytest` as the default test framework (VS Code usually auto-detects it).
