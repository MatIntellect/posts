# Business process audit before AI: data inventory template

Type: audit template. Reader: an owner, operations lead or consultant preparing a business for AI. Goal: inventory which data is already collected, find what is missing or cannot be linked, and turn the findings into a short, checkable list. Limits: a planning template in prose and tables; it ships no code or configuration, and the example fields are teaching material

![AI-generated illustration of a business process audit before AI](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-business-process-audit-before-ai-1794010880.jpg)

## Reference setup

Verified facts, as published on my project pages, from my own business where the data is already collected in one place:

- every client call becomes a transcript, a summary, tasks and a CRM card; a 57-minute call is processed in about 10 minutes
- about 40 calls with 15 clients have gone through the system
- a daily plan is assembled each morning from calendar, tasks and reminders, 127 days in a row
- a marketing agent collects 20 live questions people ask AI and 10 topics each morning
- long client calls are transcribed on my own computer, so clients' voices do not leave it

## Principle

During the audit, change nothing. First give AI access so it can start counting and building a record. Decide on changes once the data shows where time, resources and clients are lost. AI cannot reconstruct events that were never recorded

## Inventory table

Fill in one row per area

| Area | Questions | Typical finding |
|---|---|---|
| Customer path | Where does a request appear, who receives it, what happens next, where is the result recorded? | Requests live only in employees' personal chats |
| Time and resources | Which tasks repeat, how long they take, what they cost | Hours spent on work that appears in no record |
| Money and source | Are payments visible, is each paying client's source recorded? | Payments visible, source missing; channels cannot be compared |
| Storage and links | Which systems hold data, is there a shared field such as the client contact? | Records exist but cannot be joined |
| Access and rights | Which data the task needs, who can see it, may it be passed to the chosen service? | Access wider than the task requires |
| Existing agents | What works, what is broken, where the keys are, what spends money | Agents that look alive but do no work |

## Checks per area

| Area | Check |
|---|---|
| Customer path | From records alone, count last week's requests and how many were answered |
| Time and resources | Have each person log repeated work by the hour for a week and compare with expectations |
| Money and source | For the last ten payments, find the client's source in records |
| Storage and links | Reconstruct one recent paying client's path end to end from records only |
| Access and rights | For each connection, write one line: what it sees and why |
| Existing agents | Inspect without changes; list working, broken, keys, spend |

![Data and charts on a laptop screen](https://images.pexels.com/photos/577210/pexels-photo-577210.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Recording template for one process (teaching example)

| Field | Example values |
|---|---|
| Received at | Date and time |
| Channel | Site, messenger, call, comment |
| Received by | Person or bot |
| First reply at | Date and time |
| Next step | Booking, invoice, refusal, silence |
| Outcome | Paid, lost, pending |

Keep it to six or seven fields and record every day. After a couple of weeks it shows where requests stall longest and why

## Choosing the first process

- prefer a process that directly affects money or clients: requests, bookings, payments
- avoid processes where the result cannot be defined
- one process at a time

## Existing AI systems

If agents already exist but are unfinished or failing, the audit starts the same way: inspection without changes. Only then is it clear what to finish and what to rebuild. Finishing such a system takes 1–2 weeks depending on its size

## Output format

| Item | Content |
|---|---|
| Collected | Data already recorded and linkable |
| Missing | Data to start recording |
| Losses | Where clients, time or money are lost |
| Start with | The first process to change |
| Check in a month | How each item will be verified |

An item without a check is a wish, not a finding

![Work documents and data on a desk](https://images.pexels.com/photos/95916/pexels-photo-95916.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Common mistakes

- changing processes before they are recorded
- connecting AI to everything instead of the data for one task
- treating gaps as audit failure instead of findings
- expecting AI to recover unrecorded events
- delivering a presentation instead of a checkable list

More on how this audit is run is on the [AI audit service page](https://matintellect.com/en/services/ai-audit) of my site
