# LaunchNotes MCP Server Guide

Bring LaunchNotes into your AI assistant. Connect the LaunchNotes MCP server and your agent can turn shipped work into announcements, keep your public roadmap up to date, and measure how updates land — from Claude, Cursor, or any MCP client, in your own voice.

This repo is the install surface: the MCP connection plus a set of **skills** — pre-built playbooks that teach your agent how to run the LaunchNotes jobs that matter, so you describe the outcome and it runs the sequence.

> **Skills teach your AI assistant how your team turns work into announcements, a roadmap, and a branded page — reliably, and in your own voice.** Without them, you'd walk the assistant through every step each time; with them, you just say _"draft an announcement for what we shipped this week"_ and it already knows where to look and how you write. And because your assistant already has your other work open — your issue tracker, your docs, your analytics — a skill teaches it to pull from those and hand you a polished draft, never publishing anything without your go-ahead.

## What you can do

- **Announcements** — list and filter, read details, create, update, publish now, schedule, archive, attach supporting links.
- **Roadmap** — list stages and work items, create and edit items, move them between stages, read an item's full details, post progress updates that notify followers.
- **Categories** — list a project's categories and assign them to announcements and roadmap items.
- **Search** — find announcements, roadmap items, and ideas by topic, across the whole project.
- **Analytics** — top announcements by engagement, and a project snapshot (subscriber counts, feedback sentiment). Aggregate only, no personal data.
- **Feedback** — search and read reader feedback.
- **Page & brand** — set colors, page content, and features (feedback, roadmap, ideas, RSS, voting).

## Skills

Each skill is a playbook your agent loads automatically when the moment fits. Start with **`launchnotes-use`** — it's the foundation the others build on (your voice, the safety rules, how the objects behave).

| Skill | What it does |
|---|---|
| **`launchnotes-use`** | Foundation — loads first, everywhere. Establishes your voice, the draft-first safety rules, and how LaunchNotes objects behave. |
| **`launchnotes-draft-from-work`** | Turn shipped or in-progress work from your issue tracker (Jira, Linear, GitHub, ClickUp) into a publish-ready announcement draft. |
| **`launchnotes-ship-the-roadmap`** | Take a finished roadmap item public: draft its announcement, link the two, and advance its stage. |
| **`launchnotes-post-roadmap-update`** | Post a progress update to a roadmap item's timeline and notify the people following it. |
| **`launchnotes-feedback-to-roadmap`** | Cluster reader feedback into themes and turn the approved ones into roadmap items. |
| **`launchnotes-release-recap`** | Report how a published update landed — engagement and audience health, from LaunchNotes analytics. |
| **`launchnotes-style-your-page`** | Match your public page to your brand: colors, content, and features. |
| **`launchnotes-import-existing-changelog`** | Bring an existing changelog or blog into LaunchNotes, as drafts or a dated backfill. |

Skills live in [`skills/`](./skills) — each is a folder with a `SKILL.md` (and optional reference files). They're plain markdown: no code, and they run on **your own agent**, never LaunchNotes' AI.

## Installation

One install gives your agent the LaunchNotes **tools** and all the **skills**. Pick your client.

### Claude Code

```shell
/plugin marketplace add launchnotes/mcp-server-guide
/plugin install launchnotes@launchnotes
```

Sign in through your browser when prompted — the connection runs as **you**, with your real LaunchNotes permissions. Skills load automatically; just describe an outcome (see [Prompting your assistant](#prompting-your-assistant)).

### Cursor

Add the MCP server in **Cursor → Customize → MCPs → Add**, then save:

```json
{
  "mcpServers": {
    "launchnotes": {
      "url": "https://mcp.launchnotes.com/mcp"
    }
  }
}
```

Sign in through your browser when prompted — this gives you the tools today. This repo also ships a `.cursor-plugin/` manifest so the skills travel with the plugin; one-command install in Cursor is coming as we finalize Cursor distribution.

### Claude Desktop / claude.ai — tools only

Add LaunchNotes as a **custom connector** pointing at:

```
https://mcp.launchnotes.com/mcp
```

Sign in through your browser when prompted. Connectors carry the **tools** but not the skills — for the full one-install experience (tools + skills), use Claude Code. _(If you want the skills on claude.ai too, they can be added manually as a ZIP upload.)_

## Prompting your assistant

Describe the outcome; the right skill loads itself. For example:

- _"Draft an announcement for everything we closed in the 2.4 milestone."_
- _"We shipped the billing revamp — announce it and move it to Released."_
- _"Post a roadmap update that the auth feature is now in development."_
- _"What are people asking for? Put the top themes on the roadmap."_
- _"How did last week's announcement do?"_
- _"Make my page match our website's brand colors."_

## Best practices

- **Draft-first.** Your agent creates and edits freely, but treats anything customer-visible as publish-on-confirmation. It won't publish, schedule, notify, or move a roadmap stage without your explicit go-ahead.
- **Know who gets notified.** Before anything reaches subscribers, your agent states the effect — _"this emails ~30k subscribers"_ vs. _"public page only, no email"_ — and waits for your yes.
- **Give it your voice.** If you have a tone/voice guide or drafting instructions, point your agent at them; drafts come out sounding like your team, not a generic AI.
