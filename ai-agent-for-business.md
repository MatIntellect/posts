# AI agents for business: architecture notes for a personal operations agent

Type: architecture note and design worksheet. Reader: a developer or technical founder planning an agent that runs everyday business tasks. Goal: understand which components such an agent needs, how a request flows through them and where human approval sits. Limits: this describes the structure of a working setup in prose; it does not ship runnable code or configuration, and the worksheet at the end is a teaching template, not a tested configuration

![AI-generated illustration of a personal AI agent working for a business owner](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-ii-agent-biznes-assistent-jes-1791298177.jpg)

## Reference system

The notes are based on my personal agent Jes. Verified facts about it, as published on my project page: it has been running for 134 days, lives in Telegram, understands text and voice notes, remembers earlier conversations and my profile, runs 10 scheduled jobs on its own, hands tasks to 7 other bots and has passed on 165 tasks since July. Anything risky, paid or public happens only after my explicit yes

## Components

| Component | Responsibility | Why it is separate |
|---|---|---|
| Chat interface | Receives text and voice notes, sends approval cards | Users already live in a messenger; no new app to install |
| Speech recognition | Turns voice notes into text | Voice is the fastest input on the go |
| Language model, primary | Understands requests, drafts work, picks a delegate | Replaceable part |
| Language model, backup | Takes over if the primary fails or hits a limit | Keeps work moving during outages |
| Memory | Earlier conversations, user profile, written rules | Must survive a model swap |
| Scheduler | Recurring jobs such as morning checks and reminders | Runs on time without a prompt |
| Delegation | Hands tasks to specialised bots such as a copywriter | Keeps each bot's job narrow |
| Approval gate | Holds irreversible actions until a human confirms | Single place for the riskiest decision |
| Service supervisor | Restarts the agent after a crash | The agent must not depend on a laptop being on |

## Data flow for one request

1. Input arrives in the chat: for example a voice note asking for a reminder at 10:00 and a post draft from the copywriter
2. Speech recognition produces text
3. The model splits the text into independent intents: a reminder for the owner and a task for another bot
4. The reminder goes to the scheduler and fires at the requested time
5. The task goes to the copywriter bot with context; the bot returns a draft to the agent, not to the public
6. Publishing is an irreversible action, so the approval gate sends a card: what, where, current state, with Yes and Edit buttons
7. Yes releases the action. Edit returns the draft with the owner's comment, and the agent records the reason as a rule for next time

![Developer reviewing an AI agent workflow on a laptop](https://images.pexels.com/photos/16094038/pexels-photo-16094038.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Approval policy

In the reference system four action kinds always require approval: deleting data, spending money, messaging clients and publishing. Two design rules follow from running it

- Keep the decision in one place. If each tool decides for itself whether it needs approval, the checks drift and one eventually forgets
- Keep the card short. What, where and state. A long approval message turns into a reflexive click

For new tools, prefer default-deny: treat an unknown action as risky until someone decides otherwise

## Failure modes and expected behaviour

| Failure | Expected behaviour |
|---|---|
| Model misunderstands a request | Mistake is visible on the approval card; cost is one Edit |
| Primary model unavailable or rate limited | Backup model continues the work |
| Agent process crashes | Supervisor restarts it automatically |
| Owner does not answer a card | Action stays pending; decide in advance whether to remind or expire, never proceed silently |
| Same correction needed twice | The written rule is unclear and should be rewritten |

## Real limits

- Approval adds latency by design
- The agent only knows what it has been shown; undocumented steps of a process stay invisible to it
- Self-hosting keeps data under the owner's control and makes memory portable, but someone has to keep the service healthy
- In my experience building an agent like this takes one to two weeks, mostly spent on memory, approval rules, scheduling and testing on real data

![Documents and a laptop during a design review](https://images.pexels.com/photos/9052851/pexels-photo-9052851.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Design worksheet (teaching template)

Fill this in before writing any code. It is a template, not a tested configuration

- First job: one repetitive task with a clear input and a clear result
- Input source: mailbox, spreadsheet, chat or calendar
- Expected output and how to check it is correct
- Actions the agent may take unattended
- Actions that require approval
- Behaviour when the model is unavailable
- Where corrections are written so the agent reads them next time
- Who watches the service and how they learn it stopped

More context on how these agents are scoped for real businesses is on the [AI agent development page](https://matintellect.com/en/services/ai-agents) of my site
