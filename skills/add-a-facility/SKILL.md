---
name: add-a-facility
description: Put a pool facility's published schedule into Pool Relay, lane by lane. Use when someone asks to add, import, build or model a pool, aquatic center, YMCA or swim facility, or to enter a schedule from its website, a PDF or a registration system. Covers finding the lane counts, building pools and lanes, placing each program on lanes, staging it in a draft, and listing questions for the pool staff.
---

# Add a facility to Pool Relay

The result is a facility whose calendar a swimmer can read the way a pool deck is read: lanes across the
top, time down the side. Everything is staged in a draft and shown to the person before it goes live.

## Rules that are never broken

- **Model only the physical water:** facility → pool → configuration → lane. Never create areas named for
  programs or groups ("Lap Lanes", "Lesson Area", "Team Lanes", "Program Area", "Open Swim Area"). They tell a
  swimmer nothing.
- **Every pool gets its real lanes.** Find the count (see `references/finding-lane-counts.md`). If it cannot be
  found, use the standard and say it is an estimate: a 25-yard pool has 8 or 10 lanes; a 50 m pool has two
  configurations, 8 lanes long course and 20 lanes short course. Only a feature with no lanes (a splash pad, a
  play pool) takes bookings on the pool itself.
- **One event holds one set of lanes.** When a program's lanes change during its block, split it into separate
  events at each change.
- **Lanes in one event are side by side.** Never give an event lanes 1, 2, 5 and 6.
- **A booking that repeats is one recurring event.** Same title, groups, time and lanes on several days means one
  event with a weekly recurrence (`byWeekday` listing its days), ending on the season's last day when it has one.
  Never a copy per day: a person changes a series in one edit, but has to find every copy. Days that differ in time
  or lanes are separate series.
- **More than one write means a draft first.** Show the review before taking it live.
- **Never invent a time, a lane count or a program.** A time that isn't published is a question for the staff,
  not a guess.

## Steps

1. **Find the sources.** Read the facility's own pages first: hours, lap swim, lessons, water fitness, teams.
   Then look for its registration system (ActiveNet, Daxko, RecDesk, Salesforce, YMCA360, mywellness) and the
   practice pages of any clubs that train there. Note the date each source was read and the season it covers.
   Many sites are stale: a lesson list from a session that already ended is common. Registration usually holds
   the current classes.
2. **Find each pool's lane count and length** (`references/finding-lane-counts.md`). Record the source and your
   confidence.
3. **Check what exists.** Call `list_facilities` and `list_groups`. Don't duplicate a facility that is already there.
4. **Build the water.** Call `add_facility_area` for the facility, with its real street address. Then add each
   pool. For a 50 m pool, add two configs, "Long Course" and "Short Course", each with its own lanes numbered from
   1. Otherwise add the lanes straight under the pool. Name things what people say: "Lap Pool", "Lane 3".
5. **Build the groups.** Add one org for the facility (and one per outside club). Under it add teams by program
   (Lap Swim, Swim Lessons, Water Fitness, Swim Team), and practice groups for levels or squads.
6. **Place programs on lanes.** Follow `references/lane-placement.md`, and use `suggest_assignment` when unsure.
   Add "Lane assignment is our estimate" to the description whenever the source doesn't name lanes.
7. **Stage it.** Call `create_draft`, then `create_events` with a whole pool or week per call (up to 60), one
   entry per recurring series rather than per day. Keep
   titles short so they fit in a lane column ("Level 1", "Parent & Child"), and keep full names in the
   description. Lessons that start at the same time share one event tagged with every level.
8. **Audit before publishing.** Call `find_conflicts` for the range. Every conflict is either a data-entry error
   to fix, or a real overlap in the published schedule to keep and ask about.
9. **Review and publish.** Call `review_draft`, show it, get agreement, then call `take_draft_live`.
10. **Report the open questions** (`references/questions-for-staff.md`): conflicts between the facility's own
    pages, missing times, and every estimate you made.

## What to tell the person at the end

- What was entered: pools, lane counts and their sources, programs and date ranges.
- What was estimated: lane counts, lane placement.
- The questions for the staff.
- Whether the draft is live.
