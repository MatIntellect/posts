# AI assistant for business: role card template and readiness checklist

Type: specification template with a filled teaching example. Reader: a developer or operations lead scoping a first AI assistant for a small business. Goal: describe one assistant role precisely enough that it can be built, tested and handed over: input, rules, output, bad-data handling, boundaries and acceptance. Limits: the example is invented for illustration; the template is a teaching aid, not a tested configuration for a specific framework

![AI-generated illustration of creating an AI assistant for business](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-ai-assistant-for-business-clear-tasks-1791359987.jpg)

## Definition used here

An AI assistant for business is treated as an employee for one area. It has its own memory, skills and connected services and does one clearly defined job every day. Roles with clear input and checkable output (documents, numbers, payments, sorting incoming requests by rules) are preferred over roles where the right answer is a matter of taste

Reference system: my own assistant Jes has been running on my server for 134 days, runs 10 scheduled jobs and hands tasks to 7 other bots; since July she has passed on 165 tasks. Deleting data, spending money, messaging clients and publishing always wait for an explicit yes. A first assistant for one clear role took one to two weeks in my projects

## Role card template

| Field | Question it answers |
|---|---|
| Role | What does the assistant do, in one sentence |
| Trigger | When does it run: schedule, new file, new message |
| Input | Where data comes from and in what form |
| Reference data | What trusted source the input is compared with |
| Rules | Steps applied to the input, in order |
| Calculations | Which numbers are computed, and by code, not by the model |
| Output | What is produced and where it goes |
| Bad data | What happens when input is missing, unreadable or contradictory |
| Boundaries | What it does alone; what always needs a person |
| Acceptance | How a person decides the output is correct, and how often |
| Owner | Who reviews results during the first weeks |

If a field cannot be filled in, the role is not ready to build

## Filled example (teaching only)

| Field | Value |
|---|---|
| Role | Check every incoming supplier invoice before payment |
| Trigger | New invoice file in the shared inbox |
| Input | Invoice file |
| Reference data | Contract with the supplier: amount, bank account, payment terms |
| Rules | Extract supplier, amount, due date, account; compare with contract |
| Calculations | Amount difference computed by code with exact decimal arithmetic |
| Output | One row per invoice in a spreadsheet: status, issues |
| Bad data | Status "cannot check" with the reason and the file attached; never guess |
| Boundaries | Never pays, never writes to the supplier |
| Acceptance | Weekly: five random rows compared with the original invoices |
| Owner | Finance lead |

![Working with documents and a calculator](https://images.pexels.com/photos/33175651/pexels-photo-33175651.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Architecture split

| Part | Holds | Changes when |
|---|---|---|
| Memory | Stable context: rules, decisions, facts the role needs | A rule is corrected or added |
| Skills | How to perform the task step by step | The procedure changes |
| Services | Access to data and actions: mail, spreadsheets, accounting | A tool is added or removed |
| Calculator or code | All arithmetic and comparisons | A new check is introduced |

Keeping these apart avoids one huge instruction where a change in one place silently breaks another

## Readiness checklist

- [ ] Role card filled in, every field
- [ ] Reference data identified and trusted
- [ ] Arithmetic moved to code
- [ ] Bad-data scenario written and tested on a broken example
- [ ] Boundaries agreed with the owner
- [ ] Test run on typical documents and on deliberately wrong ones
- [ ] Acceptance owner named
- [ ] Same kind of mistake has stopped repeating for at least a few weeks before widening the role

![Checking financial spreadsheets](https://images.pexels.com/photos/7054415/pexels-photo-7054415.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Failure modes

| Symptom | Cause | Response |
|---|---|---|
| Correct-looking total that is wrong | Model did arithmetic | Move calculation to code |
| Invoices marked ok with missing fields | No bad-data scenario | Add cannot-check status |
| Endless tuning arguments | Role depends on taste | Pick a role with checkable output |
| Errors hard to trace | Several services connected at once | Connect one at a time |
| Assistant drifts into other tasks | Role widened without a new card | Write a new card or a separate helper |

More on assistants and AI employees is on the [AI employee page](https://matintellect.com/en/services/ai-employee)
