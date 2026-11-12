# AI voice agent: architecture notes for a voice front end on top of an agent system

Type: architecture note and launch checklist. Reader: a developer or technical founder adding voice to an existing set of AI agents. Goal: understand which layers a voice agent needs, how one spoken instruction flows through them, and which checks to run before giving it real access. Limits: this describes the structure of working setups in prose; it does not ship runnable code or configuration, and the checklist at the end is a template, not a tested configuration

![AI-generated illustration of an AI voice agent and the system behind it](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-ai-voice-agent-needs-system-1793019689.jpg)

## Reference systems

Two setups inform these notes. Verified facts, as published on my project pages:

- My personal agent Jes lives in Telegram and accepts text and voice notes. Behind it are 10 scheduled jobs and 7 other bots it hands work to; since July it has passed on 165 tasks, and it has been running for 134 days
- Ami, a voice agent for the owner of an aesthetic medicine clinic. The owner opens a private page, presses Start and talks; a face appears and Ami answers in English or Russian. A fast model handles small talk, real requests go to the clinic's agent with tools, memory is shared with the Telegram assistant, and everything runs on the clinic's server. The clinic already had a team of 6 agents before voice was added. The voice layer on top of that took about 2 weeks

## Core principle

Voice is an input channel, not a worker. Every instruction that should change something must end at a component that can act: an agent with tools, a scheduled job or an approval gate. A voice layer with nothing behind it can only talk

## Layers

| Layer | Responsibility | Failure signal |
|---|---|---|
| Access | Private page with a password; strangers get no reply | Agent answers from an unknown device |
| Speech recognition | Turns speech into text | Names, amounts and dates come out wrong |
| Fast conversational model | Greets, clarifies, acknowledges instantly | Promises results the system cannot deliver |
| Router | Splits an utterance into parts and picks a destination for each | One of two combined instructions disappears |
| Agent with tools | Does real work and returns a result | Task accepted, no result anywhere |
| Scheduler | Runs recurring and delayed work without a prompt | Owner repeats the same instruction every day |
| Shared memory | One record for voice and text | Things said by voice are unknown in chat |
| Approval gate | Holds spending and client messages until a human confirms | A risky action ran on a spoken phrase |
| Speech output | Reads the result back | Long silence after the acknowledgement |

## Data flow for one instruction

1. The owner says: "Check the server and remind me tomorrow at ten about the supplier invoice"
2. Recognition produces text
3. The fast model replies "Got it, working on it" so there is no silence
4. The router splits the text into two parts: a server check and a reminder
5. The server check goes to the agent with tools; its result is spoken back when ready
6. The reminder goes to the scheduler and fires tomorrow without anyone speaking
7. Both items are written to shared memory, so the text assistant knows about them
8. Had the sentence included "pay the invoice", that part would go to the approval gate and wait for a confirmation in a channel where the amount is shown in writing

![A sound mixing console](https://images.pexels.com/photos/33204438/pexels-photo-33204438.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Why two models

In speech a two second pause is noticeable; in chat it is not. Routing every utterance through a tool using agent makes the conversation drag. Splitting conversation from work keeps the reply instant and lets the slow part run in the background. The contract between the two is simple: the fast model never claims a result, it only acknowledges and relays

## Security notes

- Keep the voice page private. A voice agent with tools is an operator console, not a public chatbot
- Do not accept spoken confirmations for risky actions. Recognition can mishear numbers; confirm in writing
- Run the system where the owner's keys already live. In the clinic case it runs on the clinic's server and the keys stay there

## Failure modes and expected behaviour

| Failure | Expected behaviour |
|---|---|
| Request matches no skill | Fast model says the system cannot do it yet |
| Agent is slow | Acknowledgement already given; after a set time, result is promised to the chat |
| Recognition mishears a word | Risky actions stop at approval, so the cost is one card |
| Agent unavailable | Voice says so instead of pretending the task was done |
| Two instructions in one sentence | Both reach their destinations, or the missing one is reported |

## Real limits

- The voice cannot be more reliable than the agents behind it
- Voice adds a second front end to maintain, alongside chat
- If there is no agent system yet, it has to be built first; voice on an empty system is a demo

![Network cables in server equipment](https://images.pexels.com/photos/4682189/pexels-photo-4682189.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Launch checklist (template)

- List the five instructions the owner will give by voice most often and the component that executes each
- Confirm that each of them works by text before voice is added
- Define the approval set: spending, client messages and anything irreversible
- Confirm that memory is shared between voice and chat
- Test access from an unknown device: no reply expected
- Test a request the system cannot handle: honest refusal expected
- Test a combined instruction: both parts must arrive

More on how voice agents are scoped on top of existing systems is on the [AI voice agent service page](https://matintellect.com/en/services/voice-ai-agent) of my site
