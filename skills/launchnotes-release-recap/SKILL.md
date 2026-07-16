---
name: launchnotes-release-recap
description: >
  Use when the user wants to know how a published update or a release landed — e.g. "how did
  last week's announcement do?", "recap the 2.4 release performance", "which updates got the
  most engagement?". Reports per-announcement engagement (views, email open/click, feedback
  sentiment, reach) and audience health from LaunchNotes' own analytics. Read-only. It does
  not measure product usage or adoption — that data isn't in LaunchNotes. Load launchnotes-use first.
---

# Recap how a release landed

An engagement recap a PM can paste into standup — from LaunchNotes analytics only.

Requires: launchnotes-use loaded, a LaunchNotes project. Best when the user names a specific
announcement or a recent release window.

## Steps

1. Pull per-announcement metrics with launchnotes_get_top_announcements (ranked, up to 50):
   unique viewers, emails sent, open/click rate, feedback sentiment, per-channel reach. A
   specific recent announcement will surface here reliably.
2. Add audience context with launchnotes_get_project_analytics: subscriber count and the
   confirmed / unsubscribed / blocked breakdown, plus overall sentiment.
3. Report the highlights plainly — what got read, what resonated, how the audience is trending.
   Lead with the one or two numbers that matter, not a data dump.

## Guardrails (specific to this skill)

- Aggregate only, and say so. You can't see individual subscribers, emails, or raw exports —
  that stays in LaunchNotes by design. Frame it as a trust feature, not a gap.
- No product-usage claims. LaunchNotes measures communication engagement, not whether the
  feature got adopted. Don't imply otherwise.
