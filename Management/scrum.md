## Scrum

Scrum is an agile(Agile is a way to build and improve products step by step, testing and adjusting as you go) team collaboration framework,

#### Core Principles

- Transparency: Everyone knows what’s happening in the project.
- Inspection: Regularly check progress and problems.
- Adaptation: Adjust plans based on feedback or new findings.

#### Scrum Roles

- Product Owner (PO)
- Scrum Master
- Development Team

#### Scrum Artifacts

- Product Backlog
- Sprint Backlog
- Increment

#### Scrum Events (Ceremonies)

- Sprint
  - A fixed time period (usually 1–4 weeks) to complete a set of tasks.
- Sprint Planning
  - Decide which Product Backlog items go into the Sprint Backlog.
- Daily Scrum (Standup)
  - 15-minute daily meeting where team members answer:
  - What did I do yesterday?
  - What will I do today?
  - Any obstacles?
- Sprint Review
  - Demonstrate what was completed during the sprint to stakeholders.
  - Collect feedback.
- Sprint Retrospective
  - Team reflects on what went well, what went wrong, and how to improve in the next sprint.


#### Scrum Workflow

1. Product Owner creates the Product Backlog.
2. Team selects items for a Sprint Backlog.
3. Team works in a Sprint (build → test → deliver).
4. Daily Scrum ensures alignment and removes blockers.
5. Sprint ends → Increment delivered, reviewed, and feedback gathered.
6. Retrospective → team improves process for next sprint.

Simple Example: Imagine building a website:
- Product Backlog: Login page, homepage, contact form, blog.
- Sprint 1: Team builds login and homepage → reviews → adjusts based on feedback.
- Sprint 2: Builds contact form and blog → reviews → improves.
- This repeats until the website is complete.

```mermaid
flowchart TD
    A[Product Backlog] --> B[Sprint Planning]
    B --> C[Sprint Backlog]
    C --> D[Sprint Execution Build Test Deliver]
    D --> E[Daily Scrum Standup]
    D --> F[Increment Delivered]
    F --> G[Sprint Review Demo and Feedback]
    G --> H[Sprint Retrospective Improve Process]
    H --> B


