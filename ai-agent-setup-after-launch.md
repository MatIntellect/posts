# AI agent setup after launch: onboarding, permissions and memory worksheet

Type: setup note and fill-in worksheet. Reader: a developer or operations lead who has just deployed an AI agent for a business owner or a small team. Goal: move the agent from generic answers to the owner's actual work through three steps with clear checks: onboarding, tools and permissions, memory rules. Limits: this note describes a process; templates are teaching material, not a tested configuration for any specific agent framework

![AI-generated illustration of setting up an AI agent after launch](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-ai-agent-setup-after-launch-1794192129.jpg)

## Reference

The steps come from my own agents. My personal agent Jes has been running for 134 days, runs 10 scheduled jobs and hands tasks to 7 other bots; since July she has passed on 165 tasks. Four kinds of actions there always wait for an explicit yes: deleting data, spending money, messaging clients and publishing. A first agent for one clear task took one to two weeks in my projects, mostly spent on rules, memory and testing on real data

## Step 1: onboarding

The agent interviews the owner, one question at a time, with answer options and room for free text. Prompt to start with:

> Ask me about my work. One question at a time. Offer three or four answer options for each and let me answer in my own words if none fit

Topics the interview must cover:

| Topic | Why it matters |
|---|---|
| What the business does, who the clients are | Context for every later answer |
| First tasks to hand over | Defines which tools are needed in step 2 |
| Communication preferences | Length, language, quiet hours |
| Topics that matter and topics to avoid | Prevents tone mistakes |
| Stop points | Where the agent must ask before promising or sending anything |

Exit check: the agent shows what it saved, the owner reads it and corrects any misunderstanding before the agent relies on it

## Step 2: tools and permissions

Connect one tool at a time, each for a specific task, and try it on real work before adding the next. External services can be connected through MCP, the standard protocol for linking an AI application to other programs and data

![Two colleagues talking](https://images.pexels.com/photos/5951759/pexels-photo-5951759.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

Permission matrix (fill in per tool):

| Tool | Read | Create | Change | Delete or send | Needs approval for |
|---|---|---|---|---|---|
| Mail | | | | | |
| Calendar | | | | | |
| Task list | | | | | |
| Other | | | | | |

Rule of thumb: anything that cannot be undone needs approval. Access to a tool is not permission to act with it

## Step 3: memory rules

| Rule | Example setting |
|---|---|
| Fact length | One or two lines |
| Details | Stored in a separate file, the note links to it |
| Old material | Archived, not deleted |
| Cleanup schedule | Daily or weekly |
| Before cleanup | Confirm nothing important is lost and details remain findable |
| After a correction | The agent writes a new rule so the mistake does not repeat |

Conversation alone does not guarantee the agent saves new information. Test it: tell the agent a new preference, start a fresh conversation the next day and check whether it applies

![External drive next to a laptop](https://images.pexels.com/photos/6930265/pexels-photo-6930265.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Instruction files

| Agent | Main instruction file |
|---|---|
| Codex | AGENTS.md |
| Claude Code | CLAUDE.md |
| Other systems | Ask the agent which files and settings it reads |

Some setups also keep a separate file for tone and character. Review all of them every few weeks: remove rules that now get in the way, merge duplicates, rewrite any rule that needed the same correction twice

## Failure modes

| Symptom | Likely cause | Response |
|---|---|---|
| Generic answers weeks after launch | Onboarding skipped or never checked | Repeat step 1, read the saved notes |
| Same correction repeats | Rule written unclearly or not saved | Rewrite the rule, test in a fresh conversation |
| Error source unclear | Several tools connected at once | Disconnect back to one tool, add again one by one |
| Agent applies an old, irrelevant note | No memory cleanup | Add a cleanup schedule and archive rule |
| Agent acts where it should ask | Stop points not defined | Add them to the permission matrix and instructions |

## Worksheet

Fill in during the first week. It is a template, not a tested configuration

- Onboarding conversation done: date
- Saved notes reviewed by owner: yes / no
- First task:
- First tool connected and tried on a real task:
- Actions that always need approval:
- Memory rules written: fact length, link rule, archive rule, schedule
- Instruction files located and reviewed:
- Next review date:

More on how agents are scoped and supported is on the [AI agent development page](https://matintellect.com/en/services/ai-agents)
