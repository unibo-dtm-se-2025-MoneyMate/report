---
title: Validation
has_children: false
nav_order: 6
---

# Validation

## Testing approach

We adopted **test-first / TDD-inspired** development for the most critical parts of the system:

- **Data layer** (API facade and managers)
- **Validation logic**
- **User management and authentication**
- **Core GUI flows** (login, registration, CRUD screens)

We used **`pytest`** because:

- fixtures make it easy to manage temporary SQLite DBs and GUI apps;
- it integrates directly with coverage (`pytest-cov`) and CI.

Over the whole `MoneyMate` package we reach **76%** coverage. We decided not to push coverage further because the unchecked lines represent mostly because:

- Testing these specific parts would require simulating fake errors or unrealistic scenarios (like a corrupted hard drive). We preferred to focus our testing efforts on the **real features** that users actually use every day, ensuring the main requirements are fully met.

## Testing (automated)

> In the following subsections, when useful we reference functional requirements F1–F14 and non‑functional/implementation requirements NF1–NF7, I1–I10.


### Unit testing

We developed unit tests focused on the **GUI components** (located in `MoneyMate/gui`) and the pure **data validation logic** (`validation.py`).

  **Rationale:** We verified that the interface handles user input correctly (e.g., preventing empty fields or negative amounts) and triggers the correct API calls without actually writing to a real database. We used **mocking** (via `unittest.mock.MagicMock` in `conftest.py`) to isolate the interface, ensuring the UI logic is robust and tests run quickly.

- **Success rate and test coverage**

  * **Success Rate:** 100% (All tests passed).
  * **Test Coverage:** **77%** (Focusing on `MoneyMate.gui` and `validation.py`).

### Integration testing

We tested the integration between the **API Facade** (`MoneyMate.data_layer.api`) and the **SQLite Database Manager** (`MoneyMate.data_layer.database`).

  **Rationale:** The plan was to verify that high-level API calls (like `api_add_expense`) correctly orchestrate the internal logic, respect database constraints (like foreign keys), and persist data to a real file on the disk. We also tested the integration between the **Managers** and the **Logging system** to ensure audit trails are created for operations like adding expenses or contacts.

- **Success rate and test coverage**

  * **Success Rate:** 100% (All tests passed).
  * **Test Coverage:** **75%** (Focusing on the `MoneyMate.data_layer` package).

### System testing

We developed an End-to-End test scenario in `test_system_end_to_end.py` that simulates a full user lifecycle without the GUI.

  * **Test Rationale/Plan:** This test follows the "Giulia Rossi" persona user story. It registers a user, adds categories, expenses, and contacts, creates complex transactions, and finally asserts that the calculated Net Balance is mathematically correct.
  * **Matching Requirements:** This validates requirements **F1-F11** (Registration to Balance Calculation) and **NF5** (Data Consistency).

- **Success rate and test coverage**

  * **Success Rate:** 100% (All system flows passed).
  * **Test Coverage:** **23%** (This is expected because this test runs "headless" against the API and does not execute the GUI code, which constitutes a large part of the codebase).

## Acceptance tests (manual)

We complemented automated tests with **manual acceptance tests** designed to match the acceptance criteria in the requirements.

**Rationale/plan.**

We executed the application with:

```bash
python -m MoneyMate
```

and followed manually defined scenarios:

1. **User onboarding and first usage** (F1–F4, F13, NF1–NF3)
   - Register a new user and log in via the GUI.
   - Add a first expense (amount, date, category, description).
   - Check that:
     - the expense appears in the Expenses table;
     - invalid or incomplete forms (e.g. missing amount, invalid date, empty title) produce clear error messages and do not crash the app.

2. **Managing contacts, transactions and balances** (F7–F11, NF2–NF6)
   - Add contacts; add transactions between the logged‑in user and these contacts.
   - Check that:
     - filters (All/Sent/Received, search by text) work;
     - balances and per‑contact breakdowns shown in the GUI match the operations.

3. **Multi‑user isolation** (F14, NF5, NF6)
   - Create at least two users.
   - As User A, create data (expenses, contacts, transactions).
   - As User B, verify that User A’s data is not visible and cannot be modified.

4. **Robustness and error handling** (NF3–NF7)
   - Try invalid logins, invalid forms and operations without selection (e.g. delete with no row selected).
   - Confirm that:
     - error messages are shown;
     - the application never crashes and remains usable.

Each scenario is documented as a **sequence of steps + expected results**, so another person can repeat the tests and verify pass/fail outcomes. All planned acceptance scenarios **passed** on the tested environments.
