---
title: Requirements
has_children: false
nav_order: 3
---

# Requirements

This section defines the requirements for the **MoneyMate** desktop application, as implemented in the `unibo-dtm-se-2025-MoneyMate/artifact` repository.  

## User stories

Below is a rewritten **Personas** subsection you can drop into your `index_Version8.md`, keeping only **Regular user** and **Administrator / Maintainer** but making them richer “persona-style” like your friend’s example.

### Personas

#### Persona 1 – Regular User: *Giulia Rossi*

**Profile**

- **Age:** 23  
- **Occupation:** Computer Science student living with two roommates  
- **Tech skills:** Confident with basic software (Office, browsers, messaging apps), not a programmer  
- **Devices:** Personal laptop (Windows), smartphone  

**Biography**

Giulia has recently moved to another city for university and now shares an apartment with two friends. They split rent, utilities, groceries and often pay each other back via bank transfers or cash. Giulia is usually the one who anticipates common expenses (e.g., buying monthly transit passes or household items) and then has to remember who owes what.  

In the past she tried to manage everything with Excel sheets and chat messages, but she often loses track of which transfers have already been made and which are still pending. She wants a simple desktop tool she can keep on her laptop that helps her record expenses and debts without needing any advanced financial knowledge.

**Motivations**

- Keep a **clear, up‑to‑date view** of how much she is spending each month.  
- **Avoid conflicts** with her roommates about who has already paid and who still owes money.  
- Have a **single place** where expenses, contacts and transactions are stored, without spreading information across multiple chats and spreadsheets.  
- Understand her **spending habits** over time (e.g., how much she spends on transport, groceries, leisure).

**Goals**

- Quickly **add new expenses** with category, description and (optionally) a roommate/contact.  
- **Record debts and credits** with each roommate, and see at a glance who owes whom.  
- **Filter and search expenses** when she needs to check a specific purchase or a period (e.g., last month’s utilities).  
- Use **charts and summaries** to understand which categories cost her the most.

**Frustrations**

- Losing track of debts when people pay her back in different ways (cash, bank transfer, apps).  
- Tools that are **too complex**, full of accounting jargon or requiring manual formulas.  
- Having to **re‑enter the same information** multiple times (e.g., contact details, categories).  
- Systems that crash, freeze or **do not give clear feedback** when something goes wrong.  
- Fear that a mistake (e.g., deleting an expense by accident) will silently break the totals.

## Requirements analysis

The requirements observed to build the application can be divided into functional, non-functional and implementation needs.

The FUNCTIONAL REQUIREMENTS involve:

ID | Requirement | Acceptance Criteria
---|------------|--------------------
F1 | The system must allow users to register a new account with username and password. | Checked when a user can complete registration via GUI, a new user record is created in the SQLite database, and the same credentials can be used to log in successfully.
F2 | The system must allow users to log in and log out via a graphical interface. | Checked when, with valid credentials, the main GUI (sidebar + dashboard) is shown, and when clicking “Logout” the session is cleared and the login screen is displayed again.
F3 | The system must allow users to add a new expense with at least amount, date, category and description. | Checked when an expense created via the GUI appears in the expenses table, is persisted in the database through the data layer API, and is used in subsequent analytics.
F4 | The system must allow users to view, search and filter their expenses. | Checked when opening the Expenses screen shows a list of expenses and applying filters/search (e.g., by text or date range) returns only matching rows.
F5 | The system must allow users to edit an existing expense. | Checked when modifying one or more fields of a selected expense and saving updates the corresponding record in the database and the GUI list, without creating duplicates.
F6 | The system must allow users to delete an existing expense they own. | Checked when deleting a selected expense removes it from the GUI list and it is no longer returned by the data layer nor counted in balances/analytics.
F7 | The system must allow users to create, view and delete expense categories. | Checked when categories added via the GUI appear in the categories list, can be selected when adding expenses, and can be deleted according to the semantics enforced in the data layer.
F8 | The system must allow users to create, view and delete contacts. | Checked when contacts added via the GUI appear in the contacts list, can be used when creating transactions, and are removed from the list when deleted.
F9 | The system must allow users to record transactions representing credits and debts with contacts. | Checked when creating a transaction with a contact and amount adds a row to the transactions list and the transaction is stored via the data layer API.
F10 | The system must allow users to view and manage their transactions. | Checked when the Transactions screen loads all transactions for the logged-in user, and deleting/closing a transaction updates the list and related balances.
F11 | The system must compute and show the user’s net balance and per-contact breakdown. | Checked when summary views (Transactions/Charts) display a net balance and per-contact amounts consistent with stored transactions.
F12 | The system must provide a dashboard with charts for expenses and balances. | Checked when the Charts screen displays charts (e.g., expenses by category, expenses over time, balance summaries) built using matplotlib and refreshed from the data layer.
F13 | The system must validate required input fields in GUI forms before saving. | Checked when attempts to save expenses, contacts, categories or transactions with missing/invalid required fields are rejected and a clear error message is shown.
F14 | The system must restrict access so that each user can only access their own data. | Checked when tests and manual checks confirm that expenses, contacts, categories and transactions created under one user account are not visible or modifiable from another account.

The NON-FUNCTIONAL REQUIREMENTS touch:

ID | Requirement | Acceptance Criteria
---|------------|--------------------
NF1 | The application must run locally on a standard desktop environment (Windows, macOS, Linux) with Python. | Checked when, after installing dependencies, a user can run `python -m MoneyMate` and use all core features without requiring a network connection.
NF2 | The GUI must be usable by non-technical users through mouse and keyboard. | Checked when typical users can complete flows like “login → add expense → add contact → add transaction → view charts” using only GUI controls (no CLI).
NF3 | The system must provide clear feedback for errors and successful operations. | Checked when operations such as failed login, invalid input or backend errors trigger message boxes with understandable messages, and successful actions provide visible confirmation.
NF4 | The system must keep response times acceptable for typical personal datasets. | Checked when, with realistic amounts of data (e.g., thousands of expenses and hundreds of contacts/transactions), loading screens and refreshing tables complete in a few seconds on a standard student laptop.
NF5 | The data layer must preserve consistency and integrity of stored information. | Checked when automated tests in `test/data_layer` and `test/system` concerning integrity, ownership, listing order and analytics all pass successfully.
NF6 | The system must avoid crashes on invalid operations, handling errors gracefully. | Checked when exceptional situations (e.g., failing DB operations, missing GUI backend) are handled by showing errors or skipping tests, and the application or test suite does not crash irrecoverably.
NF7 | The system must log key events (especially authentication-related) to support auditing and debugging. | Checked when login/logout and other relevant events produce audit/log entries as described in the README, verifiable via tests or inspection of log data.

The IMPLEMENTATION REQUIREMENTS, which are more technical stuff, are about:

ID | Requirement | Acceptance Criteria
---|------------|--------------------
I1 | The system must use an SQLite database to store users, expenses, contacts, categories, transactions and audit data. | Checked when the application creates and uses an SQLite file (including `moneymate_gui.db` for the GUI) where these entities are stored in structured tables.
I2 | The data layer must expose a Python API for all core operations (CRUD and analytics). | Checked when GUI modules interact only with the data layer via functions such as `api_add_expense`, `api_get_expenses`, `api_add_contact`, `api_get_user_balance_breakdown`, and all GUI tests patch these APIs.
I3 | The system must be developed primarily in Python. | Checked when the repository language statistics show Python as the main language and all core modules (`MoneyMate/data_layer`, `MoneyMate/gui`) are implemented in Python.
I4 | The GUI must be implemented using Tkinter and ttk. | Checked when GUI modules import `tkinter` and `ttk`, and the main window is implemented by the `MoneyMateGUI` class inheriting from `tk.Tk`.
I5 | The system must use matplotlib to render charts inside the Tkinter GUI. | Checked when the `ChartsFrame` embeds matplotlib figures using the TkAgg backend and these figures are visible in the running application.
I6 | The project must include automated tests for the data layer, GUI, and system behavior. | Checked when tests under `test/data_layer`, `test/gui`, and `test/system` can be executed with `pytest` and are integrated in the CI workflows defined in `.github/workflows`.
I7 | The codebase must follow the modular structure defined in the template (separated packages and tests). | Checked when the repository contains the documented structure: `MoneyMate/data_layer`, `MoneyMate/gui`, and `test/` with subfolders for `data_layer`, `gui`, and `system`, consistent with the README.
I8 | The GUI must configure its own local SQLite database file at startup. | Checked when `MoneyMate/gui/app.py` computes a path like `MoneyMate/data/moneymate_gui.db`, ensures the directory exists, calls `set_db_path` with that path, and the file is created on first launch.
I9 | GUI tests must avoid side effects on the real GUI database file. | Checked when `test/gui/conftest.py` patches `set_db_path` before importing the GUI, so tests run without creating or modifying the actual `moneymate_gui.db`.
I10 | The project must be configurable and buildable using the provided packaging files. | Checked when `pyproject.toml`, `requirements.txt` and CI configuration allow installation/build and automated tests execution according to the course guidelines.

---


- The requirements must explain **what** (not how) the software being produced should do.
    - You should not focus on the particular problems, but exclusively on what you want the application to do.
- Requirements must be clearly identified, and possibly numbered.
- Requirements are divided into:
    - **Functional**: some functionality the software should provide to the user.
    - **Non-functional**: requirements that do not directly concern behavioral aspects, such as consistency, availability, security, efficiency, etc.
    - **Implementation**: constrain the entire phase of system realization, for instance by requiring the use of a specific programming language and/or a specific software dependency.
        - These constraints should be adequately justified by political / economic / administrative reasons (which must be written down)...
        - ...otherwise, implementation choices should emerge *as a consequence of* design (and therefore described in the design section).
- If there are domain-specific terms, these should be explained in a **glossary**.
- Each requirement must have its own **acceptance criteria**.
    - These will be important for the validation phase. 

> You may consider adding a use-case diagram here (via PlantUML) to better visualize the requirements and their relationships
