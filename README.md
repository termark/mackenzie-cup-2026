# Mackenzie Cup 2026 – Herschel U13 Companion

A lightweight mobile-friendly tournament companion for the **2026 Mackenzie Cup U13 Girls Water Polo tournament** at Reddam House Constantia.

The app is focused on **Herschel U13A and U13B**, but also tracks all U13 pool results so it can calculate live group standings and project Herschel's likely knockout opponents.

## Live site

GitHub Pages:

https://termark.github.io/mackenzie-cup-2026/

GitHub repository:

https://github.com/termark/mackenzie-cup-2026

Official tournament PDF:

https://termark.github.io/mackenzie-cup-2026/Mackenzie-Cup-2026.pdf

## How to use

Open the live site on any phone or computer.

Use the tabs at the top:

- **Herschel A** – U13A fixtures, standings and projected knockout path
- **Herschel B** – U13B fixtures, standings and projected knockout path
- **All Herschel** – combined Herschel A/B schedule
- **Results** – enter or view all U13 pool results across Groups A–D
- **Simple** – fallback schedule planner that works without complete tournament results or editor access (this is now the default landing view)

Public visitors are **read-only** for the shared Results database, but anyone can use the **Simple** planner.

To update scores:

1. Tap **Editor sign in**
2. Sign in with an authorised Supabase user
3. Open **Results**
4. Enter any score you know
5. The shared standings and projections update automatically

Results are stored centrally in Supabase, so updates entered on one device are visible to everyone else using the site.

### Simple fallback mode

If nobody is able to capture all the other U13 results, the app is still useful.

Open **Simple**, choose **Herschel U13A or U13B**. The team's fixed pool matches are shown first; then select the team's final group position. The app shows the corresponding published knockout route. As Herschel plays each knockout game, select **Win** or **Loss** to reveal the next scheduled match.

This mode is stored locally in the browser and does **not** require Supabase authentication or knowledge of every other pool score. For knockout opponents, it shows the bracket placeholder (for example **2nd Group C**) unless the relevant shared group results are complete and the ranking is unambiguous; only then does it display the actual team name.


### Quick result import

The **Results** tab includes a bulk importer for fast score capture.

You can paste one result per line, for example:

```text
Oakhill Prep 3-5 Springfield
St Cyprians B 4-7 Herschel A
WGJS 6-6 Sun Valley Primary
```

This is useful when results arrive as a screenshot, WhatsApp message, or photo of a handwritten results sheet. A practical workflow is to transcribe/extract the visible scores into this simple text format and then use **Preview / edit**.

The preview is editable before submission:

- correct either score directly
- untick any match you do not want to submit
- see existing stored scores
- see when a proposed import would overwrite an existing result
- review any lines the parser could not recognise

After checking the preview, an editor uses **Approve & submit** to write the selected results to Supabase.

Only signed-in editors can submit imported results to Supabase.

## What the app calculates

The page tracks all U13 pool fixtures across Groups A–D and calculates:

- Played
- Won
- Drawn
- Lost
- Goals For
- Goals Against
- Goal Difference
- Points
- Current group position
- Herschel's projected quarter-final
- Current likely opponent
- Knockout route after Win / Loss results

U13 scoring follows the tournament rules:

- Win = 3 points
- Draw = 1 point
- Loss = 0 points

The official tie-break order is:

1. Head-to-head
2. Winner against the top team
3. Goal difference

Where a tie cannot be resolved safely from the entered data, the page marks the standings as provisional rather than inventing an order.

## Architecture

This is intentionally a very small stack:

```text
GitHub Pages
    ↓
index.html
HTML + CSS + vanilla JavaScript
    ↓
Supabase
Postgres + Auth + Row Level Security
```

There is no build system, package manager, framework or server-side application.

### Frontend

The site is a single static `index.html` file containing:

- HTML layout
- CSS
- tournament fixture data
- standings logic
- knockout mapping
- Supabase client integration
- local browser cache

It is hosted directly by **GitHub Pages**.

### Backend

**Supabase Free** provides:

- shared `match_results` table
- authentication for editors
- Row Level Security
- public read access
- authenticated write access

The browser uses a Supabase **publishable key** only. No database password or service-role key is embedded in the page.

### Sync model

- Public users read shared scores from Supabase
- Signed-in editors can insert/update results
- The page refreshes shared results periodically
- A local cache is kept in the browser for resilience

## Repository layout

```text
mackenzie-cup-2026/
├── index.html
├── Mackenzie-Cup-2026.pdf
└── README.md
```

## Source data

Tournament structure, fixture times, groups, scoring rules and knockout brackets were transcribed from the official **Mackenzie Cup Correspondence 2026** PDF supplied by the tournament organisers.

## Current version

**Page version: 0.8.5**

## Prize giving

- **Sunday 13 September 2026**
- **15:20 – Prize Giving**
- **15:30 – Tournament ends**
- Prize-giving dress code: **Summer uniform and blazers** (from school email)

## Notes

This is an unofficial parent-built companion page.

Always treat the official tournament communication as the authoritative source if there is any discrepancy.
