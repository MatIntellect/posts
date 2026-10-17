# AI system maintenance: what breaks after launch

![Поддержка системы после запуска](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-ai-system-maintenance-what-breaks-after-launch-1792199900.jpg)

Every AI system I have launched broke after launch. Not because of sloppy work - because AI development is always custom, and there are plenty of points where something can go wrong. The difference between a living system and dead weight is one thing: whether someone kept watching.

## Where it breaks

**Data drifts.** Price lists, schedules, documents - they change without warning. The code is intact, but part of the logic is already working blind.

**External dependencies.** A model gets updated and answers slightly differently. A platform changes its API - the chain snaps. You touched nothing.

![Component repair in a workshop](https://images.pexels.com/photos/33118659/pexels-photo-33118659.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

**Users.** Tests had clean requests; real life has typos and questions that were never in the plan. All of it lands exactly where tests never looked.

**The business itself.** A new service, new rules - logic built for the old process quietly goes stale.

**Time.** A system nobody touches degrades on its own: data drifts, small issues pile up, and one day it simply no longer matches reality.

## Why this is normal

None of the five mean the system was built badly. A custom system lives inside reality, and reality does not stand still. That is not a defect - it is a property. Launch and forget works only with a toaster.

![System monitoring dashboard](https://images.pexels.com/photos/10468213/pexels-photo-10468213.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## What to do

Plan maintenance from the start, as a stage of development rather than an option. Watch the system on live data, fix bugs before users notice, keep the logic aligned with the process. A month of live work reveals more than any acceptance run before launch - and every following month keeps that picture true. This stage can never be skipped - without it, the development becomes dead weight. That is why I run maintenance in monthly cycles rather than one-off emergency calls. A practical pattern that works: keep a short journal of what changed around the system each month - data sources, upstream APIs, business rules - and check the system's answers against it. Most drift becomes visible in ten minutes of comparison; invisible drift becomes an incident.

I wrote a longer breakdown here: [AI system maintenance: what breaks after launch](https://matintellect.com/en/posts/ai-system-maintenance-what-breaks-after-launch)
