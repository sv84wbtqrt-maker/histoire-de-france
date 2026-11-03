# French History Academy

A daily course on the **history of France**, in chronological order, copied by hand in English in
10 to 15 minutes. Sister project of the Middle Office Academy, same principle as the market brief:
every morning a Claude scheduled task writes the next lesson and drops it in Google Drive; a Google
Apps Script imports it into a Google Sheet and shows it on a web page. A new lesson comes only after
you mark the previous one as written.

## How it works
```
Claude scheduled task (morning) ── lesson_NNN.json ──▶ Drive "French History Academy/Imports"
        ▲                                                         │ (Apps Script imports it)
        │ reads your progress and questions                       ▼
Google Sheet "Suivi French History Academy" ◀── your clicks ── web page (Apps Script web app)
```
- **Numbered lessons with links**: L1, L2, ... From L2, each lesson links back with (→ L<n>) to show
  causes and consequences across the centuries; links are clickable on the page.
- **Questions** ("Ask" page) become one of the next lessons (3 lessons later at most).
- **Feedback** (too easy / too hard, too short / too long) adapts the next lessons.
- **Every 7th lesson is a review.**
- **Memory of the teacher**: `memory/journal.md`, `memory/state.json`, `memory/progress_snapshot.json`,
  `curriculum/roadmap.md` (14 periods, about 196 lessons, then a deepening phase), `lessons/`.
  Rules: `CLAUDE.md`, `prompts/daily_lesson.md`.

## Setup (once, about 5 minutes, same as the Middle Office Academy)
1. https://script.google.com > **New project**, name it "French History Academy".
2. Replace `Code.gs` with `apps-script/Code.gs`.
3. **+ > HTML**, name it `Index`, paste `apps-script/Index.html`.
4. Project Settings > tick "Show appsscript.json manifest file in editor"; replace `appsscript.json`
   with `apps-script/appsscript.json`.
5. Run `setup` and accept the permissions: it creates the folder "French History Academy", the
   subfolder "Imports" and the Sheet "Suivi French History Academy".
6. **Deploy > New deployment > Web app**: execute as "User accessing the web app", access "Only myself".
   Bookmark the URL.
7. In claude.ai, open the scheduled task "French History Academy: daily lesson", select this repository
   and add the **Google Drive** connector.

## Checks
```
python3 scripts/build_index.py && python3 scripts/validate_lesson.py && python3 -m unittest discover -s tests
```
