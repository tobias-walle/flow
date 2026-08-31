---
name: implement-tasks
description: Implement the given .agents/changes/<change>/tasks. Only use if a concrete .agents/changes path or task is specified. Do not use for generic implementation tasks.
---

Implement a change or focused task. Follow the `changes-folder` skill for folder conventions.

1. Determine the scope:
   * If the user gave you a full change, the scope is all tasks of this change
   * If the user referenced a single task, the scope is only this task

2. Decide how to work:
   * Default: **In Context Implementation**
   * Explicit User Request: **Sequential Subagents**
   * Explicit User Request: **Parallel Subagents**

   The user can always override that recommendation.

## Implementing a task

1. Understand the task and its scope
2. Read the referenced documents and key files
3. Mark the next work items with `[-]`
4. Focus on speed. Do all the relevant edits in as few turns as possible, including the tests. Do not use TDD if not explicitly requested.
5. Mark completed work items with `[x]`
6. Run relevant checks and tests and fix issues directly.
7. Mark verification items already covered by the tests with `[x]`.
8. For remaining items:
   * If you can test them yourself with ad hoc scripts and experiments, do that. Mark the verification with `[-]`.
   * Fix mistakes directly. Use TDD for hard-to-detect logic bugs.
   * Mark with `[x]` once passed.
   * Add a note to each passed item that states how you verified it. For example: `**Note:** Verified via <reference to automated test>`.
   * Mark remaining items that you cannot test with `[ ] (manual testing required)`.
9. If the implementation requires a meaningful deviation from the design, do not silently change it. Adapt implementation details to the current codebase where necessary, but make design deviations and their reasons explicit.
10. Double-check the changes for completeness and documented best practices. Use a subagent only when the user requested subagents. Integrate relevant feedback directly.
11. Present a visual, structured, concise summary to the user. Include what was done, what problems occurred, how you resolved them, and what manual tests remain.

## Sequential Subagents

Use this mode only when the user explicitly requests subagents.

1. Read the change and task documents. Do not read source files unless they are relevant to the orchestration task.
2. Select the next task whose dependencies are complete.
3. Start one subagent for the task. Start the prompt with: `You are a subagent for task <filepath> of change <changepath>. Only focus on this task and respond with a clear summary of your work for the main agent`. Include the exact steps from `Implementing a task` and other relevant file references.
4. Start only one subagent at a time.
5. After all tasks are complete, use a subagent to check that the change is fully integrated.
6. Present a visual, structured, concise summary to the user. Include deviations from the design and their reasons.

## Parallel Subagents

Use this mode only when the user explicitly requests parallel subagents.

Follow `Sequential Subagents`, but use worktrees to isolate independent tasks.

Process only tasks whose dependencies are complete.

Merge completed worktrees into the current branch one at a time. Resolve integration issues directly.

If not otherwise specified in the project setup, store worktrees in `.agents/worktrees` and make sure it is in `.gitignore`
