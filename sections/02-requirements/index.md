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
