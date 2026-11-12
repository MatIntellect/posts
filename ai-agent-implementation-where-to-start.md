# AI agent implementation: rollout stages and acceptance notes

Type: implementation note and planning worksheet. Reader: a developer, operations lead or technical founder about to introduce the first AI agent into a small business. Goal: a staged rollout where each stage has an entry condition, an exit condition and a clear owner. Limits: this is a process note, not a library; the worksheet and diary template are teaching material, not a tested configuration

![AI-generated illustration of starting with one agent task](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-ai-agent-implementation-where-to-start-1793407087.jpg)

## Why stages

A first agent usually fails for organisational reasons, not technical ones. The task was too wide, nobody defined a correct result, or the team never learned to check the output. Splitting the rollout into stages forces each of those questions to be answered before the agent touches anything that matters

The reference for these notes is my own work with agents. My personal agent has been running for 134 days, runs 10 scheduled jobs and hands tasks to 7 other bots; four kinds of actions there always wait for an explicit yes: deleting data, spending money, messaging clients and publishing. A first agent for one clear task took one to two weeks in my projects, including memory, approval rules, a schedule and testing on real data

## Rollout stages

| Stage | Entry condition | What the agent does | Exit condition | Owner |
|---|---|---|---|---|
| 0. Diary | Owner agrees to record one normal workday | Nothing | Written list of actions with input and output for each | Owner |
| 1. Pick | Diary exists | Nothing | One task chosen: repetitive, clear input, checkable output, low cost of error | Owner and implementer |
| 2. Shadow | Task defined in writing | Runs on real inputs, output goes only to a reviewer | Reviewer agrees with the output on a set of real cases, including hard ones | Reviewer |
| 3. Drafts | Shadow passed | Prepares drafts in the real tool; a human sends or applies them | A week with no correction of the same kind twice | Reviewer |
| 4. Unattended | Drafts stage stable | Runs the safe part of the task alone; risky actions still gated | Decided by the owner, action by action | Owner |

Stage 4 is not the goal for every task. Some tasks stay at drafts forever, and that is a valid outcome

## Task definition

Each task gets a short written definition before stage 2. Fields:

- Input: where the data comes from (mailbox, chat, spreadsheet, calendar)
- Output: format and destination
- Correct result: how a human decides the output is right
- Forbidden actions: what the agent must not do, for example reply to clients
- Ambiguity rule: when the input is unclear, flag it and ask; never guess
- Escalation: who receives the flag and how

![Writing down a workday](https://images.pexels.com/photos/3746963/pexels-photo-3746963.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Diary template (teaching example)

One line per action, in the order it happened. The example rows are invented for illustration

| Time | Action | Input | Output | Minutes | Could be checked by someone else? |
|---|---|---|---|---|---|
| 09:10 | Read new emails | Mailbox | List of requests in my head | 15 | Yes, if written down |
| 09:25 | Update client table | Emails | Two new rows | 10 | Yes |
| 11:00 | Reply to a pricing question | Email, price list | Reply | 5 | Yes |
| 14:30 | Decide on a discount | Client history | Decision | 2 | No, owner judgement |

Rows with a clear input, a written output and "yes" in the last column are candidates for stage 1. Rows that are judgement calls stay with people

## Failure modes

| Failure | Where it shows up | Response |
|---|---|---|
| Task too wide | Shadow never passes; every case is different | Split it; go back to stage 1 |
| No definition of correct | Reviewers disagree with each other | Write the rule before testing the agent |
| Agent guesses on missing data | Confident output referring to things not in the input | Add the ambiguity rule and a test case for it |
| Same correction repeats | Drafts stage | The written rule is unclear; rewrite it so the agent reads it next time |
| Team ignores drafts | Drafts pile up unchecked | Shrink the task or move the output into a tool the team already opens |
| Silent stop | Nothing arrives and nobody notices | A service supervisor plus a daily line that the job ran |

## Acceptance notes

- Keep a small labelled set: ten real cases with two or three hard ones beat a hundred easy ones
- Every correction becomes a new labelled case and, where it applies, a written rule the agent reads next time
- Measure agreement with a human, not abstract accuracy; the human is the definition of correct for this task

![Reviewing results at a desk](https://images.pexels.com/photos/9052597/pexels-photo-9052597.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Planning worksheet

Fill in before stage 2. It is a template, not a tested configuration

- First task (one sentence):
- Input source and access method:
- Output format and destination:
- Who decides the output is correct:
- Ten real cases collected: yes / no
- Forbidden actions:
- Actions that always need approval:
- Who gets flags when input is unclear:
- How we learn that the agent stopped:
- Date to review whether to move to the next stage:

Scoping, rollout and support for agents like this is described on the [AI agent development page](https://matintellect.com/en/services/ai-agents)
