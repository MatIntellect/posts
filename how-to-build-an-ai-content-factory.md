# Architecture note: a human-approved AI content factory

This repository-style note describes the content workflow documented in the Content Engine README and the request handoff in `llm.py`. It is an architecture description, not a deployment guide or a claim that the suggested checks have been run.

![AI content factory illustration featuring Mat](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-how-to-build-an-ai-content-factory-1794285443.jpg)

## Components and boundaries

- **Source intake:** the owner’s Telegram account reads channels listed in `sources.json`. Candidate news is filtered for advertising and repeats, then shown as cards in an Ideas topic. A person can submit an idea manually.
- **Workflow engine:** a Python process handles Telegram messages and buttons, routes tasks, keeps pending state and coordinates previews. It is not the text-generating model.
- **AI writer:** a separate Claude Code instance with a Telegram plugin, called the “brain bot” in the README. It receives task files and returns text. Channel instructions and examples specify the writing voice.
- **Human operator:** chooses whether a source is worth using, selects channel/platforms, optionally adds an author comment, and decides whether to publish a preview.
- **Publishers:** Telegram is the main post destination. Separate drafts are prepared for selected social platforms; a site row depends on a Telegram post URL.

The AI’s role is specific: research, draft and check text within the workflow. The program supplies the process around that role. A generated draft is not an editorial approval.

## End-to-end flow

```text
Telegram sources ──> candidate cards ──> human selects idea + channel + destinations
                                               │ optional author comment
                                               v
                                      Content Engine sends task
                                               │ .txt + request envelope
                                               v
                                         AI writer bot
                                               │ response + request marker
                                               v
                                  preview in Posts topic
                                   /      |       |      \
                              rewrite  media   cancel   publish
                                                        │
                                                        v
                                              Telegram master post
                                                        │
                                           separate platform drafts
```

## Request/reply protocol

The engine’s one model-call path is in `llm.py`. It sends a text file whose first line contains `request_id`, `stage` and `schema_version`. The writer is instructed to end with `[END:<request_id>]`.

The reply listener buffers messages from the configured writer account and joins likely fragments. A matching end marker resolves the waiting task immediately. If a message with the request ID arrives but no terminator follows, a 15-second timer starts. Another message containing that ID resets the timer; a fragment without the ID does not. That fallback prevents an omitted marker from leaving a request waiting indefinitely; silence does not prove the answer is complete.

Calls are single-flight. An `asyncio.Lock` covers sending the file and waiting for the response, so another model call through this function cannot overlap that interval. This simplifies message correlation at the cost of making queued calls wait behind a slow response. The function’s normal timeout is 600 seconds, followed by a 60-second grace period for a late reply. Errors are returned as an empty `LLMReply` with an error label; the code does not switch to a different model path.

A request ID and end marker establish protocol structure, not trust. They cannot replace fact checking, editorial review, access controls or verification of an external publication.

![People working at a computer. Photo: Pavel Danilyuk, Pexels](https://images.pexels.com/photos/7675029/pexels-photo-7675029.jpeg?auto=compress&cs=tinysrgb&w=1400)

## Approval and channel-specific output

A preview appears in the Posts topic with controls to publish, mark as a reference, rewrite, replace media or cancel. The README’s rule is clear: without a person pressing the button, nothing is published.

After the main Telegram post is approved, drafts for other selected platforms are prepared separately, each with its own publishing button. `platforms.py` centralizes platform order, labels, defaults, text limits and the rule that site publishing requires Telegram selection. Some platforms are opt-in by channel; a channel can override text limit and language. Table defaults include Instagram 2,200 characters, Threads 500 and X 280. They describe this application’s configured limits, not universal guarantees from those services.

The separation matters operationally: generating a shorter caption is a new draft, not proof that meaning survived compression. A destination-specific draft still needs a person’s decision.

## Suggested acceptance checks (not executed here)

1. Submit a distinguishable idea and verify the selected source and optional author comment appear in the intended task.
2. Exercise the request protocol with an immediate matching marker, split marker, omitted marker followed by silence, and delayed response. Confirm each branch resolves the intended request.
3. Request a rewrite and verify that it returns to preview rather than publishing.
4. Cancel a preview and confirm it does not proceed to publication.
5. Approve a test post only in a safe environment, then inspect the exact external result and platform-specific drafts.
6. Test group membership and button permissions. The README warns that any participant in the private forum can press its buttons.

![Video editing workspace. Photo: Ron Lach, Pexels](https://images.pexels.com/photos/8102675/pexels-photo-8102675.jpeg?auto=compress&cs=tinysrgb&w=1400)

These checks are recommendations, not reported results. No execution tests are claimed in this document.

For a broader explanation of the design and its editorial boundaries, see the [AI content factory walkthrough](https://matintellect.com/en/posts/how-to-build-an-ai-content-factory). Keep credentials out of example documentation and repositories; the README treats platform credentials as separate configuration inputs.
