# How much does an AI agent cost: a scoping worksheet and cost-driver reference

Type: reference note and worksheet. Reader: a founder or developer preparing to commission or build an AI agent. Goal: turn "how much does an AI agent cost" into a defined scope that can be estimated. Limits: this note contains no prices; reference timelines come from my own projects and are not guarantees for yours. The worksheet is a teaching template, not a tested configuration

![AI-generated illustration of the parts that shape an AI agent's cost](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-how-much-does-an-ai-agent-cost-1792290476.jpg)

## Cost drivers

| Driver | What it means | Why it changes the effort |
|---|---|---|
| Jobs | Concrete pieces of work: task list, triage, reminders, client replies, publishing | Each job has its own input, output and tests |
| Connections | Services the agent reads or writes: mail, calendar, spreadsheet, messenger, drive | Each one needs setup, permissions and testing |
| Approval gates | Actions that wait for a human yes | Each gate needs a card, buttons and a test that nothing leaves without the click |
| Memory | What the agent keeps between conversations | Must be designed so it survives a model swap |
| Schedule | Jobs that run on a timer rather than on request | Needs time-based testing and failure handling |
| Resilience | Backup model, automatic restart | Prevents the agent from silently stopping |

## Reference system

The numbers below describe my own setup, as published on my project pages. A personal agent, Jes, has been running for 134 days, runs 10 scheduled jobs and hands tasks to 7 other bots; 165 tasks have gone through her since July. Four action kinds always require my approval: deleting data, spending money, messaging clients and publishing. A separate content factory watches 13 news sources and has published 84 posts

![Planning jobs before estimation](https://images.pexels.com/photos/39204858/pexels-photo-39204858.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Reference timelines

| Scope | Typical duration in my projects |
|---|---|
| Personal agent with memory, approval rules, schedule and testing on real data | one to two weeks |
| Narrow helper, for example video subtitles | from 3 days |
| Sales chatbot across several channels | about 2–3 weeks |
| Voice entrance on top of an existing system | about 2 weeks |

## One agent or several

A single agent expected to cover marketing, copywriting, client work and design accumulates mixed memory and conflicting rules. Splitting by role usually makes each part simpler to configure and test. In the reference system, the coordinating agent does not write posts or draw images; dedicated bots do, and the coordinator only routes and tracks

## Failure modes in estimation

| Failure | Symptom | Prevention |
|---|---|---|
| Vague job | The same word means different work to each side | Describe every job as input and output |
| Hidden connection | A data source appears mid-project | List every source before estimating |
| Missing gate | The agent can already send messages, the approval rule is not designed | Decide approval per job up front |
| Optimistic testing | Works on samples, fails on real data | Budget time for testing on the client's data |
| No correction loop | The same mistakes return after launch | Agree where corrections are written and read |

![Budget review for an automation project](https://images.pexels.com/photos/5480781/pexels-photo-5480781.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Worksheet (teaching template)

Fill in before asking for an estimate. Untested template

- Jobs, one line each
- For each job: input source and expected output
- Connections required, and which ones can be dropped
- Actions that require approval
- What the agent must remember between conversations
- Which jobs run on a schedule and which on events
- Who approves, and how quickly they usually respond
- Where corrections will be written so the agent reads them next time

## Ownership note

An agent hosted on your own server keeps its memory and rules with you and can be moved to another system. An agent hosted inside a third-party service usually cannot. This affects long-term cost more than the initial build

The same applies to the correction loop. Rules the agent has learned from corrections are part of its value: in the reference system they made the agent more accurate over time than any new feature did. If those rules live only inside a vendor's platform, they are lost with the contract

More on how these agents are scoped and built is on the [AI agent development page](https://matintellect.com/en/services/ai-agents) of my site
