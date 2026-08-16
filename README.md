# Course Combinator

A web app that turns a university course selection list PDF into a clash-free class routine — built for the EWU (Course · Sec · Faculty · Capacity · Timing · Room), but adaptable to similar layouts.

**Try it instantly:** [course-combinator.netlify.app](https://course-combinator.netlify.app) — no setup required.

Upload the PDF once each semester, pick your courses, and get ranked, clash-free combinations — complete with a visual weekly calendar and a per-day quality score, so the "best" schedule is never a guess.

## Why this exists

Manually cross-referencing a 100+ page faculty list to find a schedule that doesn't clash — and doesn't leave you with brutal gaps between classes — is tedious and error-prone. This tool automates it: parse the PDF, generate every valid clash-free combination for your chosen courses, and rank them by a transparent scoring system.

## Features

- **Drag-and-drop PDF upload** — parses course, section, faculty, capacity, timing, and room straight from the source PDF, entirely in the browser (nothing is uploaded to a server).
- **Smart combination generation** — automatically produces every possible clash-free combination of sections for your selected courses.
- **Transparent day-quality scoring.** Each weekday (Sun–Thu) gets a status chip:
  - **Worst** — 4+ classes in a day, or a gap that's either too tight (<15 min) or wastes the whole day (≥180 min)
  - **Carry** — manageable but not ideal: exactly 3 classes, or a ~90-minute gap
  - **Okay** — 2 or fewer classes with gaps in the 30–119 minute sweet spot
  - **FUNDAY** — no classes at all that day; free time, never counted against a combination

  Combinations are ranked by fewest **Worst** flags first, then fewest **Carry** flags, then by the largest single-day gap.
- **Built-in explainer** — a `?` tooltip next to the results explains exactly how the scoring works.
- **Visual weekly calendar** — every combination can be viewed as an actual calendar grid, not just a list.
- **Search-as-you-type course picker** — quickly find and select courses from the parsed list.

## Getting started

1. Open [course-combinator.netlify.app](https://course-combinator.netlify.app)
2. Upload your faculty/section-list PDF.
3. Search and select the courses you want to take.
4. Browse the ranked, clash-free combinations and pick your favorite.

No build step, no installation, no backend.

## How it works

1. **Parsing** — PDF.js runs client-side to extract text from the uploaded PDF, which is then parsed into structured course/section/faculty/timing data.
2. **Combination generation** — the app builds every possible clash-free combination of sections across your selected courses.
3. **Scoring** — each combination is evaluated day-by-day using the Worst/Carry/Okay/FUNDAY rules above.
4. **Ranking & display** — combinations are sorted by score and rendered as both a list and an interactive calendar view.

## Privacy

The uploaded PDF is processed entirely client-side in your browser — it is never sent to a server. There's no backend, no analytics, and no data collection.

## Tech notes

- Single HTML file with PDF.js and Roboto embedded for portability.
- No frameworks, no build tools, no dependencies to install.
- Works by opening the file directly or hosting it anywhere as a static file.

## License

Licensed under the [Apache License 2.0](LICENSE).
