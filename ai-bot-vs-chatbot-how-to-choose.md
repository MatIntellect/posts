# AI bot vs chatbot: decision table for program steps and model steps

Type: design decision guide. Reader: a developer or product owner scoping a bot for a business. Goal: decide, step by step, which parts are an ordinary program and which need a language model, and where checks go. Limits: guidance from my own systems; adapt the markers and examples to your domain

![AI-generated illustration of an AI bot vs a chatbot](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-ai-bot-vs-chatbot-how-to-choose-1793847670.jpg)

## Definitions

| | Ordinary bot (program) | AI bot (model attached) |
|---|---|---|
| How it chooses actions | Rules written by the developer | Interprets input, chooses within allowed actions |
| Consistency | Same result every time | Can vary between runs |
| Running cost | Almost none | Tokens or subscription quota per call |
| Memory, schedule, files | Possible, built by the developer | Possible, also built by the developer; the model does not provide them |
| Weak spot | Unforeseen cases | Confident wrong answers |

## Reference systems

| System | Program part | Model part |
|---|---|---|
| Morning plan | Everything: calendar, tasks, reminders; 127 days in a row; reminders checked every 5 minutes, 240 sent | None |
| Content factory | Watches 13 sources, selects topics, checks, publishes | Gathers material, writes in my voice, checks facts |
| Marketer brief | Python program collects 20 live questions and 10 topics | Agent adds what worked yesterday |
| Clinic chatbot | Prices from the price list | Natural-language answers only from documents covering about 114 price items and 48 services |

![Working with a program](https://images.pexels.com/photos/36496927/pexels-photo-36496927.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Step assignment rules

| If the step | Assign to | Notes |
|---|---|---|
| Is the same every time | Program | |
| Produces exact data: price, date, count, total | Program | Even inside a conversation |
| Needs interpretation of free text | Model | Followed by a check if output matters |
| Writes wording for a person | Model | Numbers inserted from program output |
| Decides on money, clients or publishing | Human | Model or program prepares, human approves |

Test for a model step: can it be described without "depending on", "as appropriate" or "work out what they meant"? If yes, it is a program step

## Combining program and model

The usual answer is both. A program keeps the order of steps and a model handles content: the program receives a message, hands it to the model for a draft, checks the draft passed the required stages, and only then sends it on for approval. If the model slips, the program catches it; if the program meets an unforeseen case, the model helps interpret it. Function calling is the bridge: the model asks the application to act, and code performs the action and returns the result

## Worked example (teaching)

Job: evening summary of incoming requests for a manager

| Step | Owner |
|---|---|
| Fetch requests from the sheet | Program |
| Count received, handled, lost | Program |
| Find recurring complaints in comments | Model |
| Compose message: numbers plus short conclusion | Program inserts numbers, model writes conclusion |
| Send to Telegram | Program |

One step in five needs a model

## Questions for whoever builds the bot

- Which steps use a model, and why
- Where prices, dates and numbers come from
- Who checks model output before it reaches a customer
- Where memory is stored and how scheduling is configured
- What the model will cost per month at your volume

![Discussing a decision](https://images.pexels.com/photos/9783346/pexels-photo-9783346.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Diagnosis table

| Symptom | Likely cause |
|---|---|
| High monthly cost for simple repetitive work | Model used where a program would do |
| Frequent failures on unusual wording | Program used where interpretation is needed |
| Confident wrong numbers | Exact data assigned to the model |
| Bot forgets previous conversations | Memory not implemented |

## Why not everything on the model

A single prompt that does everything is quick to start and hard to live with: every call costs money, the same case is handled differently on different days, wrong numbers hide in fluent text, and failures are hard to locate because everything sits in one instruction. Splitting steps costs a little more at build time and pays back in cost, consistency and debuggability

More on choosing and building bots on the [AI development page](https://matintellect.com/en/services/ai-development)
