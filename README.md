# HomeGuard — Contractor Quote Analyzer Prototype

An AI-powered homeowner decision assistant. This is the scoped-down Phase 1 prototype: a contractor quote analyzer plus a minimal home record with an accuracy-tracking log, built to validate the core idea before expanding.

## What this is

Open `index.html` in a browser (works locally or hosted — e.g. GitHub Pages).

- **Review a contractor quote** — paste quote text and/or attach a photo. The page calls the Anthropic API directly (`fetch` to `https://api.anthropic.com/v1/messages`) to extract structured fields and produce a decision-oriented review: assessment vs. a reference cost range, issues worth clarifying, questions to ask the contractor, and a recommendation.
- **Reference pricing is grounded, not invented** — the model is only allowed to compare totals against 4 categories sourced from published 2026 home-services cost guides (HVAC replacement, water heater replacement, roof replacement, electrical panel upgrade). Anything outside those categories is honestly flagged as "no reference data" rather than guessed.
- **Home record & accuracy log** — saved quotes persist via the artifact storage API and can be reviewed later; each one can be marked "accurate" or "was off" so the tool's real-world track record builds up over time.
- **Evidence tagging** — every extracted field is labeled Verified / Inferred / Unknown so it's clear what came from the document vs. what the model inferred.
- **Honest failure states** — malformed model output, HTTP errors, and network failures all route to a clearly labeled `NOT VERIFIED` error screen rather than showing fabricated data.

## Explicitly NOT in this prototype

- Photo-based problem diagnosis and warranty checking (shown on the home screen but marked "Not in this prototype")
- Real accounts / multi-user database — storage is tied to this artifact/browser, not a backend
- Location-adjusted or licensed pricing data — only 4 project categories have any reference range at all

## Background

Built from a product brief for a full-featured "AI home decision engine" (diagnosis + quotes + warranties + home health score). Market research found that most of those individual features already exist as free or well-funded competitors (photo diagnosis, quote benchmarking, warranty tracking all have direct competitors). This prototype deliberately narrows to the single highest-value, lowest-competition loop — quote analysis tied to a persistent, growing home record — rather than building the full spec at once.
