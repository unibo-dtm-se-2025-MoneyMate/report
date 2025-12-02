---
title: Deployment
has_children: false
nav_order: 8
---

# Deployment

This section explains what operations are needed to make the software work on the users' machine(s)

## User installation

- Does the user need to install something on their machine(s) to run your software?  
  Yes. To run MoneyMate, a user needs:
  - A Windows operating system.
  - A compatible Python interpreter (as defined in the `.python-version` file in the project).
  - The MoneyMate Python package and its dependencies.

- Users can either:
  - Install the **released MoneyMate package** from PyPI, or
  - Install MoneyMate **from the GitHub repository source**.

- How to install it? 

  **Option 1 – Install from PyPI (recommended for end users)**

  1. Ensure `python` and `pip` are available:

     ```bash
     python --version
     pip --version
     ```

  2. Install MoneyMate from PyPI:

     ```bash
     pip install MoneyMate
     ```

  3. Run the application:

     ```bash
     python -m MoneyMate
     ```

  **Option 2 – Install from source (for developers)**

  1. Clone the repository:

     ```bash
     git clone https://github.com/unibo-dtm-se-2025-MoneyMate/artifact.git
     cd artifact
     ```

  2. (Optional but recommended) create and activate a virtual environment:

     ```bash
     python -m venv .venv
     .venv\Scripts\activate
     ```

  3. Install dependencies for development:

     ```bash
     pip install -r requirements-dev.txt
     ```

  4. Run the application:

     ```bash
     python -m MoneyMate
     ```

- How to configure it?

  Minimal configuration is required for basic usage:

  - **Database location**

    On first run, the GUI will configure its own local SQLite database file. The default GUI database path is:

    ```text
    MoneyMate/data/moneymate_gui.db
    ```

    The path is set programmatically through the `set_db_path` API in the data layer. No manual creation of the file is required; it is created automatically.
    
    - **Optional: populate the database with demo data**

    Developers or testers who want a pre-populated database can use the provided script:

    ```bash
    python populate_db.py
    ```

    This script:

    - Removes the existing `MoneyMate/data/moneymate_gui.db` file if present.
    - Recreates the database using the data layer API.
    - Adds sample users, categories, expenses, contacts, and transactions.
