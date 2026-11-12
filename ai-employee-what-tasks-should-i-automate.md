# AI employee task boundaries: a practical review checklist

This note is for someone designing a content workflow with an AI employee. The goal is to make each stage inspectable before allowing an external action. It describes boundaries and checks, not a complete implementation or a benchmark

![Gradual delegation to an AI employee](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-ai-employee-what-tasks-should-i-automate-1794451323.jpg)

My content factory is a team of AI agents operating in Telegram. It receives material from 13 news sources, removes duplicates, highlights topics, prepares posts in the author's voice, checks facts and adds an image. A preview goes to me; publication requires my approval

The point of describing these stages is not that every system needs this exact arrangement. It is that the output of one stage becomes the input of another. When a result is wrong, the designer needs to know which boundary to inspect

## 1. Input: preserve the source

A source item should remain identifiable to the person reviewing a resulting claim. If the draft says that an event happened, the reviewer needs to find the material on which that sentence was based. A source reference is useful only if it points to material that supports the specific statement

For a proposed test, select a few items with known content. Include one with a missing number. Ask the system to prepare its normal output, then check whether it reports the absence or fills in a plausible value. This is a test design, not a claim about a completed run

If an item was never received, a downstream model cannot be expected to recover it from the defined input. Diagnose the input boundary before adjusting writing instructions. In a production system, an unavailable source and an empty result should be distinguishable to the reviewer; otherwise an absence of data can look like an absence of news

![Reviewing source notes](https://images.pexels.com/photos/6170173/pexels-photo-6170173.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## 2. Filtering: inspect both sides

The factory removes repeated news. This is a separate decision from writing a post. Two headlines may describe the same event, but similar language does not prove that two events are identical

A useful proposed test has two pairs: one event reported with different wording, and two distinct events with similar wording. Inspect both retained and rejected items. The first pair checks whether repetition survives; the second checks whether a valid item disappears. Keep the source material available for the review

If a rule changes to fix one pair, rerun both. A test that only checks the original failure can miss a regression. The expected result is a set of distinct items with source evidence available, not a guarantee that an AI classifier will be correct on every new item

## 3. Draft: separate voice from factual support

The factory prepares text in the author's voice and checks facts against sources. Voice and accuracy are separate properties. A sentence can sound natural and still change the meaning of its source. A well-supported sentence can still be unsuitable for the author's style

Review numbers, names and whether statements preserve the status of the underlying information. A plan is not a completed event; a forecast is not an observed result. When the result is wrong, correct the relevant stage rather than issuing a generic instruction to improve everything

The factory also adds an image. A useful image review asks whether the visual corresponds to the material and whether it can be used. These are editorial checks; generating an image is not proof that it is appropriate

## 4. Approval: distinguish prepared from authorized

In my workflow, I receive a preview and can ask for changes. A post goes out only after my yes. Across 84 published posts, none went out without my approval. The approval boundary is the difference between presenting a draft to an operator and taking an action that readers will see

Design the handoff so the reviewer can see the actual text and image to be released. If the input is incomplete or a claim cannot be supported, a safe outcome is to stop for correction. A prepared draft is not an authorization, and a missing approval is not the same state as a rejection

This distinction matters when the system is extended. New capabilities should not silently inherit permission to act externally. For a different application, define the corresponding boundary: preparing an answer is distinct from sending it, and presenting a financial calculation is distinct from authorizing a payment

![Review of a draft by people](https://images.pexels.com/photos/5313151/pexels-photo-5313151.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## 5. Corrections and regression

Since October 28, the factory has compared my edits with channel rules and added to them to avoid repeating mistakes. A rule is useful only insofar as later results can still be checked. It does not prove that future drafts are correct or remove the approval step

A practical review record can contain the source, the incorrect output, the desired correction and a case that should continue to work. Do not publish real private material when creating such an example. Run the new check after a change and review earlier cases as well. This is a recommended method, not a claim that a specific automated test suite has run here

In my process, preparation that took around an hour now takes roughly 5 minutes to a finished preview. That number is tied to this workflow; it does not establish performance for another implementation. The operational question remains whether each result can be examined before the next stage

My [article on delegating tasks to an AI employee](https://matintellect.com/en/posts/ai-employee-what-tasks-should-i-automate) gives the broader context. For an implementation, start with one bounded input and one observable output. Add the next stage only when the earlier one can be checked, and keep the person responsible for the external decision explicit
