---
title: CI/CD
has_children: false
nav_order: 9
---

# CI/CD
This section describes the continuous integration and continuous deployment (CI/CD) workflow of the MoneyMate project. 

### What is automated and why?

The project leverages GitHub Actions to automate both testing and releases. The overall workflow can be summarized in the following stages:

1. **Code validation and testing**
   - Every change triggers automated checks to validate code integrity and environment compatibility.
   - The test suite is executed (e.g., unit tests and other configured checks) to ensure that new changes do not introduce regressions.

2. **Versioning and changelog generation**
   - Semantic Versioning (SemVer: `MAJOR.MINOR.PATCH`) is applied automatically.
   - The new version number and the contents of `CHANGELOG.md` are derived from the Git commit history.
   - Commits are expected to follow the Conventional Commits convention so that changes can be correctly classified (e.g., fix, feat, breaking change).

3. **Artifact build and release**
   - A Python package distribution is built as the main release artifact.
   - This artifact is intended to be automatically:
     - tagged in the repository,
     - published to PyPI,
     - and attached to GitHub Releases.
   - Some parts of this release process are still under refinement and may not yet be fully operational.

4. **CI as a gate for CD**
   - Deployment (CD) is only triggered if all CI checks have completed successfully.
   - This prevents untested or unstable code from being released.
   - The use of `semantic-release` ensures that version bumps strictly follow SemVer rules based on the actual content of commits, avoiding arbitrary or inconsistent manual versioning by developers.

### How the workflow is implemented?
The CI/CD pipeline for the `unibo-dtm-se-2025-MoneyMate/artifact` repository is implemented using GitHub Actions workflows stored under `.github/workflows/`. In this repository:

- Continuous Integration (CI) workflows are triggered on events such as `push` and `pull_request` to relevant branches.  
- These CI workflows install the appropriate Python environment and project dependencies, then run the project’s automated tests to validate code correctness and compatibility.
- A dedicated deployment/release workflow is triggered only after CI has completed successfully and only from the Main branch (intended for release).
- The release workflow is responsible for building the project’s artifact(s) and publishing them to PyPI
