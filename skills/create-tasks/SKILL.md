---
name: create-tasks
description: Create a list of tasks from a design doc or change description. Only use if user explicitly wants to "create tasks" or mentions the skill directly.
---

Split a planned change into vertical slices (tasks) that can be implemented independently.

1. Understand the intent by either reading the attached documents or analyzing the user request.
2. Gather all relevant context by reading relevant files and rules in the codebase. Do not use subagents unless otherwise specified. Fully understand the relevant context.
3. Plan what changes are necessary to fully integrate the given change request, honoring all the described restrictions and rules of the codebase.
4. If important details are not specified yet, such as file structure and core interfaces, propose a design and present it to the user. Be visual. Once they confirm, save it in a referenced existing design document or create a new one using `/create-design`.
5. Split the work into vertical slices (tasks).
   - Each task is an independently verifiable, vertical slice.
   - Tasks may depend on other tasks and might be parallelizable.
   - Dependencies represent actual blockers, not a preferred execution order.
   - Tasks are split by scope, not time. There might be only one task required for a given change.
6. Give a concise overview of the task split by listing each task number and title. Ask the user for confirmation of this split if it involves meaningful trade-offs.
7. If the user gives feedback, ask follow-up questions if necessary, integrate it, present the results, and repeat until the user confirms.
8. Once the user confirms, store the tasks in the given format:

File Location: `.agents/changes/YYYY-MM-DD-<slug>/tasks/`

Each task is a file `<id>-<slug>.md`, e.g. `01-add-login-page.md`.

Each task file follows the following format:
```markdown
---
id: <id>
dependencies:
- <task-id>
---

# Task <id>: <title>

<One or two sentences describing the independently useful outcome of this task.>

## References

* `design.md#session-store`
* `design.md#resume-semantics`
* <Reference relevant documents and files here>

## Work

* [ ] Update `ResumeCommand` in `src/cli/` to support resuming persisted sessions through `SessionStore`
* [ ] Integrate with `SessionStore.resume` in `src/session/` while preserving the semantics defined in the design
* [ ] Add or update automated coverage around the CLI resume flow
* [ ] <Describe a meaningful implementation change. Prefer concrete symbols and paths, but leave internal implementation details to the executor.>

## Verification

* [ ] An existing session can be resumed by ID
* [ ] Its persisted state is restored
* [ ] An unknown ID produces the error defined in the design
* [ ] Existing new-session behavior remains unchanged
* [ ] Relevant repository tests and checks pass
* [ ] <Describe an observable, falsifiable outcome that proves the task works. Prefer behavior over implementation details.>
```
