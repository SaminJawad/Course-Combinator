# Course Combinator

A single-file web app that turns a university faculty/section-list PDF into a clash-free class routine - built for the EWU course-tracker export format (Course · Sec · Faculty · Capacity · Timing · Room), but adaptable to similar layouts.

**Live demo:** [course-combinator.netlify.app](https://course-combinator.netlify.app)

Upload the PDF once each semester, pick your courses, and get ranked, clash-free combinations, complete with a visual weekly calendar, a per-day quality score, and one-click PNG downloads of any routine you like, so the "best" schedule is never a guess.

## Why this exists

Manually cross-referencing a 100+ page faculty list to find a schedule that doesn't clash — and doesn't leave you with brutal gaps between classes is tedious and error-prone. This tool automates it: parse the PDF, generate every valid clash-free combination for your chosen courses, and rank them by a transparent, weighted scoring system.

## Features

- **Drag-and-drop PDF upload** - parses course, section, faculty, capacity, timing, and room straight from the source PDF, entirely in the browser (nothing is uploaded to a server).
- **Smart combination generation** - automatically produces every possible clash-free combination of sections for your selected courses.
- **Lock in an already-registered section** - mark a course as already taken and pin its exact section; every combination builds around it. For courses you haven't registered yet, you can still set a preferred section that's tried first.
- **Transparent, weighted day scoring.** Each weekday (Sun–Thu) is evaluated flag-by-flag:
  - **Worst** (−8 pts each) - 4+ classes in a day, or a gap that's either too tight (<15 min) or wastes the whole day (≥180 min)
  - **Carry** (+3 pts each) - manageable but not ideal: exactly 3 classes, or a ~90-minute gap
  - **Okay / FUNDAY** (+10 pts each) - 2 or fewer classes with gaps in the productive 30–119 minute range, or a day with no classes at all

  Flags stack - a day with two Worst issues counts twice - and combinations are ranked by **highest total weighted score** across the week.
- **Built-in explainer** - a `?` tooltip next to the results explains exactly how the scoring works.
- **Visual weekly calendar** - every combination can be viewed as an actual calendar grid, including same-hour overlapping classes or labs shown as stacked slices rather than silently hidden.
- **Download any routine as a PNG** - one click exports a clean, shareable image of the calendar view, drawn to match the on-screen design exactly.
- **Search-as-you-type course picker** - quickly find and select courses from the parsed list.
- **Paginated results** - browse every valid combination (not just the top-ranked ones), five at a time, each with its own expandable calendar and download button.


## How it works

1. **Parsing** - PDF.js runs client-side to extract text from the uploaded PDF, which is then parsed into structured course/section/faculty/timing data.
2. **Combination generation** - the app builds every possible clash-free combination of sections across your selected courses, respecting any locked or preferred sections.
3. **Scoring** - each combination is evaluated day-by-day using the Worst/Carry/Okay/FUNDAY rules above, and a total weighted score is computed across the week.
4. **Ranking & display** - combinations are sorted by score; the highest-scoring ones appear in "Your best combinations," and every valid combination is browsable (paginated) in "All clash-free combinations."
5. **Export** - the calendar for any combination can be downloaded as a PNG, drawn directly with canvas so it always matches the on-screen grid.

## Privacy

The uploaded PDF is processed entirely client-side in your browser. It is never sent to a server. There's no backend, no analytics, and no data collection.

## Tech notes

- Single HTML file with PDF.js and Roboto embedded for portability.
- No frameworks, no build tools, no dependencies to install.
- Calendar PNG export is drawn directly with the Canvas API (not a DOM screenshot) — Chromium treats any canvas populated from an SVG `<foreignObject>` containing HTML as "tainted" and blocks its export, even for local/same-origin content, so the grid's layout is deliberately recomputed against canvas drawing primitives instead.
- Works by opening the file directly or hosting it anywhere as a static file.

## License

Licensed under the [Apache License 2.0](LICENSE).
