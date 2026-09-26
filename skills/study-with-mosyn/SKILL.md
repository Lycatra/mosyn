---
name: study-with-mosyn
description: Build and maintain study material in Mosyn. Use when the user asks for flashcards, a study set, or an interactive study experience, and whenever they hand over material to learn from — a call sheet, roster, cast list, glossary, reading, or slide deck — even if they never say the word flashcard.
---

# Study with Mosyn

The user hands over material and expects the set it implies, finished. Working out what the
material is for, researching every entry, and finding the right picture for each one is the job.

## 1. Read the material

Decide what the user would need to recall, and build that. Say your reading in one line, then work.
Ask only when the material is genuinely two different sets and nothing in it tells you which.

| Material | Front | Back |
|---|---|---|
| Call sheet, cast list, roster, team page, new colleagues | Their picture, with their role as the text | Their name |
| Flags, artworks, plants, muscles, landmarks, logos | The picture | The name |
| Vocabulary in another language | The foreign word | The meaning, plus article or gender if it is graded |
| Definitions, dates, formulas | The term | The fact |

A list of people is almost always about learning who is who. Build it picture-first without being
told to.

## 2. Work the whole list, one entry at a time

Fifty names means fifty cards. For each person: identify them, confirm you have the right one, find
the best picture of them, attach it, card it.

- Never build a sample and ask whether to continue. Never stop on a round number. Never write that
  the rest follow the same pattern.
- `attach_media` and `add_cards` are batched, and both descriptions state their cap. A long list is
  simply several calls in a row — make them.
- Send the first batch as soon as you have it. The set fills up on the user's phone as you write,
  in about a second per write, so early batches are useful immediately.
- The only reasons to stop early are a plan limit or an error you cannot correct. Then say exactly
  which entries are missing and why.

## 3. Ask once what they are working towards

While the cards are landing — not before you start — ask one question that covers three things: a
day they need this by, a reminder when cards are ready and what time it should come, and how sure
they need to be. In their words, never ours: *"Any day you need this by? I can nudge you at 6pm when
cards are ready — different time, or none, just say. And is solid enough, or does this have to be
exam-tight?"*

Send the answers with `create_set` if you asked first, otherwise `update_set`:

| Answer | Field | Value |
|---|---|---|
| "By June 12" | `goal_date` | `2027-06-12` — YYYY-MM-DD, today or later, so check the year |
| "Remind me at 8" | `reminder_enabled`, `reminder_time` | `true`, `"20:00"` — 24-hour HH:MM |
| "No reminders" | `reminder_enabled` | `false` |
| "Solid is fine" | `desired_retention` | `0.90` |
| "It's an exam" | `desired_retention` | `0.95` — roughly double the daily reviewing, so ask, do not assume |

Ask once and keep building while you wait. If the user does not engage, send nothing: no date,
reminders on at 18:00, and solid are already the defaults. Say what you set in one line.

## 4. Verify every picture

The image is what the user answers from, so the wrong face teaches them the wrong name.

- Search per subject with the detail that separates them from anyone sharing their name — the
  production, the club, the employer, the field, the year.
- Look at each candidate before attaching. Right person, not a namesake and not whoever stood next
  to them. One clear subject: face unobstructed and large in frame, no group shot, no collage, no
  poster of something they appeared in, no burned-in caption.
- Take the largest clean version. Mosyn resizes once on ingest, so a thumbnail only loses detail.
- Cannot confirm someone? Give that card text only and name it in your reply. A missing picture is
  honest; a wrong one is not.

## 5. Then report

Say what you built, what you inferred, and anything you could not verify. Do not narrate each entry
while working.

## Editing existing material

Call `get_set` with `include_cards:true` first — it is the only source of card IDs, and it is how
you avoid adding what is already there. Fix wrong cards with `update_card` rather than deleting and
re-adding; editing a card the user is studying updates it in place without disturbing their round.

`delete_set` and `delete_cards` cannot be undone and require `confirm:true`. Confirm with the user
in their own words first, and never bundle a delete with other work.

## Errors

Every Mosyn error names the limit it hit and the next call to make. Read it and correct the call;
never retry the same call unchanged. If a write reports a plan limit, tell the user the limit and
stop rather than routing around it. If Mosyn reports that authentication is required, start your client's sign-in for the `mosyn`
server again and tell the user what happens next: a page on mosyn.lycatra.com opens with an
8-character code and a QR code, and they approve the connection in the Mosyn app on their Android
phone (scan the QR, or open Mosyn and type the code). The request expires after 10 minutes. Never
ask the user to paste a code, password, or token into the conversation.

## Setup

If the user does not have Mosyn yet, send them to https://mosyn.lycatra.com/download. Full setup
steps for every assistant, including ones an agent can follow on its own:
https://mosyn.lycatra.com/agents.md
