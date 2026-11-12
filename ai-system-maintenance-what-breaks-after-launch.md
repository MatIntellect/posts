# AI system maintenance: runbook template for the first months after launch

Type: operations runbook template. Reader: whoever owns an AI system after launch, technical or not. Goal: know what typically breaks, what must exist before launch, and what to check daily, weekly, monthly and after changes. Limits: a template in prose and tables; no runnable code or configuration

![AI-generated illustration of AI system maintenance after launch](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-ai-system-maintenance-what-breaks-after-launch-1792199900.jpg)

## Reference systems

Verified facts, as published on my project pages:

- my personal agent Jes has been running for 134 days as a server service that restarts itself after a failure; a backup model takes over if the main one fails; after each correction it writes itself a new rule
- my subtitle assistant reports failures and retries; each video is transcribed only once, so a retry costs nothing extra
- my morning plan has arrived for 127 days in a row
- assistants I have set up run for five people on their own servers; a clinic runs a team of 6 agents
- getting a half-finished, failing system into working shape takes 1–2 weeks depending on size; maintenance then runs in monthly cycles

## What breaks

| Cause | Example | Symptom |
|---|---|---|
| Data drift | Price list, schedule, invoice format or supplier page changes | Answers look fine but are based on old data |
| Dependency change | Model update, platform rules or limits change | Behaviour changes with no code change |
| Real usage | Typos, half sentences, unplanned questions | Failures where tests never looked |
| Business change | New service, rule or process | Logic quietly stops matching |

None of these means the system was built badly; it lives inside a moving business

## Before launch

| Item | Requirement |
|---|---|
| Failure message | The system reports failures itself; recipient and channel decided |
| Log | Input, answer and reason recorded for every request |
| Live-answer reviewer | A named person reviews real answers, not only status reports |
| Replay set | Ten to twenty real requests with approved answers |

![Repairing a component in a workshop](https://images.pexels.com/photos/10468213/pexels-photo-10468213.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Schedule

| When | Check |
|---|---|
| Daily | Review failure messages; confirm recurring jobs ran; confirm retries did not duplicate results |
| Weekly | Sample live answers; list weak or missing answers; check source data for changes; watch for more requests to talk to a human |
| Monthly | Review log and live answers; list failures and weak answers; reconcile data with business changes; fix logic; confirm fixes broke nothing nearby |
| After a model update | Replay the set; compare meaning, tone, figures and rule compliance; adjust rules or roll back |
| After a business change | Update source data the same day; review dependent logic; replay requests on the new topic |

## Reading the log

| Pattern | Meaning |
|---|---|
| Same client repeats a question | The system did not understand the first time |
| Client leaves or asks for a human after an answer | The answer did not help |
| Long delay before an answer | A slow external service or model |
| Same error at different times | A logic fault, not chance |

## Weak-answer list format

| Field | Content |
|---|---|
| Date | When it happened |
| Request | What was asked |
| Answer | What the system said |
| Expected | What it should have said |
| Cause | Stale data, new phrasing, model change, business change |

The cause tells you where to fix: data, rules or logic

## Silent decline

- answers become shorter or longer for no reason
- clients ask for a person more often
- fewer tasks are handed on while requests stay the same
- figures stop matching the price list or schedule
- status reports say all is well while live results drop

![Monitoring a system on a dashboard](https://images.pexels.com/photos/33118659/pexels-photo-33118659.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Existing broken systems

Start with an inspection without changes: what works, what is broken, where the keys are, what is spending money. Then decide what to finish and what to rebuild, and move the system onto this runbook

## Roles

- someone who knows the business notices problems in live answers
- someone who knows the system finds causes and fixes logic
- a short path between them: notice, record one line, hand over

More on how ongoing support is organised is on the [AI support service page](https://matintellect.com/en/services/ai-support) of my site
