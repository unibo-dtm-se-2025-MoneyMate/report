---
title: User guide
has_children: false
nav_order: 10
---

# User Guide

This section explains how to use MoneyMate from the final user's perspective.

MoneyMate is a desktop application for personal finance management. It allows users to create an account, log in, organize expenses into categories, manage contacts, register money transfers, and monitor their financial situation through a dashboard with charts.

## 1. Starting the application

Before starting the application, install all required dependencies by running:

```bash
pip install -r requirements.txt
```

To start the application, run:

```bash
python -m MoneyMate
```

When launched, the application automatically creates and uses a local SQLite database file dedicated to the GUI. Therefore, the user does not need to manually create the database before first use.

## 2. First access

When the application starts, the user is presented with the **Login** screen.

From here, the user can:

- log in with an existing account;
- create a new account by clicking **Create an account**.

### Registration

If the user does not already have an account, they can open the registration screen and provide:

- a username;
- a password.

The application performs some basic validation:
- all fields must be filled in;
- the password must contain at least 6 characters.

After successful registration, the user is redirected back to the login screen and can authenticate with the newly created account.

### Login

To log in, the user must enter:

- username;
- password.

If the credentials are valid, the main application interface is shown.

## 3. Main navigation

After login, a sidebar appears on the left side of the window. From there, the user can access the main sections of the application:

- **Dashboard**
- **Expenses**
- **Categories**
- **Transactions**
- **Contacts**
- **Logout**

The dashboard is the first page shown after a successful login.

## 4. Dashboard

The **Dashboard** provides a visual summary of the user's financial data.

It includes charts and aggregated information derived from the user's stored data, such as:

- expenses by category;
- expense trends over time;
- transaction flow summaries;
- balance-related information.

This page is useful to quickly understand spending habits and the overall financial situation.

## 5. Managing categories

The **Categories** page allows the user to organize expenses using custom categories.

From this page, the user can:

- create a new category by entering:
  - a name;
  - an optional description;
- view the list of existing categories;
- remove a selected category.

Categories are personal to the logged-in user. They can later be selected while inserting expenses.

## 6. Managing expenses

The **Expenses** page is used to record and manage personal expenses.

For each expense, the user can provide:

- date;
- amount;
- category;
- description.

From this page, the user can:

- add a new expense;
- edit an existing expense;
- delete a selected expense;
- search/filter expenses;
- clear all expenses.

The interface shows expenses in a table and supports category-based organization. This makes it easier to keep track of spending and analyze it later through the dashboard.

## 7. Managing contacts

The **Contacts** page is intended to manage people related to the user's transactions.

Although the detailed interaction logic was not fully visible in the extracted files, based on the application structure and navigation it is clear that this section is used to maintain the list of contacts that can be associated with money transfers.

From the user's perspective, this section is used to keep the set of relevant people organized before registering transactions.

## 8. Managing transactions

The **Transactions** page allows the user to record money exchanges involving other users or contacts.

The page supports viewing transactions in different ways, including:

- all transactions;
- sent transactions;
- received transactions.

For each transaction, the interface displays information such as:

- date;
- type;
- direction (sent/received);
- counterparty;
- description;
- amount.

The user can also:

- search transactions;
- remove the selected transaction.

This section helps the user keep track not only of expenses, but also of transfers of money between parties.

## 9. Logout

At any time, the user can press **Logout** from the sidebar.

This operation:

- ends the current session;
- removes the authenticated user context;
- returns the interface to the login screen.

## 10. Typical usage scenario

A typical user workflow is the following:

1. Start MoneyMate.
2. Create an account if this is the first access.
3. Log in.
4. Add a set of categories such as *Food*, *Transport*, *Bills*, or *Entertainment*.
5. Add contacts if needed.
6. Register expenses day by day.
7. Insert transactions to track money sent or received.
8. Periodically open the dashboard to inspect charts and summaries.
9. Log out when finished.
