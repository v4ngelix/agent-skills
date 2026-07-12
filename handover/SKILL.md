---
name: handover
description: Produce a tight, self-contained handover note that lets a brand-new chat pick up the current task without seeing this conversation. Use this whenever the user wants to continue work in a fresh chat, start a new conversation, hand off context, or is running low on context window — triggered by phrases like "handover", "hand-off", "handoff note", "continue in a new chat", "fresh chat", "carry this over", "transfer the context", "summary to start a new conversation", or "pick up where we left off". Use it even when the user phrases the request loosely, as long as the goal is to seed a new chat with the state of the current work.
---

# Chat Handover

The user is about to continue this work in a brand-new chat where the next assistant sees none of the current conversation. The job is to write the smallest possible note that lets that fresh assistant continue seamlessly: what the task is, where it stands now, what's been decided, what to avoid, and what comes next.

A handover is a snapshot of the present and a pointer to the future. It is NOT a diary of the past.

## Output rules (read first — these are the whole point)

1. **Output ONLY the handover, inside a single fenced code block. Nothing else.** No preamble ("Here's your handover note:"), no sign-off, no explanation before or after the block. The user wants to copy the block and paste it straight into a new chat. A single line of chatter defeats that.
2. **Wrap the entire handover in one ``` code block** so it copies cleanly as raw text.
3. **Light structure — include only the sections that carry real information.** Drop any section that would be empty or filler. A short handover with three sections beats a padded one with six.
4. **Precise and concise.** Concrete nouns over vague summary: real file names, identifiers, versions, numbers, decisions. Cut adjectives, hedging, and throat-clearing.
## What to put in (only the sections that apply)

Use plain labels, in roughly this order. Skip any that don't apply.

- **Task** — one line naming what is being built/written/solved. Always include this; without it the new chat is blind.
- **Goal** — the concrete outcome the new chat should reach. Include if it adds information beyond the task line.
- **Current state** — where things stand *right now*, in present tense. The live approach, what's settled, what's in progress. This is the spine of the handover.
- **Decisions & constraints** — settled choices, requirements, conventions, and user preferences the new chat must honor so they aren't re-litigated (e.g. "uses Postgres, not SQLite"; "tone stays formal"; "no external libraries").
- **Avoid** — approaches already ruled out, one terse line each. Include ONLY where the new chat would plausibly re-attempt them. State the approach and, in a few words, why it's out. This is the only place the past appears, and only because it saves wasted effort.
- **Next** — the immediate next step(s), concrete and actionable.
- **References** — files, paths, links, names, or values the new chat needs to know exist. Skip if there are none.
## What to leave out (this is where handovers usually go wrong)

- **No history-as-narrative.** Do not write "we tried X, then I did Y, then it worked." The new chat does not need the journey. Convert any such narration into its end state: keep the current approach under *Current state*, and demote only the still-relevant failures to *Avoid*.
- **No accomplishment log.** "We successfully implemented auth and fixed the bug" is past tense and adds nothing forward-looking — delete it. If auth is done, that's just part of *Current state* ("auth is in place"); if the bug's fix matters, capture the resulting constraint, not the event.
- **No restating of the obvious or generic advice.** The receiving assistant is capable; don't pad with instructions it doesn't need.
- **No meta-commentary** about the handover itself.
## Template

Fill this in, then delete every label you didn't use. Output exactly one such block and nothing around it.

```
Task: <one line — what this is>
Goal: <the outcome to reach>
 
Current state:
- <where it stands now, present tense>
- <current approach / what's settled / what's mid-flight>
 
Decisions & constraints:
- <settled choice or requirement to honor>
 
Avoid:
- <ruled-out approach> — <why, in a few words>
 
Next:
- <immediate, concrete next step>
 
References:
- <file / path / link / name the new chat needs>
```

## Example

**Bad** (narrates history, brags about progress, chatter outside the block):

Here's a handover for you!
```
We started by trying to use a CSV parser but it choked on the quoted commas,
so we switched to pandas and that worked great. We've now successfully cleaned
all 12k rows and built three charts. It took a while but the dashboard looks
really good now.
```

**Good** (present state + what's left + the one dead-end worth flagging, nothing else):

```
Task: Sales dashboard from the raw export in data/sales_2025.csv.
Goal: Interactive dashboard with revenue-by-region and month-over-month trend.
 
Current state:
- Data is cleaned and loaded via pandas; 12,043 rows, no nulls remaining.
- Revenue-by-region and MoM-trend charts are built (Plotly).
 
Decisions & constraints:
- Plotly for charts, not matplotlib (interactivity needed).
- Region names normalized to the 5 canonical values in references below.
 
Avoid:
- Python's csv module for ingest — it mis-splits the quoted, comma-containing
  address field. Use pandas.read_csv.
 
Next:
- Add the per-rep leaderboard chart, then assemble the three into one HTML page.
 
References:
- Canonical regions: North, South, East, West, Central.
- Working notebook: dashboard.ipynb.
```

Notice the good version never says what *happened* — only what *is* and what's *next*. The CSV dead-end survives solely because the new chat might otherwise repeat it.
