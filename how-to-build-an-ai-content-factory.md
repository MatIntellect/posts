# Designing a human-approved content workflow

This note describes the components and checks in my Telegram-based content factory. It is an architecture walkthrough, not a ready-to-run implementation: channel configuration, credentials and a working Telegram account are required for a real deployment

## Components

- A private Telegram group with two work topics: ideas and posts
- A source reader using the owner's account to monitor selected channels
- A Python process that presents cards, handles buttons, passes jobs and saves state
- A model that researches, drafts and checks the text against the task
- A person who chooses the topic and approves or cancels publication

A channel instruction contains voice rules and examples. The writer receives the selected source, the channel's instruction and an optional author comment. This does not eliminate the need to review facts

## Handoff

1. The reader collects news, filters advertising and repeated items, and sends cards to the ideas topic. A person can also submit an idea manually
2. The person selects a card, destination channel and platforms, then chooses whether to add a comment
3. The Python process sends the task to the model. Each request has an identifier and the response ends with the same identifier, allowing the process to associate the response with its task
4. A draft arrives in the posts topic with actions for publication, rewrite, media replacement and cancellation
5. Only after approval does the main Telegram post go out. Drafts for other selected platforms are prepared with their own publication buttons

The identifier helps correlate messages; it does not validate the facts inside a response. Likewise, persisted state is not a substitute for checking the exact result of an external publication

## Check before relying on the workflow

Use one test idea and verify that the correct source and author comment reach the draft. Request a rewrite and check that the revised result returns to the correct task. Cancel another test and confirm it never becomes a published post. Finally, check the selected platform drafts and their configured lengths

My system uses configuration limits of 2,200 characters for Instagram, 500 for Threads and 280 for X by default; individual channels can override them. These are application settings rather than a statement of each platform's universal API limits

For the editorial side and the division between author and automation, see the [content factory walkthrough](https://matintellect.com/en/posts/how-to-build-an-ai-content-factory). Do not store credentials in an example repository or treat this description as tested deployment code
