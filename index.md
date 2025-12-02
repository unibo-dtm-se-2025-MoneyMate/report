---
title: Home
layout: home
has_children: false
nav_order: 1
---

# MoneyMate – Data Layer Artifact

### Authors

- [Andrea Giovanardi](mailto:andrea.giovanardi6@studio.unibo.it)
- [Matteo Fabbri](mailto:matteo.fabbri34@studio.unibo.it)
- [Cristian Romeo](mailto:cristian.romeo3@studio.unibo.it)

## Abstract

MoneyMate is a Python-based data layer for managing personal finance information.  
It provides a structured way to store and access data about users, contacts, categories, expenses, and transactions using a SQLite database. The core idea is to offer a clean, well-tested backend that can be reused in different contexts (for example, a GUI application or other tools) without rewriting the data management logic each time.

The project centers on a set of “managers” that expose clear operations (add, update, list, delete, calculate balances, etc.) with input validation and consistent behaviour. Listings are deterministic (stable ordering), operations are logged, and there is support for user roles (normal user vs. admin) and basic auditing. The current artifact is designed to run locally on a single machine, using SQLite as the storage engine and pytest as the main testing framework.


## Disclaimer

During the preparation of this work, the authors used AI-assisted tools (such as GitHub Copilot / ChatGPT) to help with code suggestions, documentation drafting, and text/code refinement.

After using these tools, the authors reviewed and edited the content as needed and take full responsibility for the content of the final report and artifact.
