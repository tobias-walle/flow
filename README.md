# Flow
Flow is a flexible, skill based workflow.

Skill based workflows are always a tradeoff of giving up control, but in return increase the performance of agents by enforcing best practices.

I couldn't find the right workflow for me, so I build my own. The focus area is:
- **Modularity**: The skills must be easy to adapt into other workflows
- **Readability**: Each skills should be small and easy to read. I wrote most of them by hand and only used LLMs to tweak them. If you cannot understand the main skills in your workflow you are loosing control.
- **Customizability**: The skills are focused and relatively unoppinuated. I encourage you to change them and make them your own instead of blindy accepting my design choices.

A lot of popular skills are extremly verbose and overengineered. This happens naturally if you rely too much on LLMs without guiding it. 
I believe you must push against this trend to keep quality high. This workflow is my attempt to do this.

Enough talking, the main workflow is:
1. `/brainstorm`: Discuss a topic with your agent with the goal to reach an alignment (Heavily inspired by Matt Pococks /grill-me skill, but with a bit more guidance)
2. `/create-design`: Save the results of your discussions in a design doc to use in a later session. The format is very flexible so it can adapt to the content. All main decisions are persistet in enough detail so nothing is lost.
3. `/create-tasks`: Split work across multiple tasks, that can be implemented in multiple sessions.
4. `/implement-tasks`: Implement the tasks created in the previous step. Either in one or more session, or by using subagents with or without worktrees. You could also build a ralph loop around it. You choice!

In addition there is a `/be-visual` skill that is used by `/brainstorming` and `/create-design` to make content easier to understand.

Let's walk through an example:
1. `/brainstorm Let's brainstorm how we can add auth to my app. I already know I want to support OAuth2 and login via google.`
2. *Q&A session around the main design decisions is happening*
3. `Now let's design the main interfaces and file structure` <- You are guiding the discussion into areas you want to align on
4. *Q&A session around architecture and code design*
5. `/create-design` <- Let's save our results. This will create a new file in `.agents/YYYY-MM-DD-oauth-support/design.md`.
6. `/new` or `/clear` <- This is a good handoff point. Let's start a new session to keep the sessions focused. Of course you can decide to stay in the same session if you prefer or the task is small.
7. `/create-tasks for oauth-support` <- This creates one task file for each vertical slice in `.agents/YYYY-MM-DD-oauth-support/tasks/`
8. `/new` or `/clear` <- Another good handoff point.
8. `/implement-tasks Implement all tasks of oauth-support  using subagents. Commit between each task.` <- You decide how you want to implement the tasks.

Basically each phase is optional. Directly implement after `/brainstorm`? You choice. You only want to use `/create-design` but not `/create-tasks` or `/implement-tasks`. Fine for me.

## Installation
The easiest way is to run:
```sh
npx skills add TODO
```

Alternatively you can just use git if you prefer:
```sh
TODO
```


## Inspiration
As I watching the space quite closely, I mostly combined existing ideas. The main inspiration was:
- [Matt Pocock Skills](): I really like the minimal skill design of Matt Pocock. His skills are often quite readable and unoppinuated. I have different oppinions on some of the details of his skills, thats why felt the need to create my own workflow.
- [Research Plan Implement by Dex Horty](): I used a customized version of this workflow in the first half of the year and it really helped me to conceptualize some of the experiences I had. The main lessons around context engineering are still in this workflow. His latestest workflow [CRYSPI]() also influenced the modular design of this workflow.
- [/show-me by Dex Horty](): Our `/be-visual` skill is basically a lightweight version of this skills.
