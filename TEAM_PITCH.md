# StartShield — Team demo and technical defence

## One-line pitch

**“Private start-ups don't have daily share prices. StartShield proposes public-market risk proxies, makes its assumptions visible, and models how an angel investor's liquid capital might reduce portfolio concentration under a technology shock.”**

## 90-second demonstration

1. Introduce Sarah, an angel investor with five illiquid stakes totaling **$400,000**, plus **$100,000** in cash. This is a fictional example; together the private stakes constitute **80%** of initial estimated wealth.
2. Click Sarah's preset. Point out the names, stake estimates and industry descriptions. Switch to historical Yahoo only if data connectivity works; the default is **fictional offline fixture**.
3. Run analysis and scroll to the Public Twins. Show that the system matches business exposures, explains the similarities and allows manual overrides. None of the match scores imply that private valuations track daily prices.
4. Show the **fixed** 30/30/20/20 example research basket, not an algorithmic optimiser. Explain per-holding limit at 15%.
5. Slide “technology falls” from 20% to 60%. The total estimated wealth changes in both liquid-cash scenarios. The difference is modeled, not a guarantee. Click **Recalculate scenarios** to fully recompute server-side.
6. Download the PDF and show the source label, method, stress comparison and limitations.

## What is genuinely implemented

Frontend, editable start-up inputs, validation, custom comparator overrides, optional Groq allowlisted matching, 40-name demo candidate catalog, optional actual 2022 yfinance return fetching, hypothetical private stress engine, deterministic eight-instrument allocation, interactive SVG, SQLite run history, PDF report, and automated tests.

## Defend the approach

**Q. Why use public twins?** Private valuations are sparse and subjective. Public twins provide observable proxy data, not validated private-company betas. We keep all twin choices editable and explicitly disclose uncertainty.

**Q. Isn't a 1.5x risk factor arbitrary?** Yes: it's a user-adjustable stress sensitivity, **not a calibrated or guaranteed minimum**, and the scenario allows a private-stake total wipeout.

**Q. How does AI improve this?** It helps interpret qualitative start-up descriptions and articulate reasons; an allowlisted schema prevents it from executing arbitrary trades or inventing market metrics. Offline heuristics also work without a model.

**Q. Is the portfolio optimised?** No. We deliberately chose a transparent fixed basket with 15% max holdings, and compare scenario outcomes. Actual optimisation would require constraints, estimation error controls and a suitability process.

**Q. Why doesn't a better 2022 result prove protection?** A stress scenario is a single historical mapping with strong simplifying assumptions. Crisis correlation can change, private stakes can fail for unrelated reasons, and liquid instruments can also lose money.

**Q. Can the judge try a made-up start-up?** Yes. Modify name/description/stake and rerun. If Groq is unavailable, the deterministic comparator matcher falls back and flags weak matches.

**Q. What would you improve?** Use licensed LSEG data, multi-factor private risk exposures, multiple crises and Monte Carlo with calibrated distributions, robust scenario optimisation, permissioned encrypted data, and backtests of residual concentration risk.

## Suggested division of responsibilities

- Product/pitch: Sarah story, investor journey and final judging narrative.
- Data: validate 2022 historical mode, source disclosure, demonstrate robust price retrieval.
- Quant: explain total-wealth algebra, shock scaling, asset constraints and uncertainty.
- Frontend: clickable demo, input forms, slider and report download.
- Integration: ensure offline fallback, tests and same-day run instructions.

**Rule for demo:** Prefer a functioning offline scenario over a broken live-data dependency. Never label fictitious 2022-like numbers as actual historical performance.
