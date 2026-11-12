# AI in sales: lead tracking schema and staged rollout plan

Type: data schema and rollout plan. Reader: a developer or sales operations lead introducing AI into a small sales team. Goal: define the lead record and the order of automation so every later step, including a customer-facing chatbot, can be measured by what happens to leads. Limits: the schema and plan are teaching material, not a tested configuration for a specific CRM

![AI-generated illustration of AI in sales](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-ai-in-sales-where-to-start-1792468371.jpg)

## Principle

AI gives the most in sales where input and output are clear and the step is short. Full conversations with customers have too many branches to hand over at the start; strict repetitive steps do not. The plan therefore automates recording and follow-up first and customer replies last

Reference: my own setup records website requests as Telegram cards and turns each client call into a summary, tasks with dates and an updated CRM card; about 40 calls with 15 clients have gone through it. A clinic chatbot I built answers only from the clinic's documents, about 114 price items and 48 services, and passes anything else to the owner. Launching tracking, calls, CRM and reminders takes about 2–3 weeks

## Lead record

| Field | Type | Filled by | Notes |
|---|---|---|---|
| id | string | system | Unique per lead |
| created_at | datetime | system | One time zone for all records |
| source | enum: web_form, messenger, phone, social, other | AI step | From the channel the lead arrived in |
| request | short text | AI step | What the customer wants, one line |
| owner | person | rule or human | Every open lead has one |
| step | enum: new, in_progress, waiting_client, booked, paid, lost | AI step or human | Fixed list, no free text |
| next_action | date | AI step or human | Mandatory for open leads |
| lost_reason | enum or short text | human | Filled when step becomes lost |
| history | links | system | Messages, call summaries |

## Rollout stages

| Stage | AI does | Humans keep | Exit check |
|---|---|---|---|
| 1. Tracking | Creates a record for every lead, fills source and request, reminds when next_action passes | Replies, prices, decisions | Weekly count in tracking matches leads in all channels |
| 2. Calls | Transcribes, summarises, extracts tasks with dates, updates the lead | The conversation and its decisions | Sample summaries match the recordings |
| 3. Follow-up | Morning plan, reminders, list of silent leads | What to do with each reminder | No overdue lead older than a set limit |
| 4. Replies | Answers typical questions from approved documents, books when allowed | Discounts, deadlines, complaints, anything not in documents | Booked or paid rate per source does not drop after launch |

![Working with incoming requests](https://images.pexels.com/photos/37568245/pexels-photo-37568245.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Metrics

| Metric | Source | Why |
|---|---|---|
| Leads per source per week | tracking | Baseline for everything else |
| Share reaching booked or paid, per source | tracking | Real outcome, not activity |
| Overdue open leads | tracking | Where follow-up fails |
| Top lost reasons | tracking | Decides the next automation |
| Time to first reply, per source | tracking plus history | Only meaningful next to conversion |

Number of chatbot messages and reply speed alone are not success metrics

## Failure modes

| Symptom | Cause | Response |
|---|---|---|
| Bot replies but bookings do not grow | Bot launched without tracking | Add stage 1, measure per source |
| Leads from one channel never appear | Channel not connected | Count leads per channel manually for a week and compare |
| Many open leads without next action | Field optional | Make it mandatory for open leads |
| Bot promised a discount | Boundaries not enforced | Discounts and deadlines only through a person |
| Each manager uses own statuses | No fixed step list | Agree on steps before automating |

![Talking to a customer](https://images.pexels.com/photos/8867190/pexels-photo-8867190.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Data handling

Call recordings, chats and lead cards are personal data. Decide before launch where they are stored, who can read them and what the AI step may do with them. In my own setup call audio is transcribed locally, so client audio never leaves my machine

## Checklist before stage 4

- [ ] Every channel feeds tracking
- [ ] Per-source conversion known for several weeks
- [ ] Approved documents the bot may answer from
- [ ] List of topics that always go to a person
- [ ] Someone reads live conversations during the first weeks

More on AI employees for sales and operations is on the [AI employee page](https://matintellect.com/en/services/ai-employee)
