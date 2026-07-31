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

## Installation

Pick your client. **Installing the plugin gives your agent the tools _and_ all the skills**; a bare MCP connection gives tools only.

### Claude Code

Run these **one at a time** — the first registers the marketplace, the second installs the plugin from it:

1. `/plugin marketplace add launchnotes/mcp-server-guide`
2. `/plugin install launchnotes@launchnotes`

Sign in through your browser when prompted — the connection runs as **you**, with your real LaunchNotes permissions. Tools + skills, done.

### Claude Desktop / claude.ai

Install the plugin (tools + skills) — requires a paid plan (Pro, Max, Team, or Enterprise):

1. In Claude's settings, go to **Customize → Plugins**.
2. Click **Add → Add marketplace → Add from a repository**.
3. Paste `https://github.com/launchnotes/mcp-server-guide` and click **Sync**. (Leave **Sync automatically** on to pick up future updates.)
4. Open the **LaunchNotes** plugin that appears and click **Install** (the **+**).
5. Sign in through your browser when prompted.

Prefer just the tools? Add a **custom connector** pointing at `https://mcp.launchnotes.com/mcp` — connectors carry the tools but not the skills.

### Cursor

**Tools** — Add the MCP server in **Cursor → Customize → MCPs → Add**:

```json
{
  "mcpServers": {
    "launchnotes": {
      "url": "https://mcp.launchnotes.com/mcp"
    }
  }
}
```

Sign in through your browser when prompted.

**Skills** — the MCP connection above doesn't include skills. Until one-click install lands in the Cursor Marketplace, add them manually with one of these:

- **Full plugin (tools + skills together):**
  ```bash
  git clone https://github.com/launchnotes/mcp-server-guide
  mkdir -p ~/.cursor/plugins/local
  ln -s "$(pwd)/mcp-server-guide" ~/.cursor/plugins/local/launchnotes
  ```
  Then run **Developer: Reload Window** in Cursor. This bundles the tools too, so you can skip the **Tools** step above — you'll still sign in when prompted.
- **Skills only (if you already added the tools above):**
  ```bash
  git clone https://github.com/launchnotes/mcp-server-guide
  mkdir -p ~/.cursor/skills
  cp -R mcp-server-guide/skills/* ~/.cursor/skills/
  ```
  Then reload Cursor. Skills appear in **Customize → Skills**.

_One-click install from the Cursor Marketplace is coming._

## Skills

Skills come with the **plugin**, so how they arrive depends on your client: **Claude Code** installs them automatically, **Claude Desktop / claude.ai** get them when you install the plugin, and in **Cursor** you add them with the manual step above. Each one loads itself when the moment fits. Start with **`launchnotes-use`** — it's the foundation the others build on (your voice, the safety rules, how the objects behave).

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
