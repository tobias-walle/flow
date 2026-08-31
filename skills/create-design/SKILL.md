---
name: create-design
description: Create a design document from a brainstorming session or another discussion. Use when important decisions must persist in a visual document for humans.
---

Create a concise design document at `.agents/changes/YYYY-MM-DD-<slug>/design.md`. Use the current date in the directory name.

Start the document with lightweight YAML frontmatter:

```yaml
---
datetime: <Current ISO 8601 date and time>
author: <Author name>
tags: [<tag>, <tag>]
---
```

Cover all important decisions from the source discussion. Include the context needed to understand each decision.

Clearly reference related documents and websites. Use paths or links that the reader can follow.

Use a free structure that fits the topic. Use concise language, a clear structure and visualizations to make the document easy to understand. Use the `be-visual` skill if available.

Use this fixed section for each key decision:

```md
## Key Decisions

### <Decision title>

- **Decision:** <Selected option>
- **Reason:** <Why this option was selected>
- **Trade-offs:** <Accepted disadvantages or rejected options>
```

Do not force other content into a fixed structure.
