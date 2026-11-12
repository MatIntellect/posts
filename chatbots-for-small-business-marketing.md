# AI chatbot for small business: launch checklist and handover specification

Type: launch checklist and specification. Reader: a developer or owner setting up an AI receptionist for a salon, clinic, studio or shop. Goal: define what the bot answers, from which documents, when it hands over to a person and how success is measured. Limits: based on bots I have built; the templates are teaching material, not a tested configuration

![AI-generated illustration of chatbots for small business marketing](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-chatbots-for-small-business-marketing-1791525778.jpg)

## Scope

| Bot handles | Person handles |
|---|---|
| Prices and what a service includes | Selling and persuasion |
| Free slots and booking | Objections such as "why are you more expensive" |
| Address, directions, parking | Complaints |
| Reminders, confirmations, rescheduling | Discounts, payment plans, any promise |
| Typical questions answered in the documents | Anything not in the documents |

Reference: the most recent bot I built is for a clinic. It answers only from the clinic's documents, about 114 price items and 48 services, steers toward booking and passes anything else to the owner as a card. It was built and tested on real questions from the clinic's inbox. A bot like this, with testing, takes about 2–3 weeks

## Why these boundaries

Bots do well on short, strict scripts and badly on long persuasion. By the third or fourth step of a rule-bound conversation a model starts losing the thread, and the customer feels they are being read a form. That is why selling and objections stay with people, and why the handover triggers above are deliberately simple

The bot earns its place by speed, not by eloquence. In small businesses leads often go to whoever replies first. Evenings, weekends and rush hours, when the receptionist is busy or gone, are exactly where a fast, accurate answer about price and free time turns into a booking. Trying to make the bot sell as well usually costs more customers than it wins

## Documents to prepare

| Document | Contents |
|---|---|
| Price list | Current prices and what each service includes |
| Service list | Short plain-language descriptions |
| Booking rules | Schedule, how far ahead, duration of each service |
| Location | Address, directions, parking |
| FAQ | Answers the receptionist gives every day |
| Handoff topics | Topics that always go to a person |

Starting point: list the ten most frequent questions from last month's messages and check which the documents answer. Fill the gaps before launch

![A shop owner taking an order by phone](https://images.pexels.com/photos/3932728/pexels-photo-3932728.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Handover specification

| Trigger | Action |
|---|---|
| Topic in the handoff list | Hand over immediately |
| Third clarifying question in a row | Hand over |
| No answer in the documents | Hand over; never improvise |
| Customer asks if they are talking to a bot | Answer honestly and offer a person |

Summary sent with every handover: who wrote, what they asked, where the conversation stopped. The customer must not have to repeat the question

## Channels

One core serves Instagram, WhatsApp and website chat. Documents and rules are written once; separate bots per channel drift apart and contradict each other

## Rollout

| Phase | Scope | Check |
|---|---|---|
| Test | Real messages from the inbox, offline | Answers match documents; handovers fire correctly |
| Launch 1 | Prices, slots, booking only | Read every conversation for a week |
| Launch 2 | Add reminders and rescheduling | Drop-off points reviewed |
| Ongoing | Add one scenario at a time | Each new scenario tested on real messages first |

![An irritated customer on a call](https://images.pexels.com/photos/6028572/pexels-photo-6028572.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Metrics

| Metric | Meaning |
|---|---|
| Bookings after bot conversations | The real result |
| Conversations outside working hours and their bookings | Where the bot adds the most |
| Handover reasons | Missing documents or unclear steps |
| Step where customers drop off | Script too long or unclear |

Not a success metric on its own: number of conversations

## Operational notes

Agree on how fast staff answer handed-over chats, including evenings and weekends; a handover nobody picks up is a lost customer. During the first weeks a receptionist reads all bot conversations and marks weak answers; each mark becomes an edit to the documents or rules. Give the bot a few real receptionist replies as a tone sample so it sounds like the business

More on AI receptionists is on the [AI administrator page](https://matintellect.com/en/services/ai-administrator)
