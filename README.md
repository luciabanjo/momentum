# Momentum — Safety Reporting Journey

Momentum is an interactive prototype for closing the loop after someone reports a lived-safety concern.

The core journey is:

> **Report → Enrich & Insights → Watch & Outcome**

Someone can report something that happened or an area where they feel unsafe, see the report connected to relevant source data, understand the insights derived from that data, and later see what changed.

## Live prototype

[Open the current prototype](https://lived-safety-journey-mockup.luciatbanjo.chatgpt.site/)

The hosted prototype is public so it can be shared during the hackathon. Everything shown in it is synthetic and nothing is submitted or stored.

## What is implemented

### 1. Report

- A simple social-post-style reporting interface.
- Two report types: **Something happened** and **I feel unsafe here**.
- Anonymous-by-default language.
- Description, location and time fields.
- An illustrative attachment interaction.
- **Share report** is the demo's starting action and unlocks the next step.
- A short private-sharing transition before the connected picture opens.

### 2. Enrich & Insights

- A dark, animated source-data graph within the otherwise light interface.
- Seven synthetic source data points: the user's report, community reports, public posts, police data and street-lighting data.
- A staged enrichment sequence: the report appears first, then connected sources and links arrive progressively rather than being ready immediately.
- Force-style movement that lets the data points react to one another.
- Draggable points, background panning, scroll zoom and reset controls.
- Click-to-focus movement for any source point.
- A compact pop-up card anchored beside the selected point.
- A fuller detail panel showing the source, date, location, distance and why the data point is connected.
- Animated connection particles, glow and a starfield-like depth treatment.
- Derived insights presented **outside** the graph as separate cards once enrichment finishes.
- A clear **Watch this report** action that unlocks the final step.

The graph contains source data only. Patterns and conclusions belong in the separate insights layer.

### 3. Watch & Outcome

- A followed-report state opened from **Watch this report**.
- An outcome banner showing a synthetic positive change.
- A timeline showing what happened after the report.
- A contribution summary showing how the report became part of a wider evidence picture.
- Nearby support and safety resources, including a safe venue, specialist support and a safer route.

Support belongs on the Watch & Outcome screen, not in the source-data graph.

## Product decisions already made

- Keep the journey understandable as **Report → Enrich & Insights → Watch & Outcome**.
- Make reporting feel as easy and familiar as composing a social post.
- Keep the interface clean, light and gently rounded outside the graph.
- Use the graph for source records, not for derived insights or support resources.
- Let people inspect every source point and understand why it was connected.
- Treat connections as possible relationships, not proof that incidents, people or places are definitively linked.
- Close the loop by showing changes, status and useful support after a report.
- Preserve anonymity and user control as core product principles.

## Current technical shape

The prototype is deliberately lightweight:

- `dist/index.html` contains the HTML, CSS, synthetic data and vanilla JavaScript.
- `.openai/hosting.json` configures the static `dist` directory for ChatGPT Sites.
- There are no runtime dependencies or build step.
- There is no backend, database, authentication or real external data connection yet.

## Run locally

From the repository root:

```bash
python3 -m http.server 4173 --directory dist
```

Then open [http://127.0.0.1:4173](http://127.0.0.1:4173).

## Repository structure

```text
.
├── .openai/hosting.json  # Static Sites configuration
├── AGENTS.md             # Decisions, guardrails and next implementation work
├── README.md             # Project overview and local setup
└── dist/index.html       # Complete working prototype
```

## Current limitations

- All reports, connections, insights, outcomes and resources are synthetic.
- Submitting a report does not send or persist anything.
- The graph is a small in-browser simulation rather than a production graph service.
- Watching does not create a real subscription or notification.
- External-source provenance, permissions, deduplication and confidence are not implemented.
- Safety moderation, safeguarding escalation and abuse prevention are not implemented.
- The support links are illustrative.

## What comes next

The next implementation should make one thin, data-driven vertical slice work without changing the approved journey or visual hierarchy. Start by defining the data model and rendering the existing prototype from structured fixture data. Then add safe report persistence, source adapters, explainable insights and the watch/outcome loop in that order.

See [AGENTS.md](AGENTS.md) for the detailed handoff and acceptance checks.

## Safety note

This is a product prototype, not an emergency-reporting service. A production version must clearly distinguish community safety reporting from emergency or police reporting and must complete privacy, safeguarding, legal and data-governance review before handling real reports.
