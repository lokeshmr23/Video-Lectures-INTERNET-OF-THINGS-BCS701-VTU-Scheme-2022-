# BCS701 — Internet of Things (VTU Scheme 2022)

Promotional site for the free module-wise video lecture series, notes, solved
papers and the 12-experiment lab.

Third site in the same family as BCS702 (Parallel Computing) and BCS703
(Cryptography & Network Security) — identical design system and behaviour.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole site — one self-contained file (inline CSS + JS) |
| `dr_lokesh_professor_new.png` | Portrait used in the hero and the teacher section |
| `render.yaml` | Render Blueprint (static site + cache/security headers) |
| `robots.txt` | Search-engine crawl rules |

## Run locally

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

Open it through a server, not by double-clicking: YouTube refuses to embed on
`file://` pages.

## What is on the page

| Section | Content |
| --- | --- |
| Hero | free series badge, 5 modules / 40 lectures / 12 lab experiments / CO1–CO5 |
| Why students use it | 3 value cards |
| The series | course facts, featured player, search, watched progress |
| Module 1–5 accordions | 40 lectures + per-module notes, slides and solved papers |
| **Practical component** | laboratory manual button + 12 lab experiments (E1–E12), each with a video |
| Study planner | days left + hours/day → day-by-day schedule |
| Exam guide, teacher, resources, FAQ, final CTA | as in the other two sites |

## Where the content lives

At the top of the `<script>` block:

```js
const MODULES = [{ id, title, hours, co,
                   notes:  "https://doi.org/10.5281/zenodo.…",   // module notes
                   slides: "https://drive.google.com/file/d/…",  // classroom deck
                   pyq:    [{ label:"Dec 25 – Jan 26", url:"…" }], // solved papers
                   lectures: [{ code, topic, url }, …] }, …];
const LAB = [{ code:"E1", topic:"Blink 5 LEDs back and forth", url:"…" }, …];
const PLANNER = { multiplier: 3, perModuleBaseHours: [8,8,8,8,8] };
```

- **Add a lecture** → add a `{code, topic, url}` entry to that module.
- **Add notes / slides / a solved paper** → fill `notes`, `slides` or push into
  `pyq`. The pills appear automatically; leave them out and nothing renders.
- **Add an experiment** → append to `LAB`. The grid re-flows by itself.
- **Change planner maths** → `PLANNER.multiplier` (3 = watch + notes + practise).

## Current data

- 5 modules · **40 lectures** (8 per module, M1-L1 → M5-L8)
- **12 lab experiments** (E1–E12), all with videos
- Module CO mapping: M1 → CO1, M2 → CO2, M3 → CO3, M4 → **CO2 & CO3**, M5 → CO5
- 5 module notes (Zenodo DOIs) + 5 classroom presentations (Google Drive)
- 2 solved previous-year papers, both on Module 1: Dec 25 – Jan 26, Jun – Jul 26
- 8 hours per module · 12-hour practical · Scheme 2022 · 4 credits
- Laboratory manual (experiment-wise CO mapping) → Google Drive PDF, linked as a
  button at the top of the Practical component section

## Deploy to Render

Same as the other two: **static site**, Root *(empty)*, Build *(empty)*,
**Publish Directory `.`**.

`render.yaml` is a Blueprint file, not a publish directory.

## Placeholders to fill

| Placeholder | Where | What to supply |
| --- | --- | --- |
| `[Add institution]` | teacher section, footer | college / university name |
| canonical / `og:url` | `<head>` | the real deployed URL — currently `https://video-lectures-internet-of-things.onrender.com/` as a **guess** |

## Data notes

- Every lecture has its own video: 40 lectures, 40 unique video ids. Module 3
  was corrected on request — M3-L1 now points at `bmxTFOYfpaU` and M3-L4 at
  `BYce1o5qQBA`, so nothing shares a recording any more.
- Tracking parameters (`?si=…`) were stripped from every URL; the video ids are
  unchanged.
- Titles were lightly normalised (capitalisation, trailing punctuation) but the
  wording is the author's.
