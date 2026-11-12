# AI agent architecture: a five-question design record template

Type: design record template with two filled examples. Reader: a developer, architect or technical founder starting an AI agent or multi-agent system. Goal: decide who does what, where it runs, on which data, what it produces and in what format, before any code is written. Limits: a planning template in prose and tables; it ships no runnable code or configuration

![AI-generated illustration of AI agent architecture and the questions before code](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-ai-agent-architecture-questions-before-writing-code-1792115525.jpg)

## Why a record before code

A decision made before code costs one line in a diagram. The same decision corrected after launch costs a rewritten system. The five questions cover the decisions that most often get rewritten

## Template

| Question | Answer | Check |
|---|---|---|
| Who does what | Model jobs, code jobs, person jobs | Exact work is in code; accountable decisions are with a person |
| Where | Server, laptop, other | Always-on systems run as a service and restart after failure |
| Data | Request sources and knowledge base | The knowledge base exists now, in current form |
| Result | A concrete action: booking, CRM request, card | Someone can look at it and say done or not done |
| Format | Recipient, channel, frequency | Per event or as a daily summary, stated explicitly |

## Filled example 1: AI salesperson for a clinic's Instagram Direct

Verified facts, as published on my project pages

| Question | Answer |
|---|---|
| Who does what | Python watches the script: required fields collected, model reply within limits. Claude decides what to say using its rules and the knowledge base. The doctor confirms bookings |
| Data | Requests from Instagram Direct. Knowledge base: the clinic's documents, about 114 price items and 48 services. Built and tested on real questions from the clinic's conversations |
| Result | A card to the doctor; a booking appears only after the doctor confirms, the bot never creates one |
| Format | Card in Telegram per conversation |

Design note: the script and the knowledge base are separate. The script sets order and required fields; the knowledge base supplies content. Anything not in the documents is not invented and goes to the owner as a card

![Designing a system diagram on a whiteboard](https://images.pexels.com/photos/1181343/pexels-photo-1181343.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Filled example 2: content team of agents

| Question | Answer |
|---|---|
| Who does what | A Python program builds the morning brief; a marketer agent adds what worked yesterday and suggests what to post; copywriter and designer agents do their parts; I approve publication |
| Where | A team of 8 agents on one server |
| Data | 20 live questions people ask AI and 10 topics each morning |
| Result | Material ready for publication, released only after approval |
| Format | Each agent in its own Telegram topic; the brief every morning |

## Shared principle

| Part | Takes | Because |
|---|---|---|
| Code | Exact, repeatable steps: counting, required fields, order | Guarantees the same output every time |
| Model | Meaning and conversation | Understands context but is not deterministic |
| Person | Decisions someone is accountable for | Responsibility cannot be delegated to the system |

## Reliability belongs in the record

My personal agent runs on a server as a service: around the clock, restarting itself after a failure. If the main model fails, a backup takes over on its own. Both decisions sit in the answers to "who" and "where", not in a fix written after the first outage

## Red flags

- the result is "a bot", "an assistant" or "automation" instead of a concrete action
- the knowledge base is "coming later"
- the model is responsible for counting, required fields or step order
- accountable decisions are taken by the system without confirmation
- an always-on system lives on a laptop
- nothing is said about the main model being unavailable

## Coupled answers

Answers depend on each other. Changing the result from a card to an automatic booking adds a code job (check free slots) and a format item (notify the doctor of each booking). Adding two more request channels adds data sources and a code job to merge them into one stream. Rewrite the record as a whole after any change

![Messages on a smartphone](https://images.pexels.com/photos/6669813/pexels-photo-6669813.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## After the record

When all five answers are written and no red flag remains, draw the component diagram: what each part receives and passes on. Choose tools to fit it. The record may also show that no AI agent is needed and an ordinary program will do

More on how these designs are worked out is on the [AI architecture service page](https://matintellect.com/en/services/ai-architecture) of my site
