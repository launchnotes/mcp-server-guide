---
name: launchnotes-use
description: >
  MANDATORY prerequisite — load this skill before any other LaunchNotes skill, and before
  the first time you create, edit, publish, schedule, link, categorize, or move anything in
  LaunchNotes in a session. It establishes the user's writing voice, the draft-first safety
  rules, and how LaunchNotes objects actually behave (announcement states, roadmap
  visibility, set-replace fields, who gets notified). Skipping it causes off-voice drafts,
  silently wiped links/categories, unexpected notification blasts, and invisible or wrongly-
  published content. Other LaunchNotes skills depend on the rules here and do not repeat them.
---

# Working in LaunchNotes

The shared foundation the other LaunchNotes skills build on. ("User" = the LaunchNotes account
holder you're helping; "customer" = their end-users/subscribers.)

## 1. Voice matters — use the user's

Announcements should sound like the user's team, not a generic AI. Before drafting, ask if they
have a tone and voice guide or drafting instructions — most teams have one. If they don't, offer
to draft a short one from their recently published announcements, then write in that voice; they
can keep it wherever's convenient. A clear guide is just a few short sentences on audience (e.g.
"internal employees"), voice (e.g. "confident, not corporate"), and a couple of rules (e.g.
"lead with value, not the feature").

Don't conflate this with LaunchNotes' in-product Smart Draft voice feature — separate surface,
not available via MCP. Don't reference or reuse its name.

## 2. Safety spine (applies to every skill)

- Confirm the project first. Resolve with launchnotes_list_projects — if there's one, use it;
  if there's more than one and the user hasn't named it, ask.
- Draft-first. Create and edit freely; treat anything customer-visible as
  publish-on-confirmation only.
- State the notification posture, then confirm. Before you publish, schedule, post a roadmap
  update, or move a stage, know who it reaches: launchnotes_get_announcement shows an
  announcement's posture (email / Slack / page, cohorts) and launchnotes_get_work_item shows a
  roadmap item's notification_audience. Say it plainly — "this emails ~30k subscribers" or
  "public page only, no email" — and require an explicit yes. Roadmap updates also can't be undone.
- No PII into content. launchnotes_search_feedback returns customer/reporter emails, and
  analytics are aggregate by design. Summarize on themes; never write a customer's name or
  email into a public field.

## 3. Set-replace fields — the wipe footgun

category_ids, announcement_ids, and work_item_ids replace the whole set, not append.
Omit → unchanged; [] → cleared; ["x"] → exactly that. Before editing an existing object's
set, read the current values (launchnotes_get_work_item / launchnotes_get_announcement) and
keep what should stay. A new object's set is empty, so a first assignment is safe.

## 4. How the objects behave (things you can't infer)

- Announcement dates: publish is immediate and stamps the date to "now"; schedule is future-only.
  To backdate, publish first, then set published_at (launchnotes_update_announcement).
- Roadmap visibility = stage, not state. An item is public when it's in a published stage
  and not archived. Make it public with launchnotes_move_work_item; there's no "publish item."
- Linking mirrors the app: only a published announcement ↔ an active work item in the same
  project. Anything else is rejected with a reason (and would be invisible anyway).
- Categories are assign-by-ID (launchnotes_list_categories); you can't create categories
  here, so never invent one.
- Draft links aren't returned on create. launchnotes_create_announcement gives you an ID only.
  Call launchnotes_get_announcement and hand back the Private URL — it opens in LaunchNotes
  whether or not the announcement is published; the Public URL doesn't resolve until it is.
  Never build a link from the slug.

## 5. Be honest about limits

If something can't be done, say so and why. An honest "can't, because…" beats a fake success.
