---
name: changes-folder
description: Manage artifacts in .agents/changes. Use whenever work involves the .agents/changes folder or the user explicitly mentions the changes-folder skill.
---

Keep all artifacts for one change in `.agents/changes/YYYY-MM-DD-<slug>/`.

If the change references an issue, use `.agents/changes/YYYY-MM-DD-<ref>-<slug>/`, for example `2026-12-31-42-some-change` for GitHub issue `#42` or `2026-12-31-PRJ-42-some-change` for Jira issue `PRJ-42`.

Use the date the change folder is created and a short kebab-case slug.

Follow these conventions:

- `design.md` contains the change's design and key decisions.
- `tasks/` contains task files for implementing the change.
- Add any other files and folders useful for the change, such as `prototype/`. Choose their structure based on the work.
