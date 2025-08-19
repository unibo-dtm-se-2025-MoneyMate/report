---
title: Concept
has_children: false
nav_order: 2
---
## Concept

The product developed is **MoneyMate**: a desktop application designed to help users manage their expenses, track credits and debts with contacts, and gain insights into their financial habits through clear visualizations. The name “MoneyMate” directly reflects its main goal—providing a practical and friendly overview of spending and personal financial relationships.

The idea originated from the need to organize personal budgets and monitor informal credits and debts among contacts. The application is meant to combine convenience, clarity, and analytical power, supporting users in everyday financial management.

The app architecture is modular, with three main components:

- **Database & Data Layer:** This module designs the SQLite schema, implements CRUD operations for expenses and transactions, validates input, and exposes a clear Python API for data access. The database structure includes tables for expenses, contacts, and transactions, allowing all relevant financial information to be stored and retrieved. Functions return standardized responses for integration with both the UI and analytics modules.

- **User Interface & GUI Logic:** The desktop GUI, built using Python libraries such as Tkinter or PyQt, enables users to add, view, search, and delete expenses, contacts, and transactions through intuitive forms and tables. The interface provides visual feedback for validation errors and is directly connected to the Data Layer via well-defined APIs, ensuring a smooth user experience.

- **Graphs & Analytics:** This module uses visualization libraries (e.g., matplotlib) to provide advanced graphs showing expenses by category, trends over time, and credits/debts per contact. Users can filter and analyze their data dynamically, gaining a clear understanding of their financial status.

The application is designed for anyone who wants to keep track of daily expenses and informal transactions, regardless of technical expertise. By integrating robust data management, an intuitive interface, and insightful analytics, **MoneyMate** simplifies budgeting and financial tracking for all users.

Here you should explain:
- The type of product developed with that project, for example (non-exhaustive):
    - Application (with GUI, be it mobile, web, or desktop)
    - Command-line application (CLI could be used by humans or scripts)
    - Library
    - Web-service(s)
    - Data processing toolkit (= Library + CLI, or Jupyter Notebook)

- Use case collection
    - Where are the users?
    - When and how frequently do they interact with the system?
    - How do they interact with the system? Which devices are they using?
    - Does the system need to store user's data? Which data? Where?
    - Most likely, there will be multiple roles.
