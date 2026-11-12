# AI content creation: content factory pipeline with author approval

Type: pipeline description and design worksheet. Reader: a developer or marketer planning an AI-assisted content pipeline for several social platforms. Goal: lay out the stages from topic discovery to multi-platform publishing, with the author's decision kept as an explicit step. Limits: describes the structure of a working setup in prose and tables; it does not ship runnable code, and the worksheet is a teaching template

![AI-generated illustration of AI content creation](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-why-do-you-need-an-ai-content-factory-1791429378.jpg)

## Reference system

My own content factory, as described on its project page: 13 sources watched around the clock, topics delivered as Telegram cards, facts checked before drafting, posts written in my voice per platform, a preview before publishing. About an hour of manual work per post became about 5 minutes to a ready preview. 84 posts published, none without my approval. Building one, including connecting the platforms, takes about a week

## Why not full automation

Readers notice AI-written text; in my experience it gets fewer views and weaker reactions. Only the author knows what happened in their work this week. The pipeline therefore automates preparation and keeps choice and approval with the author

## Stages

| Stage | Input | Output | Who decides |
|---|---|---|---|
| 1. Monitoring | Watched sources | Deduplicated topic list with the strongest flagged | Machine |
| 2. Selection | Topic card | Chosen topic, target platforms, optional voice comment | Author |
| 3. Research | Topic | Source texts with links | Machine |
| 4. Fact check | Topic and sources | Confirmed or rejected claims: names, numbers, dates, quotes | Machine, blocks on failure |
| 5. Drafting | Sources, style description, sample posts, past edits | One draft per platform and language | Machine |
| 6. Preview | Drafts | Post exactly as followers will see it, with publish, rewrite and own-picture buttons | Author |
| 7. Publishing | Approved versions | Posts on each platform | Machine, only after approval |
| 8. Learning | Author's edits | Updated rules for the next drafts | Machine |

![Planning content](https://images.pexels.com/photos/6016365/pexels-photo-6016365.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Platform versions

| Platform | Languages | Approval |
|---|---|---|
| Telegram | Russian and English | Separate |
| Website | Russian and English | Separate |
| Facebook, Instagram, Threads, YouTube | Own version each | Separate |

Versions are written as separate texts for each audience, not translated or copied

## Style memory per channel

| Item | Purpose |
|---|---|
| Style description | Sentence length, tone, words to use and avoid |
| Sample posts | The author's best posts for that channel |
| Past edits | Every correction, so the same edit is not needed twice |

## Implementation notes

Interface first. The whole loop runs in one chat: topic cards, voice comments, previews and approval buttons. The author never opens each platform separately, which is where most of the saved time comes from

Fact check before drafting, not after. Checking a finished draft tempts the reviewer to accept small errors because the text already reads well. Checking claims against sources first means a draft with an unsupported figure is never written at all

Learning from edits is the long-term lever. A pipeline without it produces the same mistakes every day, and the author stops using it within weeks. With it, each correction reduces future rewriting

Pictures are part of the post. The preview offers a button to replace the generated picture with the author's own photo or screenshot, which often works better than any illustration

Start small. If building everything at once is too much, automate the stage that costs the most time first, usually research or rewriting for each platform, and add the rest once that stage runs without attention

## Failure modes

| Failure | Guard |
|---|---|
| Invented number or quote | Fact check against gathered sources before drafting |
| Same text on every platform | One draft per platform from its own style memory |
| Author's voice drifts | Edits saved and applied to later drafts |
| Post goes out unseen | Publishing only from an approved preview |
| Topic list mistaken for a plan | Topics are suggestions; selection is a human step |

![Discussing social media](https://images.pexels.com/photos/7970812/pexels-photo-7970812.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Design worksheet (teaching template)

- Platforms and languages:
- Sources to watch:
- How topics reach the author:
- What counts as a checkable claim:
- Style description per platform written: yes / no
- Sample posts per platform collected: yes / no
- Where edits are stored:
- Who approves each platform version:
- Rules for pictures (own photos, generated images, what is not allowed):

More on content factories is on the [content factory page](https://matintellect.com/en/services/content-factory)
