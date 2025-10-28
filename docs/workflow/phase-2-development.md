# Phase 2: Development 🧩

Tools: Zed + GLM + Context7 MCP + DevTools MCP

## Workflow
Open the project in Zed

Load the feature spec into context

One feature at a time:
a. Read the tasks
b. Agent implements task by task
c. After each task: manual review
d. After the feature: comprehensive review

Commit after each completed feature

## Rules
- One feature at a time—don’t mix
- Modular code—easier context management
- Commit frequently—after each working feature
- Review manually—always check before merge

## Example session
Session 1: User Authentication Feature

Task 1: Setup auth schema [COMMIT]

Task 2: Login endpoint [COMMIT]

Task 3: Register endpoint [COMMIT]

Task 4: JWT middleware [COMMIT]

Feature Review → merge to main

Session 2: Dashboard UI

Next: [Phase 3 → Testing & Debugging](./phase-3-testing-debugging.md)

Back: [Workflow overview](./README.md)
