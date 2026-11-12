# AI development for business: project stages, exit criteria and client checklist

Type: process specification. Reader: a client commissioning a first AI project, or a developer running one. Goal: define the five stages of an AI project with inputs, outputs, exit criteria and the questions to ask at each. Limits: reflects my own practice; timelines are from my projects, not guarantees

![AI-generated illustration of AI development from first call to launch](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-ai-development-from-first-call-to-launch-1791594709.jpg)

## Overview

| Stage | Share of effort | Output |
|---|---|---|
| 1. Discovery | Together with the audit, around 70% of the time | Agreed problem statement, go or no-go |
| 2. Audit | | Blueprint: data, bottleneck, solution, success metric |
| 3. Build | The rest | System assembled to the blueprint |
| 4. Test and launch | | Results on real data; launch on a small share |
| 5. Support and development | Ongoing | Fixes, new rules and scenarios |

Each stage rests on the previous one; none can be skipped

## Stage details

| Stage | Inputs | Exit criteria | Typical failure |
|---|---|---|---|
| Discovery | Client's description, access to people doing the work | Problem stated in one or two sentences both sides accept | Vague goal like "make it easier with AI" |
| Audit | Process walkthrough, real data samples | Current cost measured; data inventory; bottleneck named; success metric | General talk about AI with no numbers about the process |
| Build | Blueprint | System matches blueprint; handoff rules defined | Rework because there was no blueprint |
| Test and launch | Real messages, calls, documents | Tested on real data; launched on a small share; monitoring owner named | Testing on invented examples; launching to everyone at once |
| Support | Live traffic | Fix and rule log; regular review | Nobody watching after launch |

![An architect working on a blueprint](https://images.pexels.com/photos/7988079/pexels-photo-7988079.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Evidence from my projects

- A clinic chatbot was built and tested on real questions from the clinic's inbox and covers about 114 price items and 48 services
- My call and CRM automation has processed about 40 calls with 15 clients; the morning plan has arrived 127 days in a row
- Turnkey content factory: about a week. Team of AI agents or call and CRM automation: about 2–3 weeks

## Client checklist

Before the first call:

- [ ] Which work should become easier, and why this one
- [ ] How long it takes now, and who does it
- [ ] Where the data lives: spreadsheets, messages, calls, documents
- [ ] What success looks like a month after launch
- [ ] What must never be handed to a machine unchecked

Questions for the developer:

- [ ] How is the audit done, and what will I receive
- [ ] Which real data will the system be tested on
- [ ] What happens when it makes a mistake after launch
- [ ] Who supports it and how quickly they respond
- [ ] Can you show a working project and what went wrong in it

![Developers writing code](https://images.pexels.com/photos/9617369/pexels-photo-9617369.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## What the client provides

| Item | Why |
|---|---|
| Time for discovery and audit | The blueprint depends on the people doing the work |
| Real data | The system learns and is tested on it |
| A reviewer after launch | Someone has to say where the system was wrong |

## What the developer owes the client

At the end of each stage the client should receive something they can read: a written problem statement after discovery, the blueprint after the audit, a short test report on real data before launch, and a log of fixes and new rules during support. If a stage ends without such a document, it is not finished, and moving on only postpones the questions it should have answered

## Red flags

- Exact price and deadline before any look at the data
- No questions about the client's data
- No mention of support
- Testing only on invented examples

## When a project stalls

Return to the blueprint before writing more code. Stalls usually come from a loosely framed problem or an audit that missed the real bottleneck. Checking whether the blueprint still answers the original question is cheaper than another round of development

## Why support starts on day one

The first days after launch are when a system first meets real traffic: people who write differently from the tests, documents in unexpected shapes, questions nobody anticipated. Treating those weeks as part of the project, not as an optional extra, is what turns a launch into a system that works every day

More on AI development is on the [AI development page](https://matintellect.com/en/services/ai-development)
