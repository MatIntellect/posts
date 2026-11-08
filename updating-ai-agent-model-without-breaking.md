# Updating AI agent model without breaking things

![Cover](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-updating-ai-agent-model-without-breaking-1794179655.jpg)

A new model release does not mean every running agent needs to move immediately. I update my Claude Code agents manually when a major model arrives. My last move was from Opus 5 to Opus 5.5, skipping the versions in between

Before every major update, I make a manual backup. Several models also make automatic backups for me at least weekly. My recommendation is a daily automatic backup of the entire system, plus a separate copy before important changes

## Make rollback possible

Model configuration is only one part of an agent. Its instructions, code, memory, data and connection settings also shape what it does. If you save only the model name, switching it back might leave the rest of the system changed

![Data storage hardware](https://images.pexels.com/photos/19825057/pexels-photo-19825057.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

Check that the backup is recent, then test restoring it somewhere separate from production. Protect access to the copy because it may include personal information and connection settings. [CISA's guidance](https://www.cisa.gov/sites/default/files/publications/protecting_your_networks_from_ransomware.pdf) recommends testing recovery and keeping backups isolated

A backup helps restore system state; it does not automatically undo actions already taken elsewhere. If an agent sent a message or changed a record in another service, that action may need its own correction

## Compare on actual work

Set up the candidate model away from the working agent. Use representative everyday tasks alongside difficult cases where mistakes matter. For a calendar agent, check date interpretation, availability lookup and whether it asks for confirmation before creating a meeting

During the test, disable real sends and changes or work with safe test records. Compare tool calls and instruction-following as well as the final answer. Measure speed and cost for your own tasks: a model can be more capable on paper without being the right fit for the job

![Software debugging](https://images.pexels.com/photos/34803990/pexels-photo-34803990.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

Read the provider's migration instructions too. [Anthropic's Opus 5.5 guide](https://docs.anthropic.com/en/build-with-claude/prompt-engineering/prompting-claude-opus-5-5) describes differences from Opus 5 and how to adjust reasoning effort. Settings that worked before may need a fresh test

## Move one agent first

Switch a single agent and inspect its real tasks and errors before updating another. Keep the old configuration available, and restore the previous model and data if needed. The choice of when to update remains yours; not every release needs to be installed

Model changes are part of [AI system support and development](https://matintellect.com/en/services/ai-support). A useful upgrade is one that works for the job and leaves a tested route back
