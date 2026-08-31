# Flow
Flow is a flexible, skill-based workflow.

Skill-based workflows always involve a trade-off: you give up control but gain better agent performance by enforcing best practices.

I couldn't find the right workflow for me, so I built my own. The focus areas are:
- **Modularity**: The skills must be easy to adapt into other workflows.
- **Readability**: Each skill should be small and easy to read. I wrote most of them by hand and only used LLMs to tweak them. If you cannot understand the main skills in your workflow, you are losing control.
- **Customizability**: The skills are focused and relatively unopinionated. I encourage you to change them and make them your own instead of blindly accepting my design choices.

A lot of popular skills are extremely verbose and overengineered. This happens naturally if you rely too much on LLMs without guiding them.
I believe you must push against this trend to keep quality high. This workflow is my attempt to do this.

Enough talking, the main workflow is:
1. `/brainstorm`: Discuss a topic with your agent with the goal of reaching alignment (heavily inspired by Matt Pocock's [`/grill-me`](https://github.com/mattpocock/skills/blob/main/skills/productivity/grill-me/SKILL.md) skill, but with a bit more guidance).
2. `/create-design`: Save the results of your discussions in a design doc to use in a later session. The format is very flexible, so it can adapt to the content. All main decisions are persisted in enough detail so nothing is lost.
3. `/create-tasks`: Split work across multiple tasks that can be implemented in multiple sessions.
4. `/implement-tasks`: Implement the tasks created in the previous step, either in one or more sessions or by using subagents with or without worktrees. You could also build a Ralph loop around it. Your choice!

Two helper skills support this workflow. `/be-visual` adds diagrams. `/changes-folder` keeps each change's context together across phases:

```text
.agents/changes/
└── 2026-12-31-42-oauth-support/  # Issue reference is optional
    ├── design.md                  # Decisions and context
    ├── tasks/                     # Implementation tasks
    └── prototype/                 # Optional supporting artifacts
```

Other task-specific files and folders can be added freely.

Let's walk through an example:
1. `/brainstorm Let's brainstorm how we can add auth to my app. I already know I want to support OAuth2 and login via Google.`
2. *Q&A session around the main design decisions is happening*
3. `Now let's design the main interfaces and file structure` <- You are guiding the discussion into areas you want to align on
4. *Q&A session around architecture and code design*
5. `/create-design` <- Let's save our results. This will create a new file in `.agents/changes/YYYY-MM-DD-oauth-support/design.md`.
6. `/new` or `/clear` <- This is a good handoff point. Let's start a new session to keep the sessions focused. Of course you can decide to stay in the same session if you prefer or the task is small.
7. `/create-tasks for oauth-support` <- This creates one task file for each vertical slice in `.agents/changes/YYYY-MM-DD-oauth-support/tasks/`.
8. `/new` or `/clear` <- Another good handoff point.
9. `/implement-tasks Implement all tasks of oauth-support using subagents. Commit between each task.` <- You decide how you want to implement the tasks.

Basically, each phase is optional. Directly implement after `/brainstorm`? Your choice. You only want to use `/create-design` but not `/create-tasks` or `/implement-tasks`? Fine with me.

## Installation
The easiest way is to run:
```sh
npx skills add tobias-walle/flow
```

Alternatively you can just use git if you prefer:
```sh
tmp_dir="$(mktemp -d)" && git clone --depth 1 --filter=blob:none --sparse https://github.com/tobias-walle/flow.git "$tmp_dir" && git -C "$tmp_dir" sparse-checkout set skills && mkdir -p .agents/skills && cp -R "$tmp_dir"/skills/. .agents/skills/ && rm -rf "$tmp_dir"
```


## Inspiration
As I follow the space quite closely, I have mostly combined existing ideas. The main inspirations were:
- [Matt Pocock Skills](https://github.com/mattpocock/skills): I really like Matt Pocock's minimal skill design. His skills are often quite readable and unopinionated. I have different opinions on some of the details of his skills, which is why I felt the need to create my own workflow.
- [Research, Plan, Implement from "No Vibes Allowed" by Dexter Horthy](https://www.youtube.com/watch?v=rmvDxxNubIg): I used a customized version of this workflow in the first half of the year, and it really helped me conceptualize some of the experiences I had. The main lessons around context engineering are still in this workflow. His latest workflow, [CRISPY](https://www.youtube.com/watch?v=YwZR6tc7qYg), also influenced the modular design of this workflow.
- [`/show-me` by Dexter Horthy](https://github.com/humanlayer/skills/blob/main/plugins/show-me/skills/show-me/SKILL.md): Our `/be-visual` skill is basically a lightweight version of this skill.
- [OpenSpec](https://openspec.dev/): Putting all relevant files into a single change folder was heavily inspired by OpenSpec.
