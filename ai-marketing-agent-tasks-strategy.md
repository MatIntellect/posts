# AI agents for marketing: a data quality checklist for briefing pipelines

This technical note is for developers designing an AI-assisted marketing briefing. Its goal is to keep incomplete metrics visible before a model summarizes them. It includes a small runnable Python example, checks to reproduce locally and the decisions that remain outside the model. It is not a production analytics connector or a complete agent implementation

![A navigator choosing direction in a fictional observatory](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-ai-marketing-agent-tasks-strategy-1794361467.jpg)

## Architecture and responsibilities

A useful boundary has four parts. A collector reads from an authorized source. Deterministic code validates the collected rows against the reporting period and data contract. The model receives values, provenance and explicit gaps, then drafts a summary. A person inspects the evidence and decides what to do

Data travels in one direction through those steps: source records become checked values, checked values become a draft, and the draft becomes an input to a human decision. A model-generated recommendation does not prove that the numbers are complete. A successful collection request does not prove that the metrics are comparable

In my team, the marketing agent's instructions assign analysis and recommendations to the agent while excluding final post writing and publication. That describes an intended role, not a measurement of each report's correctness. The local example below is independent of that production setup; it illustrates a single coverage check

## Prerequisites and input

Use Python with its standard library. I ran this exact example on Python 3.14.9. No API key, network connection or customer record is needed. The sample period is three fictional calendar days in January 2026. Each row carries an ISO date and a non-negative integer visit count

The contract allows one row for each date. A row containing zero is an explicit observation. A missing row is an unknown. A duplicate or out-of-range row is rejected rather than silently merged. These are choices for this example; a real source may require different aggregation or late-arriving corrections

![A laptop with charts and indicators](https://images.pexels.com/photos/577195/pexels-photo-577195.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Executable example

Save this as `check.py`, then run `python3 check.py`

```python
from datetime import date, timedelta

def summarize(start, end, rows):
    expected = set()
    day = start
    while day <= end:
        expected.add(day.isoformat())
        day += timedelta(days=1)
    found = {}
    for row in rows:
        day = row['day']
        count = row['visits']
        if day not in expected or day in found or type(count) is not int or count < 0:
            raise ValueError('invalid or duplicate row')
        found[day] = count
    missing = sorted(expected - found.keys())
    return {'total': sum(found.values()) if not missing else None, 'missing': missing}

if __name__ == '__main__':
    start, end = date(2026, 1, 1), date(2026, 1, 3)
    data = [{'day': '2026-01-01', 'visits': 3}, {'day': '2026-01-03', 'visits': 2}]
    print(summarize(start, end, data))
    data.append({'day': '2026-01-02', 'visits': 0})
    print(summarize(start, end, data))
    try:
        summarize(start, end, data + [data[0]])
    except ValueError as exc:
        print(type(exc).__name__ + ': ' + str(exc))
```

My local execution returned:

```text
{'total': None, 'missing': ['2026-01-02']}
{'total': 5, 'missing': []}
ValueError: invalid or duplicate row
```

The first result carries no complete total. The second supplies an explicit zero and can sum the period. The third rejects a duplicated day. A downstream summary should receive the missing list and any source error, not just a number that hides collection status

## Checks to add around a real source

Record the source, extraction time, reporting time zone, date range, metric definition and applied filters. Make sure the same definition is used for both comparison periods. A lead or inquiry may mean a form submission in one dataset and a conversation in another. Neither name guarantees the same business event

The function above does not validate reversed date ranges, check key presence gracefully or handle source-specific time zones. It rejects duplicates instead of resolving them. It does not connect to an API or test network failures. Add those cases deliberately before using the pattern in production

A source timeout should be represented separately from a successful empty response. Bounded retries for reads can address transient failures, but a request that changes an advertising budget or sends a message must not be blindly retried. First establish whether the previous write succeeded. The local example makes no external calls and performs no such action

## Review the conclusion, not only the count

A rise in visits or inquiries does not establish why it happened, whether the inquiries fit the business or whether sales followed. Those questions require further records and business context. A briefing can identify the need for that data without inventing the answer

The broader design of [AI agents for business](https://matintellect.com/en/services/ai-agents) includes specifying inputs, permitted actions and the point where a human remains responsible. For this example the only completed checks are the local Python run and its printed results above; no live analytics system was tested

![Two people review data at a laptop](https://images.pexels.com/photos/7693155/pexels-photo-7693155.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

Here is how it works in my own setup. A separate program collects 20 live questions people ask AI and 10 topics every morning, and the marketer agent adds what worked yesterday and suggests what to post today. Over three months that produced 80 daily briefs and 94 images, and I made the decision at every step: the agent never publishes or spends anything on its own

To reproduce, run the file, confirm the three output lines, then change the sample rows and observe whether a missing or duplicated day is visible. For a real deployment, add tests against the source's actual contract and verify permissions before connecting it
