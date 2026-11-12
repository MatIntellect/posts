# Multi-agent system for business: role cards and handoff rules

Type: design template with filled examples. Reader: a developer or technical founder deciding whether to split one AI agent into a team, and how to describe each role. Goal: make the split decision from evidence and specify every role and handoff before building. Limits: a planning template in prose and tables; no runnable code or configuration

![AI-generated illustration of a multi-agent system for business](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-multi-agent-system-for-business-when-to-build-a-team-1793173075.jpg)

## Reference systems

Verified facts, as published on my project pages:

- my personal agent Jes runs 10 scheduled jobs on her own and hands other bots only work that needs a separate skill; it stays a single agent
- my content team is 8 agents on one server, designed as one architecture with clear roles; marketer, copywriter and designer each work in their own Telegram topic, and tasks can be given by text or voice in that topic
- a program collects 20 live questions people ask AI and 10 topics each morning; the marketer adds what worked yesterday
- over three months the team produced 80 morning briefs and 94 images; publishing goes through a content pipeline only after my approval, and agents neither publish nor spend on their own
- models: Sonnet 5 and Opus 5.5, assigned per role
- a clinic runs a team of 6 agents the same way on the owner's own server; launching such a team takes about 2–3 weeks

## Split decision

| Test | Split if |
|---|---|
| Repetition | The task repeats systematically |
| Knowledge | It needs its own knowledge base |
| Memory | It needs its own memory of corrections |
| Tools | It needs its own tools |
| Evidence | The single agent is corrected in this area more than in others |

If fewer than the first three hold, keep one agent

## Role card

| Field | Content |
|---|---|
| Role | One line |
| Assignment | The result expected |
| Input | What it receives and from whom |
| Output | What it hands on and to whom |
| Knowledge | Rules, examples, documents |
| Memory | What it keeps after corrections |
| Tools | What it uses |
| Check | Who reviews before handoff |
| Never alone | Publishing, spending, messaging clients |

A role with an empty field is not ready

![A writing workspace](https://images.pexels.com/photos/23508096/pexels-photo-23508096.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Filled cards

| Field | Copywriter | Designer | Marketer |
|---|---|---|---|
| Assignment | Post text and three headline options | Image for the post | Morning brief and a suggestion for today |
| Input | Topic and source material | Approved topic, meaning of the post, image requirements | 20 live questions and 10 topics from a program |
| Knowledge | Writing rules and style examples | Format, visual style, what must be in frame | What worked yesterday |
| Memory | Lessons from corrections | Own lessons, not writing rules | Own history |
| Check | Owner chooses the headline | Draws only after the owner's yes | Owner reads the brief |
| Never alone | Publishing | Publishing | Publishing and spending |

## Handoff rules

- only approved versions move on, never drafts
- every handoff has a named checker
- the finished pair, text and image, is checked together
- publication is a separate step and needs human approval

Reason: most failures in agent teams happen at handoffs, not inside roles. An image drawn from a draft stops matching once the text changes

## Flow of one post

1. Marketer sends the morning brief
2. Owner picks a topic and assigns it in the copywriter's topic
3. Copywriter writes and offers three headlines
4. Owner chooses and approves the text
5. Designer receives the approved meaning and draws after the owner's yes
6. Pair is checked together
7. Content pipeline publishes after approval

## Memory separation

One shared memory grows and starts to interfere: a writing lesson pulls into images and an image lesson into text. Separate memories keep each lesson where it applies

![Working with a graphics tablet](https://images.pexels.com/photos/7968765/pexels-photo-7968765.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Common mistakes

- building a team before one agent has worked on real tasks
- a role with a title but no assignment
- one shared rule base for all agents
- passing drafts downstream
- letting agents publish or spend without a person

## Verification

Log corrections per area before and after a split. If corrections in the split area did not drop, the problem was the rules, not role mixing

More on how agent teams are designed is on the [AI architecture service page](https://matintellect.com/en/services/ai-architecture) of my site
