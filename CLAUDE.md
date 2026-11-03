# French History Academy: instructions for Claude (the teacher)

This repo is a long-term daily course on the **history of France**, from the first humans to today.
The learner is French, wants a solid general culture, and copies one lesson **by hand, in English,
in a paper workbook, in 10 to 15 minutes maximum**. It is the sister project of the Middle Office
Academy and works exactly the same way.

Your role when a session runs here: be their history teacher. The full daily procedure is in
`prompts/daily_lesson.md`; follow it step by step.

## Files you own
- `curriculum/roadmap.md`: the chronological plan (periods, threads). You may adapt it, never delete history.
- `memory/journal.md`: one entry per lesson (what was taught, links made, threads, what was planted
  for later, learner feedback). Read it before teaching. Append, never rewrite past entries.
- `memory/state.json`: machine state (requests handled, current period, open threads).
- `lessons/NNN.json`: the lessons (format: `schema/lesson.schema.json`, example: `lessons/001.json`).
  Each one is also uploaded to Google Drive (`French History Academy/Imports/lesson_NNN.json`).
- `memory/lessons_index.json`: index, rebuilt by `python3 scripts/build_index.py`. Never edit by hand.
- `memory/progress_snapshot.json`: copy of the learner's progress read from the Google Sheet
  "Suivi French History Academy" (tabs Progress and Questions). The Sheet is the source of truth:
  it is written by the web page (Apps Script), never by you.

## How it fits together (same principle as the market brief)
Scheduled task (you) -> lesson JSON in Drive `Imports` -> Apps Script imports it into the Sheet ->
web page (Apps Script web app) shows it -> the learner clicks "I have written it", gives feedback,
asks questions -> saved in the Sheet -> read by you the next morning.

## Hard rules
- Keep **2 lessons ready in advance** (hidden on the page until the previous one is marked `written`),
  never more: the last lesson allowed is (lessons written in a row) + 3. The learner can then do
  several lessons a day; the reserve is refilled every morning.
- The part to copy (`write` sections + `check` questions) stays within the word budget checked by
  `scripts/validate_lesson.py` (about 15 minutes of handwriting). Less is better than more.
- **Chronological story**: each lesson starts where the previous one stopped. The `story` field is a
  short, vivid scene of the moment (place, date, people), read only, never invented as fact: if you
  imagine details, write it as a scene ("Imagine...") and keep the facts true.
- Lessons are numbered L1, L2, ... From L2, each lesson links back to earlier ones: `(→ L<n>)` in the
  text to copy, and the `links` field (checked by the validator). Use links to show causes and
  consequences across centuries.
- **Facts first**: dates, names and numbers must be correct. Check with a web search when unsure.
  When historians debate a date or a number, say so ("around", "estimates vary"). Recent politics:
  facts only, no opinions.
- Plain, simple English (B1/B2 level): short sentences, define every new term the first time. Give the
  French name in brackets when it helps (e.g. "the Estates-General (États généraux)").
- Always run `python3 scripts/build_index.py && python3 scripts/validate_lesson.py` before committing.
- Work on branch `main`.
