# AI implementation: a loss-first audit template for small businesses

Type: audit template and decision guide. Reader: an owner, operations lead or consultant preparing an AI implementation. Goal: find where the business loses money, time and customers, price the biggest loss and choose the first automation from it. Limits: this is a planning template in prose and tables; it ships no code or configuration, and the worked numbers are teaching material, not data from a client

![AI-generated illustration of AI implementation starting with lost revenue](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-ai-implementation-start-with-lost-revenue-1793066785.jpg)

## Reference case

Verified facts, as published on my project pages:

- a clinic was losing customers after its ads because incoming requests were not processed quickly; the audit started with those requests
- a reception bot was then built that answers instantly in every channel, takes clients to a booking and reserves time in the clinic's calendar
- the clinic now runs a team of 6 agents on the owner's own server; the client chatbot covers about 114 price items and 48 services and answers only from the clinic's documents, sending anything else to the owner as a card
- my own requests run the same way: about 40 calls with 15 clients have gone through the system, each with a visible step
- a bot that answers from documents and takes people to a booking takes about 2–3 weeks to build, including testing on real client questions

## Principle

AI mostly helps a business scale. Scale what works, after closing the places where results leak. Start every implementation by asking where the business loses the most money, time and customers

## Step 1. Map the customer path

| Step | Typical source of the count |
|---|---|
| Request | Messages in all channels, call log |
| First reply | Conversation timestamps |
| Booking or order | Calendar, order system |
| Visit or delivery | Attendance marks, delivery records |
| Payment | Payment records |

## Step 2. Count one ordinary week

Record the number of people at each step, from real records, not memory. Then note the time from first message to first reply for ten recent conversations, including nights and weekends

## Step 3. List ownerless places

Write down every place where requests can sit without anyone responsible: personal inboxes, an employee's private messages, comments under posts, a second messenger

![A team reviewing work documents](https://images.pexels.com/photos/7653571/pexels-photo-7653571.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Step 4. Price the biggest drop

| Input | Meaning |
|---|---|
| People lost at the step | Count before minus count after |
| Share who pay after passing the step | Payments divided by people who passed |
| Average order | From payment records |
| Monthly loss | People lost × share × average order × 4 |

Worked example (teaching numbers): 50 requests, 28 replied, 15 paid, average order 120. Loss at the reply step is 22 people; the share who pay after a reply is 15 of 28; the monthly loss is about 5657

## Step 5. Choose the cheapest fix for the symptom

| Symptom | First automation |
|---|---|
| Replies take hours | Instant first reply and contact capture |
| Requests lost between channels | One inbox for all channels |
| Bookings do not show up | Reminders and confirmations |
| Replies do not lead to bookings | Assistant that answers from documents and books time |
| People visit but do not return | Not an automation problem first; review service and price |
| Few requests at all | Not an automation problem; look before the first contact |

## Step 6. Re-measure

Repeat steps 2 and 4 on an ordinary week a month after launch. The implementation worked if the chosen drop shrank. If it did not, the leak was elsewhere or the fix addressed the wrong symptom

## Rules for the build

- answers come from the business's own documents; anything not covered goes to a person
- every request gets an owner and a visible step
- people stay in the process for decisions and difficult conversations
- the owner steps in only where a person is needed

## Common mistakes

- starting with a task that affects neither money nor customers
- counting from memory instead of records
- choosing the solution before finding the biggest drop
- a bot that answers from general knowledge instead of the business's documents
- skipping the second measurement

![Employees working at computers](https://images.pexels.com/photos/7654133/pexels-photo-7654133.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Audit checklist

- customer path written down
- one week counted at every step
- first reply time measured, including nights and weekends
- ownerless places listed
- biggest drop priced per month
- first fix chosen from the symptom table
- re-measurement date set

More on how this audit is run for a business is on the [AI audit service page](https://matintellect.com/en/services/ai-audit) of my site
