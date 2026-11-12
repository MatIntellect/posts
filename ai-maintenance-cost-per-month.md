# AI maintenance cost: monthly budget template for an AI system

Type: budget template. Reader: an owner or operations lead planning the running cost of an AI system. Goal: list every monthly cost line, choose how to pay for models, and compare the total with the value the system frees. Limits: a planning template in prose and tables; no runnable code; prices quoted are my own bills, not quotes for anyone else

![AI-generated illustration of AI maintenance cost per month](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-ai-maintenance-cost-per-month-1793331699.jpg)

## Reference budget

Verified facts, as published on my project pages and site:

| Line | Monthly cost |
|---|---|
| Claude subscription | $200 |
| ChatGPT subscription | $20 |
| GLM subscription | $20 |
| Server | $30 |
| Total | about $300 |

- by my estimate, the same usage billed per token through the APIs would be about $30,000 a month; this is specific to my volume of work
- this budget covers about 2–3 large projects a month plus development of my own system
- on it, 8 Claude Code agents work every day; my personal agent Jes has run 10 scheduled jobs for 134 days and passed 165 tasks to other bots since July; the content pipeline has produced 84 posts; the marketing agent has sent 80 morning briefs over three months
- client systems run on the client's own server and AI subscription; a clinic runs a team of 6 agents that way; assistants run for five people on their own servers

## How to read the reference budget

The figure is small because subscriptions carry most of the load. Subscriptions and per-token billing are different products: a subscription is a flat price for work within a plan's limits, while an API bill scales with use and is paid separately from any chat subscription. The $30,000 estimate is what my measured usage would cost on per-token billing; it is not a saving anyone else should expect. Subscription limits used to be far more generous, and they keep changing, so the budget is reviewed rather than fixed

## The four lines

| Line | What it covers | Often forgotten |
|---|---|---|
| Models | Subscription, pay-per-use or own hardware | Limits and how fast they burn |
| Server | Always-on hosting | Needed as soon as the system runs around the clock |
| Services | Speech recognition, images, mailings | Each one billed separately |
| Support | Failure checks, model updates, changes for new tasks | Usually missing entirely |

Support is the line that keeps the other three useful. Data drifts, models are updated, the business adds services, and someone has to notice and adjust. Budget it as hours per month times a rate, so it can be compared with the rest and does not disappear into "we will deal with it later"

## Choosing how to pay for models

| Workload | Usually better |
|---|---|
| Daily, steady, many tasks | Subscription, within its limits |
| Light or bursty | Pay per use |
| Data must never leave | Own hardware, if the model and volume justify it |
| Unsure | One month on a subscription, then decide from observed use |

![Server equipment](https://images.pexels.com/photos/17489151/pexels-photo-17489151.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Estimating load

| Factor | Effect on volume |
|---|---|
| Requests per day | Linear |
| Conversation length | Strong; long threads multiply text |
| Tool use | Strong; tool calls add text both ways |
| Always on or on demand | Determines whether scheduled work adds volume |

## Plan versus actual

| Line | Planned | Actual | Note |
|---|---|---|---|
| Models | | | |
| Server | | | |
| Services | | | |
| Support | | | |
| One-off | | | Keep separate from regular costs |

Review monthly for the first months, then whenever the provider changes limits or prices, an agent or task is added, or the model changes

## Comparing with value

Total of the four lines versus hours freed per month times their cost. If the second is clearly larger, the system pays for itself; if not, revisit the system or the task

## Savings by design

- do work once: the subtitle assistant transcribes each video only once, so reprocessing costs nothing
- keep local what can be local: long calls are transcribed on my own computer
- route simple tasks to fast models and keep expensive ones for work that needs depth
- watch limits and move work between models when they change

![Workstations with computers](https://images.pexels.com/photos/6804612/pexels-photo-6804612.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Common mistakes

- budgeting the subscription only
- comparing subscription and API bills by price instead of workload
- using the strongest model for every task
- no comparison with freed hours

More on what ongoing support includes is on the [AI support service page](https://matintellect.com/en/services/ai-support) of my site
