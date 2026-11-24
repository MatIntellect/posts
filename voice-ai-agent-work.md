# Voice AI agent: test the tool call before you build the voice app

Engineering lab for developers who already have a report, a status endpoint, or another read-only task and want to put voice in front of it. You'll test what happens when the model asks for data and the data is missing, stale, or outside its permissions. You'll need Python 3.12 to run the lab. It uses fake data in memory and leaves out the microphone, model, and network, so passing it tells you nothing about speech accuracy or latency.

![Mat on the cover of the voice AI agent article](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-voice-ai-agent-work-1795490179.jpg)

Jump to [architecture](#where-the-model-stops), [data flow](#trace-one-request), [the Python lab](#run-the-tool-contract-locally), or [the build decision](#decide-whether-to-build).

## Where the model stops

Take a question like "What did the analyst find this morning?" A speech recognizer can turn that into text, and the model can map it to a request for the morning report. The answer depends on what the reporting system actually produced. The model has no way to tell from the question alone whether today's report exists.

```text
[Mic] > [Speech recognizer] > [Model] > [Reply renderer] > [Speaker]
                                 |             ^
                           Proposed call       | Structured result
                                 v             |
                           [Tool gateway] -----+
                                 |
                         Authorized read only
                                 v
                           [Report store]
```

The gateway is application code. It checks which operation is allowed for the signed-in user, validates the arguments, then calls the backend. In this example the model can ask for a dated report. It gets no ability to choose a file path or run a command. The user identity comes from the application session, never from what the model thinks it heard.

In my AI Agent Team project, the analyst scans five industry chats every morning and returns 20 live questions and 10 topics. Those are counts from the analyst's roundup. They tell you what a voice interface could read, not how well it understands speech. For a first pass, you could make the spoken reply a short summary and put the full report on screen. If you want to hear the third question again, the app can use the same report rather than fetch a newer one halfway through the conversation.

![Microphone, laptop and headphones on a podcast desk](https://images.pexels.com/photos/37033702/pexels-photo-37033702.jpeg?auto=compress&cs=tinysrgb&w=1260)

This drawing uses a speech-to-text, model, and text-to-speech chain. You can swap in a model that handles audio directly. The [OpenAI voice agent guide](https://platform.openai.com/docs/guides/voice-agents) describes both setups. Either way, keep the permission check at the point where the real read happens. Changing the audio stack shouldn't change who can read a report.

## Trace one request

"This morning" only makes sense relative to a date and a time zone. Choose which time zone defines the report day in the application. If two interpretations are plausible, ask which day the user means before doing the read. Keep the report date in the result. A timestamp on the request tells you when someone asked; it doesn't tell you how current the data is.

```text
Input       "What did the analyst find this morning?"
Intent      Read the roundup for the application's report day
Tool call   read_roundup(day = resolved date)
Tool result status = ok, as_of = report date, counts = backend data
Output      Speak a short summary and show the dated report reference
```

If the recognizer is still sending partial text, display it if useful and wait for the end of the turn before dispatching the tool. A pause in "read Tuesday's report ... sorry, Wednesday's" is enough to make the first date look final. After dispatch, attach a turn ID to the call. If the user interrupts and asks for a different day, suppress playback from the old turn when its result arrives. Canceling audio doesn't guarantee the backend request stopped.

## Run the tool contract locally

Save the Python block below as `voice_lab.py` in an empty directory and run `python3 -I -B voice_lab.py` with Python 3.12.3. The script uses only the standard library. It doesn't open files, start other processes, or use a network connection. The calls stand in for validated requests from a voice session; there is no live assistant and no borrowed code.

```python
from datetime import date
REPORT_DAY = date(2026, 1, 9)
FIXTURE = {"as_of": date(2026, 1, 9), "items": 3}
STALE = {"as_of": date(2026, 1, 8), "items": 3}
def reply(operation, allowed, day, record):
    if not allowed or operation != "read_roundup":
        return "I can't run that request."
    if record is None:
        return "There is no roundup for that day."
    if record["as_of"] != day:
        return "I don't have a current roundup for that day."
    return f"Roundup for {day.isoformat()}: {record['items']} items."
cases = (
    ("exact date", ("read_roundup", True, REPORT_DAY, FIXTURE),
     "Roundup for 2026-01-09: 3 items."),
    ("missing report", ("read_roundup", True, REPORT_DAY, None),
     "There is no roundup for that day."),
    ("stale report", ("read_roundup", True, REPORT_DAY, STALE),
     "I don't have a current roundup for that day."),
    ("denied reader", ("read_roundup", False, REPORT_DAY, FIXTURE),
     "I can't run that request."),
    ("unsupported operation", ("publish_roundup", True, REPORT_DAY, FIXTURE),
     "I can't run that request."),
)
for name, args, expected in cases:
    observed = reply(*args)
    if observed != expected:
        raise AssertionError(f"{name}: {observed!r} != {expected!r}")
    print(f"PASS {name}")
```

Expect five `PASS` lines ending with `PASS unsupported operation`. The stale fixture has the same item count as the current one. That's deliberate: if you remove the date check, the stale case fails even though the number still looks right. The lab passes a record in memory, so there's no storage access to protect. In a service, check permissions before issuing the query, and have the backend return a typed result the reply renderer can use without having to infer what happened.

```text
Read request
    +-- Operation or caller denied? --> Refuse, no backend read
    +-- Backend timed out? ---------> Say the read failed; allow a retry
    +-- No report for that date? ---> Say it is missing
    +-- Report for another date? ---> Say it is stale for this request
    `-- Exact date returned? -------> Read the result and show its date
```

A timeout belongs in the service test, even though the in-memory lab can't produce one. Treat it separately from a missing report: a slow backend hasn't told you whether a report exists. For a voice pilot, record the time from the end of the utterance to the first reply audio. Log the tool duration separately so you can tell whether the user's waiting on the report or on the voice pipeline. A turn ID, status, and timing are enough to start diagnosing those failures without logging raw audio or transcripts by default.

![Person holding a phone beside a laptop](https://images.pexels.com/photos/5387286/pexels-photo-5387286.jpeg?auto=compress&cs=tinysrgb&w=1260)

## Decide whether to build

For my own work on a computer, I'd try voice in Codex before building a new app. Pick a question you can verify independently and compare the returned result with the source. If you're looking at a report, check the date and the report itself. When the next step is reviewing a diff or comparing two similar results, keep the screen. I put the setup and permission rules for using [Codex as a voice remote for a computer or VPS](https://matintellect.com/en/posts/voice-ai-agent-work) on my site.

A dedicated app makes more sense when voice is how someone already reaches the business, like calling a front desk. Try one task with an answer you can check, such as reading opening hours from the same source staff use. Include a holiday schedule in the test. If the caller asks to change a booking while you're still testing hours, send them to a person. Score the pilot by whether callers got the correct answer or reached the right person, including when the system couldn't complete the task. A polished voice won't fix the wrong holiday schedule.

Photo credits: Jakub Zerdzicki and kaboompics, under the [Pexels License](https://www.pexels.com/license/). The photos illustrate the input devices; the diagrams describe the lab's design, not the internals of the AI Agent Team project.
