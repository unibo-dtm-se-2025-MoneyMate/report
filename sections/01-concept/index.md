---
title: Concept
has_children: false
nav_order: 2
---
## Concept

The product developed is **MoneyMate**: a desktop application designed to help users manage their expenses, track credits and debts with contacts, and gain insights into their financial habits through clear visualizations. The name “MoneyMate” directly reflects its main goal: providing a practical and friendly overview of spending and personal financial relationships.

### Type of product

MoneyMate is an **interactive desktop application with a graphical user interface (GUI)**, implemented in **Python**.

The project delivers:

- a **local desktop GUI application** for end users, built with **Tkinter** and ttk widgets;
- a **modular data layer** exposing a Python API over a SQLite database;
- an **analytics / visualization module** that embeds matplotlib charts inside the Tkinter GUI.

The main output of the project is the executable desktop application (run via `python -m MoneyMate`); the data layer can also be reused from scripts or tests, but it is not packaged as a standalone end‑user library or web service.

### Architecture overview

The application architecture is modular and is organized into three main components:

- **Database & Data Layer**

  The data layer, located under `MoneyMate/data_layer/`, defines and manages the SQLite database and exposes a high‑level Python API. Its responsibilities include:

  - Database connection and schema management (versioned SQLite backend).
  - CRUD operations for core entities:
    - **users** (registration, login/logout, roles, password management),
    - **categories** (expense categories),
    - **contacts**,
    - **expenses**,
    - **transactions** (credits/debts between users and contacts).
  - Deterministic listings with pagination and filtering (e.g., ordering by date, supporting date ranges and limits/offsets).
  - Balance and analytics computation (e.g., net balance, per‑contact breakdown).
  - Auditing of access events (login, logout, failed login attempts, etc.).
  - Structured logging.

  The GUI never accesses the database directly: it uses the functions provided by the data layer API.

- **User Interface & GUI Logic**

  The desktop GUI is implemented using **Tkinter** (standard Python library) and `ttk` widgets. The main window is defined in `MoneyMate/gui/app.py` as the `MoneyMateGUI` class, which:

  - Creates the root Tk window and global styles (colors, fonts, ttk themes).
  - Manages the logged‑in user context (`user_id`, `username`).
  - Registers and switches between different “screens” implemented as ttk frames:
    - `LoginFrame` and `RegisterFrame` (authentication),
    - `ExpensesFrame`,
    - `CategoriesFrame`,
    - `ContactsFrame`,
    - `TransactionsFrame`,
    - `ChartsFrame` (dashboard / analytics).
  - Shows a sidebar with navigation buttons once the user has logged in.
  - Wires GUI events (button clicks, form submissions) to the data layer API functions.

  Typical features available from the GUI include:

  - **Authentication**:
    - User registration and login via `LoginFrame` and `RegisterFrame`.
    - Logout handled by the root `MoneyMateGUI` (calling `api_logout_user` from the data layer).

  - **Expense management** (`ExpensesFrame`):
    - Add, edit, delete expenses.
    - Associate expenses with categories and, where applicable, contacts.
    - Search and filter expenses by title, category or date.

  - **Contacts and categories** (`ContactsFrame`, `CategoriesFrame`):
    - Create and manage contacts (names and optional details).
    - Create and manage expense categories.
    - List and search by name.

  - **Transactions (credits/debts)** (`TransactionsFrame`):
    - Record credits and debts with contacts.
    - View and filter transactions for the logged‑in user.
    - Remove transactions when settled.

  - **Dashboard and analytics** (`ChartsFrame`):
    - Visualize expenses and balances using charts.
    - Summarize credits and debts per contact.

  The GUI uses Tkinter `ttk.Treeview` widgets for tabular data (lists of expenses, contacts, transactions) and standard Tkinter dialogs (via `messagebox`) for feedback and error reporting.

- **Graphs & Analytics**

  The analytics module is implemented as part of the GUI, mainly in `ChartsFrame`. It uses **matplotlib** to generate charts and embeds them into the Tkinter window using the TkAgg backend. The dashboard:

  - Loads data via the data layer API (e.g., expenses, categories, per‑contact balance).
  - Computes and displays:
    - **Expenses by category** (pie or bar charts).
    - **Expense trend over time** (line charts).
    - **Transaction / balance summaries**, highlighting who owes whom and net balances.
  - Reacts to navigation by refreshing data each time the user opens the dashboard frame.

---

### Use case collection

This section summarizes the main usage scenarios for MoneyMate and addresses the required questions.

#### Where are the users?

MoneyMate targets **individual users** who need to manage personal or small‑scale shared finances. Typical examples are:

- Students or young professionals who split rent, utilities, and shared purchases with roommates.
- Workers and families who want to track recurring expenses (bills, groceries, subscriptions) and occasional debts between relatives and friends.
- Users who prefer a **local desktop tool** over a web service, for privacy or offline‑use reasons.

There is no geographical restriction: any user with a compatible desktop environment can use the application.

#### When and how frequently do they interact with the system?

Expected interaction patterns:

- **Short, frequent sessions**:
  - After each purchase or group expense, to record the new data.
  - At the end of the day or week, to insert multiple receipts at once.
- **Periodic review sessions**:
  - At least once per week or month, to:
    - check the evolution of expenses,
    - see who owes what,

#### How do they interact with the system? Which devices are they using?

Interaction is purely **graphical**, via the Tkinter desktop GUI:

- Users use a **keyboard and mouse (or touchpad)** to:
  - fill in forms (text entries, comboboxes, date fields),
  - click buttons to add/update/delete entries,
  - select rows in tables (Treeview) to edit or delete specific items,
  - navigate between screens using a sidebar of buttons (Dashboard, Expenses, Categories, Transactions, Contacts).

- The GUI runs on a **desktop or laptop computer**

There is no web-based or mobile client in the current project: all interactions happen in the **local Tkinter window**.

#### Does the system need to store users’ data? Which data? Where?

Yes. Persistent storage is essential to provide long‑term tracking and meaningful analytics.

- **Which data is stored?**

  Core data, managed by the data layer:

  - **User accounts**:
    - username, password hash, role (user/admin),
    - access logs (login/logout, failed login attempts).

  - **Contacts**:
    - name,
    - optional notes and metadata.

  - **Categories**:
    - category names for classifying expenses.

  - **Expenses**:
    - amount,
    - category,
    - date,
    - description,
    - ownership information (which user the expense belongs to),
    - optional link to a contact or other metadata.

  - **Transactions (credits/debts)**:
    - who owes whom (user/contact),
    - amount,
    - dates (creation, possibly due date),
    - status (open/closed),
    - relation to expenses where applicable.

  - **Derived and technical data**:
    - internal IDs and foreign keys,
    - timestamps and versioning information required by the data layer,
    - structured logs and audit events.

- **Where is data stored?**

  - In a **local SQLite database file** located in the MoneyMate directory.
  - For the GUI, a dedicated database file `moneymate_gui.db` is configured at startup (see `MoneyMate/gui/app.py`).
  - The file resides on the user’s machine; no remote database or external server is used in the current architecture.

As a consequence:

- There is **no automatic synchronization** between different devices.

#### User roles

The underlying data layer supports **roles and authentication** (user/admin), but the GUI is focused on the typical **authenticated end user** scenario.

Conceptually, we can distinguish:

- **Authenticated end user (primary GUI role)**

  - Registers an account and logs in through the GUI.
  - Performs all personal finance operations:
    - manage expenses, contacts, categories, and transactions,
    - explore charts and analytics,
    - log out when finished.
  - From the GUI perspective, this is the only role with direct interaction; role differences (e.g., admin) are mostly enforced in the backend or at API level, not via separate GUI panels.

- **Administrator / maintainer (project role)**

  - Not a separate graphical role in the current GUI, but a **technical role**:
    - configures and maintains the SQLite database,
    - manages packaging, distribution, and upgrades,
    - runs automated tests (data layer, GUI, system tests),
    - inspects logs and audit records if needed (outside the end‑user GUI).

The current version does **not** implement multi‑user concurrent sessions in a single GUI instance with differentiated permissions at GUI level. Each running instance of the application is effectively used by one authenticated user at a time.
