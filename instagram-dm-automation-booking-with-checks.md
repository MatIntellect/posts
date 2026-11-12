# Instagram DM automation: booking bot architecture with code checks and human confirmation

Type: architecture note and rules template. Reader: a developer building an AI receptionist that books clients through Instagram Direct. Goal: separate the conversational model, the code that owns exact data, the rule checker and the human who confirms, and define what each may do. Limits: describes the structure in prose and tables; the rules template is teaching material, not a tested configuration

![AI-generated illustration of Instagram DM automation with checks](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-instagram-dm-automation-booking-with-checks-1792717872.jpg)

## Reference system

An AI receptionist I built for a clinic in Instagram Direct answers only from the clinic's documents, about 114 price items and 48 services. Prices come from the price list, not model memory; anything not in the documents goes to the owner as a card. A completed conversation goes to the doctor as a Telegram card, and the booking exists only after the doctor confirms. Built and tested on real questions from the clinic's inbox; about 2–3 weeks to build including testing

## Participants

| Participant | Responsibility | Must not |
|---|---|---|
| Conversation model | Understands free-form questions, voice notes, follow-ups; drafts replies | State prices or times it did not receive from code |
| Data code | Price lookup, free slots, nearest options from the calendar | Guess; returns nothing if data is missing |
| Rule checker (second model) | Checks each draft against the rules set before launch | Be the same model that wrote the draft |
| Human (doctor or receptionist) | Confirms bookings; answers handed-over questions | |

## Message flow

1. Message arrives in Direct (text or voice)
2. Conversation model identifies what is needed: price, slot, address, other
3. Data code returns exact values or nothing
4. Conversation model drafts a reply using only returned values
5. Rule checker approves or stops the draft; stopped drafts become handovers
6. When name, service and time are collected, a card goes to the doctor in Telegram
7. Doctor confirms; the customer receives the booking

![Discussing an appointment](https://images.pexels.com/photos/6809657/pexels-photo-6809657.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Rules template (teaching)

| Rule | Setting |
|---|---|
| First message | States it is an AI assistant and can call a receptionist |
| Topics allowed | Prices, services, free time, address, visit preparation |
| Topics forbidden | Contraindications, diagnoses, discounts, competitor comparison |
| Price source | Price list only |
| Time source | Calendar only |
| Missing answer | Hand over as a card, never improvise |
| Booking authority | Doctor or receptionist confirms |

## Failure modes

| Failure | Mitigation |
|---|---|
| Voice note transcribed wrongly | Test on real voice notes; ask again when meaning is unclear |
| Several questions in one message | Split into questions before drafting; check each is answered |
| Service named in customer's words | Model maps words to a price list entry; code checks it |
| Plausible but wrong price in draft | Checker rejects any number code did not return |
| Rule broken by a clever question | Second model stops the draft; question goes to a person |
| Frequent handovers | Missing content in documents; extend documents, not rules |

![Phone and planner for bookings](https://images.pexels.com/photos/714700/pexels-photo-714700.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Testing notes

Test on real messages from the inbox rather than invented ones. In Direct people send voice notes, make typos, ask three things at once and return to a price a day later; invented tests miss all of that. Real messages show where the model is too loose and where code is too strict and blocks a normal conversation

## Channels

The same core serves Instagram Direct, WhatsApp and website chat. Price list, rules and handover are configured once, so prices cannot differ between channels

## Launch readiness

- On real inbox messages, no price or time appears that is not in the price list or calendar
- The checker stops every draft that breaks a rule in the test set
- Handover reasons are understandable and few
- Doctor cards contain enough to book without reading the chat

## Why separate participants

One model could talk, count and check itself, but then the same model writes an answer and judges it, and its own mistakes pass. Separating roles costs a little more setup and means each class of error is caught by the participant responsible for it

More on AI receptionists is on the [AI administrator page](https://matintellect.com/en/services/ai-administrator)
