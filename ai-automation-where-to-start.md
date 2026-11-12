# AI automation: a worksheet for choosing and specifying the first task

Type: worksheet and specification template. Reader: a founder, operations lead or developer about to start AI automation in a small business. Goal: pick a first task that can be verified, describe it precisely enough to build, and decide whether existing agents need an audit first. Limits: this is a planning template in prose; it ships no code or configuration, and the example entries are teaching material, not a tested specification

![AI-generated illustration of AI automation and where to start](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-ai-automation-where-to-start-1791966730.jpg)

## Reference setup

The worksheet follows the structure of my own automation. Verified facts, as published on my project page:

- a morning message with the plan for the day, assembled from calendar, tasks and reminders, has arrived for 127 days in a row
- reminders are checked every 5 minutes; the system has sent 240 reminders
- a 57-minute call recording becomes a transcript in about 10 minutes, with summary, tasks and a CRM client card in the same pass
- about 40 calls with 15 clients have gone through the system
- building a setup like this takes about 2–3 weeks

The simple pieces came first and the call processing was added on top of them

## Principle

Start with the task that takes the most time among those with a clear input, a clear output and a result that can be checked at a glance. Exciting tasks with fuzzy results come later

## Step 1. Time log

Record one working week to the nearest hour. Log small tasks too; they add up

## Step 2. Filters

A task qualifies only if all three hold:

| Filter | Question | Fails when |
|---|---|---|
| Explainable | Could a new employee learn it in five minutes? | The explanation ends with "it depends" |
| Checkable | Can one result be verified at a glance? | Checking takes as long as doing |
| Defined | Are input and output both clear? | Data comes from unknown places or the output is vague |

Among qualifying tasks, choose the one with the most minutes per week

## Step 3. Task specification

| Field | Content |
|---|---|
| Input | Every source the data comes from |
| Output | What exactly is produced, with two or three criteria for "important" if relevant |
| Check | How a person verifies one result in under a minute |
| Frequency | How often the task runs |
| Current cost | Minutes per week spent today |
| Source health | Is the source in order now, or are items already being lost |

## Example specifications (teaching material)

| Task | Input | Output | Check |
|---|---|---|---|
| Email triage | Messages in the inbox | List of messages that need attention | Nothing important missing from the list |
| Calls and meetings | What is planned and when | Calendar entry | Date and time match the agreement |
| Daily task list | Tasks from all sources | One list | Every source item appears |
| Incoming requests | The requests themselves | List of processed requests | Count of requests equals count of entries |

The same template applies to harder tasks. For call processing in the reference setup: input is the recording; output is transcript, summary, tasks and client card; check is that the tasks match what was agreed on the call

![Email on a laptop next to a paper planner](https://images.pexels.com/photos/14465804/pexels-photo-14465804.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Step 4. Validate on real data

Run the automation on real messages, requests and meetings, compare with what you would have done by hand, and record each mismatch against a field of the specification

| Mismatch | Likely field | Fix |
|---|---|---|
| Items missing | Input | List every source, not only the main one |
| Wrong items flagged | Output | Add explicit criteria |
| Items lost before automation sees them | Source health | Consolidate the source first |
| Same error after two fixes | Filter | Task does not pass "explainable"; defer it |

## When agents already exist

If there are half-finished agents that keep failing, the first step is an audit without changes:

- what works and what is broken
- where the keys are stored and who has access
- what spends money and how much
- which parts are worth finishing and which are simpler to rebuild

No new task is added until this inventory exists

## Common mistakes

- choosing the most interesting task instead of the most expensive one
- choosing by feeling without a time log
- leaving the Check field empty
- automating a source that already loses items
- starting several tasks at once and finishing none

## Real limits

- first results look modest; the payoff comes when several simple pieces connect
- the filter thresholds are judgement and should be written down, not assumed
- a task that is cheap in time but error-prone may deserve attention first; the worksheet does not capture that on its own

![Working through a task list on a laptop](https://images.pexels.com/photos/7439136/pexels-photo-7439136.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Exit criteria for the first task

- the specification has all six fields filled in
- validation on real data shows no repeated mismatch
- weekly minutes, including checking, are clearly lower than the current cost
- the owner has stopped thinking about the task day to day

More on how this kind of review is run for a business is on the [AI audit service page](https://matintellect.com/en/services/ai-audit) of my site
