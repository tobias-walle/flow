---
name: brainstorm
description: Explore a topic with the user through questions and answers. Use when the user asks to "brainstorm". A brainstorming session must be intentional, so don't use it for synonyms or unless explicitly requested by a user or skill.
---

Brainstorm a solution with the user.

The goal is to reach a common understanding and alignment.

## Workflow

1. If the user hasn't provided a topic yet, ask which topic they want to discuss.
2. Gather the relevant context. Tell the user what you understand.
3. Then start asking questions to clarify information you couldn't find during your exploration. Do relevant research between questions.
4. If the user has feedback or asks for clarification, fully focus on the referenced question(s). Do not ask any new questions until the answer(s) are resolved. Repeat unanswered questions that might be overlooked.
5. Stop once a common understanding is reached. Summarize the agreed direction before stopping.

## Question Formatting

- Give each question a number (e.g. `Question 1: <question>`)
- List options in a bullet point list with A, B, C, etc. labels
- Recommend one option
- Present relevant context and the different alternatives
- Present each question and the relevant context, in a visual and concise format for fast understanding. Use ASD-STE100 Simplified Technical English and visualizations (use the be-visual skill if available).

## Q&A Behavior

- As long as the general direction is unclear, ask one question at a time
- After the first few questions, once the solution falls into place and you expect the user to accept the recommended answers, ask multiple questions at once
- Batches should be grouped by question dependencies. Do not ask questions that depend on each other in the same batch.

## Scope

- Brainstorming can cover any topic. It is always focused on creating an artifact in the end, for example, a ticket, design doc, or direct code update.
- Always make sure you understand the intent of the brainstorming.
- In technical discussions focus on architecture decisions like concepts, interfaces and codebase structure. Reference concrete symbols and file structures from the gathered context.
