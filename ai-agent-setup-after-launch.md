# AI agent setup: a safe onboarding checklist

Use this checklist after an agent starts successfully but before it gets access to real messages, calendars or production data. The goal is to establish instructions, check tool permissions and verify how memory persists. It is a workflow checklist, not a tested application or an assurance that a model will obey every rule

## Prerequisites

- An agent you can run in a test environment and a way to inspect its instructions
- Test records or a sandbox for any tool that can modify data
- A human owner who can approve actions and review what the agent stores

## 1. Capture the operating rules

Ask the agent to interview the owner about tasks, communication preferences and actions that need approval. Ask for answer options but allow a free-text correction. Have the agent display its proposed persistent instructions before saving them

Check that instructions distinguish what the agent may read, what it may change, and when it must ask. Avoid adding private facts that the task does not require

## 2. Connect and test tools

Connect only tools needed for the first workflow. Test with safe records: for a calendar assistant, ask it to find availability and prepare a proposed event without creating a real one. Verify the tool's actual permissions independently of the agent's written instructions

[MCP](https://modelcontextprotocol.io/docs/getting-started/intro) is one standard for connecting AI applications to external systems. A connection is not an authorization policy; configure and verify permissions for each tool

## 3. Test memory across sessions

Ask the agent to save a harmless preference, start a new session and ask it to retrieve the preference. Inspect the stored record and correct it if necessary. That checks a single behavior, not every possible memory failure

Keep important facts concise and link to detailed material where the system supports it. Review records daily or weekly when appropriate; before archiving, check that the agent can still retrieve details and that recovery is possible

For project instructions, Codex documents [AGENTS.md](https://developers.openai.com/codex/agent-configuration/agents-md); Claude Code documents [CLAUDE.md and auto memory](https://code.claude.com/docs/en/memory). File discovery and persistence differ by product

## Done when

You can inspect the instruction the agent loaded, identify each connected tool and its permissions, and reproduce the harmless memory check across sessions. If a check fails, correct the setup before giving the agent a real action

I cover agent setup as part of [building AI agents](https://matintellect.com/en/services/ai-agents)
