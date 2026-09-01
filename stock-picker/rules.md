# Trading rules

## Objective and holding period

This project looks for aggressive, profit-focused trades expected to play out over about five trading days. Every trade must still follow the limits below. “Highest expected profit” means the strongest setup that passes the rules; it is not a guarantee of profit.

## Class universe constraint

trades only settle on tickers in the class universe — US-listed stocks and ETFs (S&P 500, NASDAQ-100, and the class ETF list). Want a ticker added? Ask, with a reason.

Do not recommend or submit an out-of-universe ticker. If eligibility cannot be confirmed, mark the candidate `ineligible` and omit it from the trade list.

## Position limits

- Maximum open positions: 5 total.
- Long position size: normally 10–15% of total portfolio value; hard maximum 20% in one ticker.
- Short position size: normally 5% of total portfolio value; hard maximum 10% in one ticker.
- Maximum simultaneous shorts: 2.
- Maximum combined short exposure: 20% of total portfolio value.
- Maximum combined exposure: 100% of total portfolio value. No leverage or borrowed buying power.
- Maximum positions from one industry: 2, even if the tickers are in different indexes.
- Keep at least 10% cash unless an existing sell and a new buy settle together.
- Never average down. A losing position may not be increased during its five-day holding window.

`size_pct` always means the trade's absolute notional value as a percentage of total portfolio value. For example, selling half of a 20% position is `action: sell` and `size_pct: 10`.

## Is shorting allowed?

Yes, shorting is allowed only for eligible class-universe tickers. A short must have a specific negative catalyst, confirming downward price action, and enough liquidity to enter and cover. Do not short solely because a stock looks expensive. Do not short leveraged or inverse ETFs, and do not open a short if the position or exposure limits above would be exceeded.

## Recommendation checks

Before recommending a trade:

1. Confirm the ticker is in the class universe.
2. Apply `principles.md`, including its catalyst, liquidity, confirmation, and five-day exit rules.
3. Check current open positions so the new trade does not violate ticker, industry, short, cash, or total-exposure limits.
4. Choose exactly one action: `buy`, `sell`, or `short`.
5. Use an integer `size_pct` within the limits. Never use vague sizes such as “small” or “half.”
6. Write one sentence explaining the catalyst and the confirming price or volume signal. Do not say only that the stock “will go up” or “will go down.”
7. If no candidate passes every check, output `NO_TRADE` rather than forcing a pick.

## Required recommendation format

Return only this YAML trade list first, with no introductory prose. Repeat the four keys in this order for every recommendation:

```yaml
trades:
  - ticker: AAPL
    action: buy
    size_pct: 15
    rationale: "A fresh earnings beat and raised guidance were confirmed by above-median volume and a close above the pre-report price."
```

Formatting rules:

- `ticker`: uppercase exchange symbol without `$`.
- `action`: exactly `buy`, `sell`, or `short` in lowercase.
- `buy` opens/adds to a long or covers an existing short; `sell` reduces a long; `short` opens/adds to a short.
- `size_pct`: whole number from 1 through the applicable maximum; no percent sign.
- `rationale`: exactly one sentence, quoted, with no line breaks.
- Multiple trades are separate items under `trades`.
- If nothing qualifies, output exactly:

```yaml
trades: []
status: NO_TRADE
reason: "No eligible ticker passed every required check."
```

After the YAML block, add a short human-readable section listing the five-day deadline and invalidation condition for each trade. The YAML block itself must remain clean and contain no commentary or Markdown table.
