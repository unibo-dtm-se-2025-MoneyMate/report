---
title: Future work
has_children: false
nav_order: 13
---

# Known issues and future work

This section describes, in simple terms, what is missing, what does not work as expected, and what could be improved in the future.

---

## 1. Things that do not work or are not ideal

- **Admin user / password behaviour**
  - The idea is to have a special “admin” user with a defined password.
  - In practice, the admin credentials do not always behave as expected (even when inserted correctly).
  - This makes real admin usage unreliable.

- **Only local usage (no real server)**
  - At the moment, MoneyMate works only locally with a local SQLite file.
  - There is no proper “server” component that multiple users or applications can connect to over the network.

- **SQLite only**
  - The data is stored in a local SQLite database.
  - SQLite is fine for a small/local setup, but for larger or more serious usage, a “normal” SQL database (e.g. PostgreSQL, MySQL) would be more robust and scalable.

- **No password reset / email link**
  - There is no feature to reset a forgotten password.
  - There is no support for linking an email to an account and sending a reset link or confirmation email.

---

## 2. Current limitations

- **Single‑process design**
  - The system is mainly designed to run in one process on one machine.
  - It is not designed or tested for many processes or many machines accessing the same database at the same time.

---

## 3. Possible future improvements

Based on the points above, some natural directions for future work are:

- **Fix and improve admin handling**
  - Make sure admin username and password always work as designed.
  - Add clear tests and documentation for the admin logic.

- **Introduce a real server layer**
  - Add a small HTTP/REST API so other clients (GUI, web app, other programs) can connect to MoneyMate over the network.
  - This would turn the local data layer into a real shared service.

- **Support for a full SQL server**
  - Allow the option to use a “classic” SQL database (e.g. PostgreSQL) instead of only SQLite.
  - This would improve performance and reliability in scenarios with more data and more users.

- **Account and password management**
  - Add password reset functionality (with proper checks).
  - Add optional email association to each account, so that:
    - a reset request can be sent by email,
    - it is clearer which real user owns each account.
