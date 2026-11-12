# Telegram bot development: workspace design with topics, bot roles and approval

Type: workspace design note. Reader: a developer or team lead moving team workflows into a Telegram group with AI bots. Goal: define topics, bot roles, who may instruct bots and which actions need a human yes. Limits: describes my own setup and general Telegram behaviour; check the current Bot API documentation for details

![AI-generated illustration of Telegram bot development with topics](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-telegram-bot-development-business-topics-1792808386.jpg)

## Reference workspace

A group called "Factory" with topics for ideas, posts, design, copywriting, marketing, video, publishing and an archive. A team of 8 AI agents works there, each in its own topic, and listens only to approved people. Separately, my personal agent Jes has run in Telegram for 134 days and delivers a morning plan as one message, 127 days in a row

| Topic | Bot role | Output |
|---|---|---|
| Marketing | Marketer | Morning brief from 20 live questions and 10 topics; 80 briefs in three months |
| Design | Designer | Image after approval of its description; 94 images |
| Ideas | Content factory | Topic cards with Interesting and Skip; 13 sources watched around the clock |
| Posts | Content factory | Previews; 84 posts published, none without approval |
| Video | Subtitle helper | Clip ready in about 2 minutes after one word |

## Why this layout

Topics organise conversation, but they do not do work. The value comes from pairing each topic with one bot that has one role and a clear output, so the team knows where to look and what to expect. Buttons turn decisions into a single tap in the place where the question arrived; in my own setup topics, post previews and image descriptions all reach me as cards. Voice notes matter more than they seem: an owner on the move can say a task instead of typing it, and the bot handles it like text

Approval is part of the layout, not an afterthought. Agents listen only to approved people, and anything that publishes, spends or deletes waits for a human yes. Without that, a busy group eventually produces a request that should never have been executed

Notifications need discipline. If every event becomes a message, people stop reading. Bots should post only what needs a reaction, plus at most one short daily summary

## Telegram building blocks

| Block | Use |
|---|---|
| Forum topics | One direction per thread; bots stay in their own |
| Inline buttons | Decisions in one tap: approve, rewrite, skip |
| Commands | Explicit triggers for a bot |
| Files, text, voice | Inputs; voice notes are transcribed and handled like text |
| Mini Apps | Own interface inside Telegram when cards are not enough |

![Working in a messenger](https://images.pexels.com/photos/4623475/pexels-photo-4623475.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Rules

Topics:
- named after work, not people
- one direction per topic
- split a topic when people get confused; delete one nobody uses

Bots:
- one role, one topic
- instructions only from approved people
- decisions arrive as cards with buttons
- publishing, spending and deleting only after a human yes
- messages only when someone must react, or one daily summary

## Rollout

| Step | Done when |
|---|---|
| Pick the most frequent team task | Task named in one sentence |
| Create group and first topic | Topic named after the work |
| Add one bot with one role | Bot answers only in its topic; approved senders set |
| Add buttons for decisions | Decisions take one tap |
| Connect the process behind the buttons | Tapping a button actually does the work |
| Add the next topic | First topic runs without attention |

![A team at work](https://images.pexels.com/photos/6669813/pexels-photo-6669813.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Telegram limitations

| Limitation | Consequence |
|---|---|
| Bot cannot message a user who never wrote to it | Customers must start the conversation |
| Bots in groups do not see all messages by default | Privacy setting must be changed for group bots |
| Customers live in other messengers | Team work and customer chat often run in different channels, connected by the system |

## Anti-patterns

- Ten topics and ten bots on day one
- Topics named after people
- Bots that accept instructions from anyone in the group
- Buttons with no process behind them
- Expecting customers to move to Telegram because the team likes it

A setup like this, with roles and approval rules, takes about 2–3 weeks. More on the [AI development page](https://matintellect.com/en/services/ai-development)
