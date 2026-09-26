---
name: publish-a-pool-calendar
description: Publish Pool Relay calendars that swimmers can read, and embed them on a facility's website. Use when someone asks for a public calendar, a shareable link, an embed code, a lap swim or lessons page, or a mockup of a pool's website with live schedules.
---

# Publish a pool calendar

A public calendar has one job: answer "when can I swim, and where?" at a glance. Build each one for a single
question, publish it, and embed it with the snippet Pool Relay returns.

## Which calendar for which question

| Question | Build this with `save_view` |
|---|---|
| "When can I swim today at this pool?" | **Lane view.** rows: time of day; cols: lane; page: day, pool (the facility's main pool selected), team (All). |
| "What's on this week?" | **Week view.** rows: time of day; cols: weekday; page: week, plus a pool or team menu. |
| "When is lap swim / are lessons / is water fitness?" | Week view filtered to that program's groups. A lessons view gets a practice-group menu so a parent can pick a level. |
| "Where can I swim across our pools?" (many facilities) | Day view with one row per pool (rows: facility, pool). This is an overview, because many pools can't sit side by side lane by lane. Link each pool to its own lane view. |

## Settings that matter

- **Menus open on All**, unless the tab is about one pool. A menu with no selection opens on whatever sorts first.
- **A tab about one facility** selects that facility in its location page filter.
- **50 m pools open on the configuration swum this season.** Pass `configurations:
  [{pool: "<facility> / <pool>", configuration: "Short Course"}]` to `save_view`. For a tab that already exists,
  call `set_view_configuration`. Without either, the tab opens on the pool's first configuration.
- **Hide conflicts on public tabs** with `presentation.showConflicts: false`. Keep block titles short, with the
  full name in the description.
- **Every public tab needs event titles on its blocks.** Put `{dim: "event", level: "title"}` in `grid`.
- **Pick a day window that fits the schedule,** for example 5:30am–8:30pm, so the grid isn't mostly empty.

## Publishing and embedding

1. Call `share_view` for each tab. It returns a public link (`/v/<token>`) and an embed snippet (`/embed/<token>`).
2. Always use the embed snippet as given. It includes `width="100%"`, so the calendar opens at the right layout
   before the host page's stylesheet loads.
3. Nobody outside Pool Relay can see a tab until it is shared. Unsharing with `unshare_view` stops the link and
   the embed immediately.

## Checking your work

Open each public link and look at it as a swimmer would, including at phone width. Check three things:
the blocks carry readable names, each block's lanes sit side by side, and nothing reads as an invented area.
