# What this project is

`stock-picker` is a research workspace for producing transparent, repeatable stock-watchlist ideas. It is not an investment-advice service or an execution system. Every conclusion must be tied to dated evidence, state assumptions clearly, and distinguish facts from interpretation.

Planned project files (name these before creating or relying on them):

- `README.md` — scope, ownership, and how to run the workflow.
- `principles.md` — defensible principles for one-week stock selection, including rejected ideas.
- `rules.md` — class-universe constraints, position limits, shorting policy, and the required trade schema.
- `universe.csv` — the symbols and basic metadata eligible for screening.
- `screening-config.yaml` — the thresholds, exclusions, and lookback periods used by the screen.
- `research-notes.md` — dated company-level evidence, source links, and open questions.
- `screen-results.csv` — generated output from the screen; do not hand-edit it.

# Which files to read before doing anything

Read `AGENTS.md` first, then read `principles.md` for the project's one-week trading logic and rejected ideas, `rules.md` for the allowed universe, position limits, shorting policy, and exact output schema, followed by `README.md` for project scope and commands. Before screening, inspect `screening-config.yaml` and `universe.csv`; before explaining or ranking a company, read its relevant entries in `research-notes.md` and the latest `screen-results.csv`. If a named file is missing, say so and stop rather than inventing its contents. Treat generated files as outputs and preserve existing changes unless the requester explicitly asks for a rewrite.

# What to do when someone asks for stock picks

Follow this sequence every time:

1. Clarify the request's constraints (market, investment horizon, risk tolerance, sector restrictions, currency, and whether the user wants ideas or a portfolio allocation). If a constraint is absent, state a conservative assumption; do not present personalized advice.
2. Read `principles.md`, `rules.md`, `README.md`, `screening-config.yaml`, `universe.csv`, `research-notes.md`, and the latest `screen-results.csv` in that order. Apply the principles' one-week scope and rejected-idea warnings, then enforce every universe, exposure, shorting, and formatting rule before ranking anything. Record the data timestamp and note any missing or stale inputs.
3. Run the repository's documented screening command from `README.md`. Verify the command completed successfully, the universe is non-empty, and every selected symbol passes the configured liquidity, valuation, quality, and risk checks. Never silently change thresholds.
4. For each surviving symbol, perform a freshness and sanity check: confirm the ticker and listing, check recent price/market-cap data, review the latest earnings and material company news, look for debt, dilution, regulatory, concentration, and event risks, and cross-check at least two independent primary or reputable sources. Cite URLs and publication dates in `research-notes.md`.
5. Compare candidates against the stated constraints. Remove names with unresolved data gaps or a thesis that depends on unsupported forecasts. Explain both the bull case and the principal failure case; do not use certainty language or promise returns.
6. Start the answer with the exact YAML trade-list schema in `rules.md`; do not put prose before it. After the YAML, include: **Assumptions and data timestamp**; **Shortlist** (ticker, company, thesis, key metrics, catalysts, risks, five-day deadline, and what would invalidate the thesis); **Comparison** (why each candidate fits the constraints); **Checks and sources** (commands run, pass/fail notes, and dated links); and **Next steps** (questions to investigate and a reminder to verify current information). Include a clear educational-not-personalized-advice disclaimer.
7. If current market data or source verification is unavailable, say that the result is incomplete and provide a watchlist or research plan instead of fabricating numbers.
