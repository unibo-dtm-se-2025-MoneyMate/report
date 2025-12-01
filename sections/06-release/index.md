---
title: Release
has_children: false
nav_order: 7
---

# Release

## Produced artefacts

From the `unibo-dtm-se-2025-MoneyMate/artifact` codebase we produce one artefact:

- the **MoneyMate Python package**


## Target repositories

The artefacts are released to:

- **PyPI** (Python Package Index):  
  <https://pypi.org/project/MoneyMate/>

- **GitHub Releases**, as part of the main GitHub repository.  
  This provides a stable, versioned history of releases and downloadable artefacts and release notes for each version.

## Release process

Releases are **automated** and based on:

- a main branch in GitHub as the integration and release branch;
- a continuous integration pipeline that:
  - runs the test suite;
  - builds the Python package;
  - determines the next version number from commit history;
  - publishes the new version to PyPI and updates the GitHub Release.

Developers contribute via branches and pull requests; once changes are merged into the main branch and the pipeline succeeds, a new release is created without manual intervention.

---

## License

The published artefact is licensed under the **MIT License**.

This license is:

- permissive and business‑friendly;
- widely recognised and easy to adopt;
- suitable for integration into both open and closed source environments, which matches the intended usage of MoneyMate beyond a purely academic or IT‑specific context.

### License for source code

The source code is also released under the **MIT License**.

Using the same license for source code and artefacts:

- avoids ambiguity for users and organisations;
- ensures that what is visible on GitHub and what is installed from PyPI is governed by identical terms;
- keeps the legal model simple and consistent.

---

## Versioning schema

### Chosen schema and rationale

MoneyMate uses a **Semantic Versioning–style** schema:

- versions have the form `MAJOR.MINOR.PATCH`;
- it directly communicates the impact of a change (breaking change, new feature, or bugfix).

The version number is automatically derived from the commit history, following conventional commit categories.

### Meaning of MAJOR, MINOR, PATCH

- **MAJOR** increases when changes are not backward compatible for existing users or integrations.
- **MINOR** increases when new functionality is added in a backward‑compatible way.
- **PATCH** increases when backward‑compatible bug fixes or small improvements are released.

The version recorded in the repository, on PyPI, and on GitHub Releases is always the same and follows this `MAJOR.MINOR.PATCH` scheme.

### Criteria and workflow for new versions

- A new **PATCH** version is created when:
  - defects are fixed;
  - internal behaviour is improved without changing public interfaces.

- A new **MINOR** version is created when:
  - new features are added;
  - existing functionality remains compatible for current users.

- A new **MAJOR** version is created when:
  - existing public interfaces or behaviours change in a way that breaks compatibility;
  - users may need to adapt their integrations or workflows.

New releases are created by:

- merging the relevant changes into the main branch;
- letting the automated pipeline:
  - compute the appropriate version number based on the changes;
  - create the corresponding tag in the Git repository;
  - publish a new release on GitHub;
  - upload the corresponding artefacts to PyPI.
