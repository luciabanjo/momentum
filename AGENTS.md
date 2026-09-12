# Agent Handoff

This file tells future agents what is already decided, what exists, and what to implement next.

## Start here

1. Read `README.md`.
2. Open `dist/index.html` locally and walk through all three screens.
3. Preserve the approved product decisions below unless Lucia explicitly changes them.
4. Keep the current prototype working while replacing synthetic behaviour incrementally.

## Approved product journey

The product journey is:

> **Report → Enrich & Insights → Watch & Outcome**

The purpose is not reporting for its own sake. A person should be able to share a safety concern, see how it connects to a wider evidence picture, follow what develops and understand what changed.

## Non-negotiable interface decisions

- The report composer should remain simple, familiar and low effort.
- The source-data graph contains data points only.
- Derived insights live outside the graph.
- Every graph point can be selected and inspected.
- Selecting a point should focus it, show the anchored pop-up and update the full detail panel.
- Support and nearby resources live on the Watch & Outcome screen.
- The user's report must remain visually identifiable in the graph.
- New source records should be visibly distinguishable when the graph grows.
- Connections must show provenance and an understandable reason for the match.
- A connection is a lead or possible pattern, never proof that events or people are linked.
- Preserve the current light, spacious visual system and the graph's darker, glowing interaction surface.

## Current implementation

The complete prototype is in `dist/index.html` and uses plain HTML, CSS and JavaScript.

It currently provides:

- a synthetic anonymous reporting flow;
- a seven-point interactive force-style graph;
- node dragging, graph panning, zooming and reset;
- click-to-focus graph movement;
- an anchored selected-node pop-up;
- a synchronized full source-detail panel;
- separate insight cards;
- a watch control, outcome banner and event timeline; and
- illustrative nearby support resources.

There is no real persistence, enrichment, identity, moderation, notification or outcome ingestion.

## Implement next

### Priority 1 — make the existing experience data-driven

Do this before connecting live services.

1. Define explicit schemas for:
   - `Report`
   - `SourceRecord`
   - `Connection`
   - `Insight`
   - `WatchState`
   - `OutcomeEvent`
   - `SupportResource`
2. Move the current synthetic content into structured fixture data.
3. Render nodes, edges, detail cards, insights and outcomes from that data rather than hard-coded markup.
4. Keep the current screens and interactions visually equivalent.
5. Add stable IDs, timestamps, source names, provenance URLs where permitted, location precision, connection reasons and confidence/uncertainty fields.

The first milestone is complete when changing one fixture updates the graph, detail panel, insights and outcome screens without editing their HTML.

### Priority 2 — create a safe report-submission vertical slice

1. Add a server endpoint and durable storage for a report.
2. Store the minimum necessary data.
3. Separate any account identity from report content.
4. Round or otherwise protect precise locations by default.
5. Add consent and retention fields for attachments and sensitive text.
6. Add rate limiting, validation, abuse controls and an audit trail.
7. Make the UI honest about what is stored, who can see it and whether it is shared.

Do not add real attachments until access control, retention and deletion behaviour are defined.

### Priority 3 — add enrichment through source adapters

Build one adapter at a time behind a common interface. Suggested order:

1. existing first-party community reports;
2. police open data at an appropriately aggregated location level;
3. council or street-maintenance open data;
4. permitted public community or social sources.

Every imported source record must retain:

- provider and source type;
- original publication or record time;
- ingestion time;
- geographic precision;
- licence/usage basis;
- provenance reference;
- match reason; and
- confidence or uncertainty.

Add deduplication and do not imply that nearby records describe the same person or event.

### Priority 4 — derive explainable insights

1. Compute insights from connected source records, not from presentation copy.
2. Keep insight logic separate from the graph data.
3. Show which records support an insight.
4. Include caveats for small samples, incomplete coverage and reporting bias.
5. Recompute or retire insights when the source picture changes.

Do not render an insight as a graph node.

### Priority 5 — implement watching and outcomes

1. Persist a person's watch state.
2. Add newly matched sources to the watched picture with a clear “new” state.
3. Record status and outcome events with source, timestamp and evidence.
4. Notify only about meaningful changes and give the person control over the channel and frequency.
5. Distinguish confirmed outcomes from pending, reported or inferred changes.
6. Populate support resources from a verified, maintained directory with opening hours and distance.

Do not place support-resource records in the source-data graph.

## Safety, privacy and data rules

- Keep the synthetic-data label until real data is genuinely connected.
- Never invent source records, outcomes or official action in a real-data environment.
- Avoid displaying exact incident coordinates to other users.
- Do not expose report author identity in graph data.
- Do not scrape or republish private-group content.
- Record provenance and permissions for every external source.
- Provide deletion, correction and appeal routes before production use.
- Add a clear emergency-services signpost; do not imply this product replaces emergency or police reporting.
- Complete safeguarding, privacy, security, legal and data-protection review before accepting real sensitive reports.

## Engineering guidance

- Preserve `.openai/hosting.json` and its existing project ID unless Lucia explicitly moves the deployment.
- `dist` is authored source in the current buildless prototype; do not add it to `.gitignore`.
- Do not commit credentials, `.env` files, private reports, downloaded datasets or local databases.
- Prefer small vertical slices over a broad platform rewrite.
- If introducing a framework or build step, reproduce and verify the existing experience before replacing the static file.
- Keep source adapters, matching logic, insight generation and presentation as separate concerns.
- Treat accessibility, keyboard operation, mobile layout and reduced-motion behaviour as release requirements.

## Validation for every change

At minimum:

1. Start the local site with `python3 -m http.server 4173 --directory dist`.
2. Complete the Report → Enrich & Insights → Watch & Outcome journey.
3. Confirm all graph points can be selected.
4. Confirm selection updates the pop-up and full detail panel.
5. Confirm points can be dragged and the graph can be panned, zoomed and reset.
6. Confirm insights remain outside the graph and support remains on Watch & Outcome.
7. Check desktop and mobile layouts, keyboard access and reduced-motion behaviour.
8. Check the browser console for errors.

## Definition of done for the next milestone

The next milestone is done when the current synthetic journey is rendered entirely from validated structured data, with no regression to the approved layout or interactions, and the data contracts are ready for a safe report-storage endpoint and the first enrichment adapter.
