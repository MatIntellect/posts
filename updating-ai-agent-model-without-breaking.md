# Updating an AI agent model: upgrade runbook with backup, test and rollback

Type: operations runbook. Reader: whoever is responsible for AI agents in a business, technical or not. Goal: decide whether to upgrade, back up the whole agent, test the new model safely, switch one agent at a time and roll back cleanly. Limits: a runbook in prose and tables; no runnable code or configuration

![AI-generated illustration of updating an AI agent model safely](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-updating-ai-agent-model-without-breaking-1794179655.jpg)

## Reference practice

Verified facts, as published on my site and project pages:

- every day 8 Claude Code agents work for me, on Sonnet 5 and Opus 5.5 depending on the role
- I update them by hand when a major model comes out; the last move was from Opus 5 to Opus 5.5, skipping versions in between
- agents are moved one at a time, with their real work watched before the next
- backups run automatically at least weekly, plus a manual backup before every major update
- my personal agent Jes has a primary and an automatic backup model, so its 10 scheduled jobs keep running if the primary fails
- client systems run on the client's own servers: a clinic runs a team of 6 agents, assistants run for five people; there, no model change happens without a backup and a single-agent test

## Step 0. Decide

| Reason | Upgrade? |
|---|---|
| Current model cannot handle a specific task | Yes |
| Clear difference in price | Yes, after testing |
| Clear difference in speed | Yes, after testing |
| New version, nothing to fix | No; the risk brings no benefit |

## Step 1. Read the provider's notes

Behaviour and settings can differ from the previous version. Write down anything that could affect your agents before running a single test

## Step 2. Back up the whole agent

| Item | Why |
|---|---|
| Instructions | Behaviour is defined here |
| Memory | Rolled-back model with new memory is a third, untested state |
| Code | Integrations may have been adjusted |
| Data | Changes made during tests or after the switch |
| Connection settings | Keys and endpoints |

Daily automatic backups for the whole system; a separate manual backup before an important change

## Step 3. Verify the backup

Check its date and restore it away from the live system. Keep backups separate from the main system with restricted access; they can hold personal data and keys

![Working at a computer during a system update](https://images.pexels.com/photos/19825057/pexels-photo-19825057.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Step 4. Test in isolation

Run the new model separately from the live agent. Switch off real sends and data changes, or use safe test records

## Step 5. Replay a task set

About ten real tasks the old model definitely handled, including rare scheduled jobs and cases where the agent must stop and ask. Example for a calendar agent: reads the date correctly, finds free time, asks before creating a meeting

| Compare | Old | New |
|---|---|---|
| Follows instructions | | |
| Uses tools correctly | | |
| Asks for confirmation where required | | |
| Speed | | |
| Cost | | |

## Step 6. Switch one agent

Leave it on real work long enough to cover all its usual tasks, including weekly ones. Tell the people who work with it that the model changed and where to report oddities

## Step 7. Continue or stop

Stop before the next agent if any of these appear:

- steps from the instructions are skipped more often
- answers become noticeably longer or shorter
- tools are used differently
- confirmations are requested less often
- tasks from the replay set no longer pass

If a model is better at one role and worse at another, different agents can stay on different models

## Step 8. Roll back

Restore the previous model and settings, and data from the verified backup if needed. Actions already taken in external services, such as sent messages or created records, are not undone by a backup and need separate fixing

![Checking work on several screens](https://images.pexels.com/photos/34803990/pexels-photo-34803990.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

## Model log

| Agent | Model | Switched on | Backup before switch |
|---|---|---|---|
| | | | |

## Common mistakes

- upgrading every agent at once
- backing up the model setting only
- never restoring a backup to test it
- testing with real sends on
- judging by the provider's description instead of your own tasks
- upgrading for the version number

More on how upgrades fit into ongoing support is on the [AI support service page](https://matintellect.com/en/services/ai-support) of my site
