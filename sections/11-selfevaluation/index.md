---
title: Self-evaluation
has_children: false
nav_order: 12
---


## Andrea Giovanardi

### Self-evaluation Narrative
During the MoneyMate project, my work started as a backend-focused contribution: designing the SQLite data layer, implementing CRUD operations for expenses/contacts/transactions, and adding validation to ensure consistent and reliable data handling. In parallel, I introduced a standardized API response format (`{success, error, data}`), which made the backend easier to use and test.

As the project grew, my role evolved beyond feature implementation into a more technical lead / guide position. I helped keep the architecture coherent by introducing and maintaining a centralized orchestration layer (DatabaseManager), so the team could build on stable interfaces instead of duplicating database logic. In later stages, I expanded the backend with user authentication and user-scoped data, improved system robustness through logging and safer database connection handling, strengthened CI/testing, and contributed to documentation to support team-wide understanding.

Overall, I moved from “building the backend foundation” to enabling smoother integration and maintaining technical consistency across the project.

### Strengths of my contribution
- **Reliability and consistency:** steady delivery while preserving backward compatibility and stable behavior.
- **Clean API/interface design:** predictable responses and modular boundaries that reduced integration friction.
- **Team support and technical guidance:** architectural decisions that kept the codebase aligned.
- **Quality focus:** strong effort on tests, CI stability, and maintainability improvements.

### Weaknesses / Points to improve
- **Documentation depth:** key architectural decisions could have been documented earlier and more systematically.
- **Need for consolidation:** fast iteration introduced areas that would benefit from a dedicated refactoring pass.
- **More explicit leadership process:** I could improve by formalizing coordination (design notes, clearer ownership, more structured reviews).

### Role in the group
I acted as a technical reference point and informal lead for the backend/data layer: first by building the core foundation, and later by guiding architectural choices, ensuring consistency, and supporting teammates through stable interfaces, tests, and tooling—helping the project converge into a maintainable final product.




## Matteo Fabbri

## Self-evaluation

### Self-evaluation Narrative
At the beginning of this project, my contribution was mostly “backend-oriented”, but in a very practical student sense: I focused on making sure that the application had a **working and stable data layer**, so that the rest of the project (GUI, scripts, tests) could store and retrieve data without constantly breaking.

Since this is not my main field of expertise, my approach was to learn by doing: I tried to understand what the project needed in order to behave like a “Money Split” app (users, contacts, expenses, and transactions), and then I worked on the parts that make those features possible in a database.

Over time, I realized that simply adding code was not enough: the project also needed to be **organized and consistent**, otherwise every new feature would become harder to integrate. For this reason, my role slowly moved from “just implementing a backend feature” to being someone who helped the team by **keeping the structure clear** and by giving a reference point for how to interact with the database.

In practice, this meant:
- Helping define a **simple, single API layer** (a set of `api_*` functions) so that other parts of the project could call the same operations in the same way.
- Supporting the idea of a **central manager** (`DatabaseManager`) that connects all the smaller modules (users, contacts, expenses, categories, transactions), instead of having every file work independently.
- Keeping database-related logic centralized in one place (`database.py`), so the database schema (tables and relationships) stayed coherent.
- Contributing to the **Design documentation and UML diagrams**, to make the structure easier to explain in the report and easier to understand for teammates.

Overall, I see my contribution as a transition: I started by working on backend foundations, but I ended up also helping as a “technical guide” by trying to keep the project consistent and easier to maintain, even if I’m not an expert in software architecture.

---

### Strengths of my contribution
- **Reliability and stability:** I worked on making the database layer behave in a predictable way, so other team members could build features without constantly changing how data is stored.
- **Keeping things consistent:** I tried to keep a consistent style (same response format, same validation logic idea), which helped reduce confusion when integrating different modules.
- **Learning attitude:** Even though backend/database design is not my strongest subject, I made an effort to understand it and improve the project step by step.
- **Support to the team:** By working on shared parts (API façade / central manager / schema), I helped the team work faster because there was a clearer “common ground”.

---

### Weaknesses / Points to improve
- **Limited confidence with advanced backend topics:** Since this is not my main subject, I sometimes had to rely on trial-and-error and incremental improvements instead of designing everything perfectly from the start.
- **More documentation could be useful:** The project has Design diagrams, but a clearer explanation of “why we chose this structure” and more examples of flows could make it even easier to understand.
- **Refactoring could be improved:** Some parts of the code could be simplified further (for example, reducing repeated patterns across modules), but we focused more on getting a working solution within the project timeframe.

---

### Role in the group
I would describe my role as someone who started as a **backend contributor** and ended up also acting as a **technical support / reference person** for the data layer.

I did not lead the project in a formal way, but I often contributed by:
- keeping the “database side” stable and consistent,
- helping define how other modules should call the backend (through a simple API),
- supporting the team by making the architecture easier to explain (documentation + diagrams).

In short, I contributed to the project mainly by strengthening the backend foundation and by helping the group keep a coherent structure while features were being developed.


## Cristian Romeo

_TODO: Add Cristian Romeo's self-evaluation section._
