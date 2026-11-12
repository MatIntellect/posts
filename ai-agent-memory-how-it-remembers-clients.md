# AI agent memory: a design template for client-facing agents

Type: design template and test plan. Reader: a developer or architect adding memory to an AI agent that works with clients. Goal: decide what the agent remembers, in which layer, with which metadata, who can see it, and how it is corrected and forgotten. Limits: a planning template in prose and tables; no runnable code or configuration

![AI-generated illustration of AI agent memory and how it remembers clients](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-ai-agent-memory-how-it-remembers-clients-1794099210.jpg)

## Reference systems

Verified facts, as published on my project pages:

- my personal agent Jes has been running for 134 days; it remembers earlier conversations, my profile and my rules, and writes a new rule for itself after each correction
- since July Jes has passed 165 tasks to other bots, which requires remembering who received what and what came back
- the voice agent built for a clinic shares memory with the owner's Telegram assistant: what is said by voice is known in chat and the other way round
- the clinic chatbot answers only from documents, about 114 price items and 48 services, and sends anything else to the owner as a card; it does not need long client memory
- a personal agent with memory, approval rules and a schedule takes one to two weeks to set up

## Decision 1. Does the agent need long memory

| Agent works | Long memory |
|---|---|
| Within a single conversation, from fixed documents | No; keep it out |
| With one client or task over days and weeks | Yes |
| Across several channels for one person | Yes, one shared store |

## Decision 2. Remember and never remember

List three things the agent must remember about every client and one it must not. Everything else is designed around this list

## Layers

| Layer | Holds | Risk | Mitigation |
|---|---|---|---|
| Working | Current request and conversation details | Grows without limit | Rotation |
| Compressed | Summaries of long conversations | Important detail dropped | Link to the full transcript |
| Long-term | Records of needs, agreements, decisions, changes | Goes stale | Source, date, status on every record |
| Archive | Everything rotated out | Search returns old data | Exclude from default retrieval |
| Rules | How to work, learned from corrections | Mixed with client facts | Separate store from facts |

Rotation in the reference setup runs daily or weekly per agent, depending on how often it is used

![Archive with rows of filing drawers](https://images.pexels.com/photos/17489151/pexels-photo-17489151.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Record schema

| Field | Purpose |
|---|---|
| Client | Keeps clients apart |
| Topic | What the record is about |
| Text | The fact or agreement |
| Source | Link to the original conversation |
| Date | When it was agreed |
| Status | Active or retired |
| Replaced by | Newer record, if any |
| Corrected by | Who changed it and when |

A newer agreement retires the older record instead of deleting it

## Retrieval

- a separate process reads conversations and files facts, decisions and conclusions; the database stores, it does not analyse
- combine meaning-based and keyword search
- return records with their source
- important decisions are checked against the original, not taken from search on trust
- a miss produces "not on record", never a guess

## Access, correction, deletion

| Concern | Rule |
|---|---|
| Separation | Records filtered by client before any other step |
| Visibility | Only agents and people who need a client's records can read them |
| Correction | Any record can be fixed or retired, and the change is logged |
| Deletion | One request removes a client from every layer, archive included |

## Test scenarios

| Scenario | Expected |
|---|---|
| Client repeats a question from a past conversation | Agent does not ask again |
| Client cites an agreement that changed | Agent states the current version with its date |
| Two clients with similar requests | No detail of one appears for the other |
| Owner corrects the agent | Mistake does not repeat the next day |
| Record missing | Agent says so and asks |
| Client asks to be forgotten | No record remains in any layer |

![Servers in blue and red light](https://images.pexels.com/photos/6549926/pexels-photo-6549926.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Common mistakes

- long memory for an agent that answers from fixed documents
- storing everything without a remember and never-remember list
- records without date and source
- one memory for all clients
- trusting retrieval without checking the original
- a separate memory per channel

More on how memory fits with tasks and other components is on the [AI architecture service page](https://matintellect.com/en/services/ai-architecture) of my site
