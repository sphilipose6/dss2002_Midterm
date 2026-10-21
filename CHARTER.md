# Team Charter - Walmart Hurricane Analytics

DS-2002 Midterm, Fall 2026

## Roster

| Name  | Primary role             | Backup for               |
|-------|--------------------------|--------------------------|
| Ethan | Cleaning + decision log  | Weather API + join       |
| Steve | Weather API + join       | Analysis Q1-Q5           |
| Henry | Analysis Q1-Q5           | Cleaning + decision log  |


## 1. Goals

### A good result

A notebook that runs clean from Restart and Run All, that every one of us can explain line by line.
Every cleaning decision is written down with the rows it touched.
Each of the five questions has code, a number, a chart, and a written finding that a Walmart leader could act on.
A 6 minute presentation we have rehearsed at least once.

### What each person wants

No one on the team has a specific preference.
We split the work evenly so that everyone gets hands on time with cleaning, the API, SQL, and charts.

### What limits our time

Other classes, exams, and work shifts.
Anyone who knows about a conflict (travel, exam, deadline) posts it in the group chat as soon as they know.

### What to avoid

- Starting analysis before the cleaning pipeline is done. Q1-Q5 wait until the clean tables exist.
- Everyone editing `team_notebook.ipynb`. Only the notebook owner for the week commits to it.
- Decisions made in chat and lost. Every cleaning or analysis decision goes in the decision log.
- Leaving the weather API to the end. Steve gets one working call by Friday, Oct 23.
- Finding out about a problem in week 3. We raise blockers within a day.

## 2. Who does what

| Role | Owner | Backup | Responsible for | Done when | Grade area |
|------|-------|--------|-----------------|-----------|------------|
| Cleaning + decision log | Ethan | Henry | Cleaning functions, the SKU mapping table, and the decision log | One function turns raw files into clean tables. The log lists every decision and rows touched | Cleaning, 25% |
| Weather API + join | Steve | Ethan | API call with retries, parsing, timezone alignment, and a checked join to sales | One function returns daily weather. The join passes a row-count check. Base URL cited | Weather, 15% |
| Analysis Q1-Q5 | Henry | Steve | The five answers: code, a number, and a written finding each. Q5 uses SQLite | Every question has code, a number, and a paragraph | Questions, 30% |
| Charts + presentation | Shared (Henry leads talk, Ethan leads README) | All | At least six plots with message titles, the six-minute talk, and the README | Six labeled plots. The talk has been rehearsed once | Visuals, 15% |

The owner is who we ask.
The backup steps in when the owner can't.

### Notebook owner (rotates weekly)

| Week | Dates | Notebook owner |
|------|-------|----------------|
| 1 | Oct 19-23 | Henry |
| 2 | Oct 26-30 | Ethan |
| 3 | Nov 2-6 | Steve |

Henry currently holds the starter notebook and adds it to the repo as `notebooks/team_notebook.ipynb`, along with the five data files in `data/`.
The notebook owner merges finished functions from `notebooks/scratch/` into `team_notebook.ipynb` and runs Restart and Run All before pushing.

## 3. Question owners

The owner writes the code, the number, the chart, and the written finding.
The reviewer tries to break it: is the baseline stated, does the row count check out, does the chart say what its title says?

| Question | Owner | Reviewer | Waits on |
|----------|-------|----------|----------|
| Q1 Demand surge | Henry | Ethan | Date cleaning |
| Q2 SKU consolidation | Ethan | Henry | The SKU mapping table |
| Q3 Weather correlation | Steve | Henry | The weather API working |
| Q4 Stores and geography | Henry | Steve | Store id cleaning |
| Q5 Signal or artifact | Ethan | Steve | SKU and category cleanup |

Q1 and Q3 are the critical path.
Ethan starts date cleaning first, and Steve starts the weather API first.

Everyone reads all five questions, reviews at least one other person's code, and writes their own part of the reflection.

## 4. How we work

### Where we talk

Group chat for day-to-day messages.
We reply within 24 hours, and within a few hours on deadline days (Lab 09 on Oct 23, Lab 10 on Oct 30, presentation on Nov 2).
Code and decisions live in the GitHub repo, not in chat.

### When we meet

A recurring 1-hour meeting outside class, twice a week, on everyone's calendar.
Proposed slot: Sunday 7:00 PM and Thursday 7:00 PM (to confirm at our first meeting).
Each meeting covers: what got done, what is blocked, what each person does before the next meeting.

### How we decide

Look at the data first.
If we're still stuck, the owner of that part decides, and the decision goes in the decision log with the reason.

### Git workflow

- Pull before you start. Push before you stop.
- Personal work goes in `notebooks/scratch/<name>.ipynb`.
- Only the week's notebook owner commits to `notebooks/team_notebook.ipynb`.
- No keys or tokens in the repo. Open-Meteo needs none.

### If someone goes quiet

Check in after one day.
After two days, bring it to the whole team.
If still stuck, email Professor Williamson.
We don't wait until it's due.

## Signatures

By committing this file, each of us agrees to the charter above.

- Ethan
- Steve
- Henry
