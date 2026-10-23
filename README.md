# StartShield — protect the portfolio you can't sell

**Evidence-aware concentration risk explorer for angel investors** | Standalone hackathon MVP, v1.0.

## The problem

Angel investors often hold multiple private stakes exposed to similar drivers, such as AI capital spending, SaaS budgets and venture financing. These private holdings rarely have timely, continuously observable prices. StartShield **does not pretend otherwise**. It uses transparent public-company comparators to explore possible concentration exposures, then models two hypothetical ways to invest spare liquid capital.

## Live product flow

1. Enter 1–10 private startups with short descriptions and **investor-estimated stakes**.
2. Match two–three public-company risk proxies using approved keyword heuristics, manually entered tickers, or an optional **Groq-assisted allowlisted match**.
3. Retrieve (a) **clearly fictional offline return fixtures** or (b) actual Yahoo Finance adjusted **2022 historical returns**, never mixing the two.
4. Stress public proxies under a variable tech-market shock using an explicitly disclosed QQQ-relative scaling assumption. Multiply the private proxy shock by an editable 1.0–3.0x uncertainty factor, with private losses bounded at 100%.
5. Compare the investor's total modeled wealth for two **different uses of the same liquid cash**: a tech-heavy QQQ comparison, or an illustrative four-sleeve / eight-holding research basket.
6. Inspect source provenance, candidate assets, comparator reasons, stress curves and an automatically generated two-page PDF. SQLite saves reproducible inputs, results and report locations.

## IMPORTANT caveats

- **No actual private-company prices.** Estimates are assumed stake values entered by the investor. Public comparators are subjective, not validated risk models.
- **Not an optimizer.** The allocation is a *fixed example* with 30% short Treasuries, 30% defensive sectors, 20% real assets and 20% international/value equities, max 15% per holding.
- **Not a hedge contract, suitability recommendation or investment advice.** Sector/cash-like funds may lose value. Startups can fail completely irrespective of any public twin.
- **2022-like DEMO returns are entirely fictional.** Do not quote them as realized equity returns. Historical yfinance mode needs internet access and is not certified exchange data.
- Scenarios linearly scale 2022 returns relative to QQQ, rather than forecasting joint shock distributions. Cross-asset correlations, asymmetric exposures, liquidity, FX, transaction costs, fees, tax and borrowing are not modeled.
- Past crises do not predict future risk; a 1.5x stress multiplier is an **assumption**, not a calibrated lower bound.
- **No trades executed.** The application has no brokerage connections.
- Yahoo Finance data may have restrictions on redistribution and commercial deployment. Licensed provider integration is required for a commercial LSEG product.
- When optional Groq is enabled, startups' descriptions and stake data are sent to an external provider. Do not input real confidential portfolio information without permission.

## Quick Windows installation

See [START_HERE.md](START_HERE.md). Commands:

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m pytest -q
python -m uvicorn startshield.api:app --app-dir src --reload --port 8002
```

Visit http://127.0.0.1:8002/ or http://127.0.0.1:8002/docs.

### Groq, optional

1. Copy `.env.example` to `.env`.
2. Set `GROQ_API_KEY` and optionally `GROQ_MODEL=openai/gpt-oss-20b`.
3. Restart Uvicorn and tick the Groq option. If model requests fail, fallbacks are labelled.

## Technology

Frontend: HTML, CSS, vanilla JS + inline responsive SVG chart. Backend: FastAPI, Pydantic, Python deterministic engine, SQLite. Visualization: Matplotlib (PDF), SVG (browser). Report: ReportLab. History: yfinance optional; Groq SDK optional. Tests: pytest + FastAPI TestClient, no API key or internet required for test suite.

## Security and data-integrity design

- Users may override comparator tickers **only from the approved catalog**.
- Groq's comparator proposals must return an exact JSON schema, approved ticker IDs, and complete startup coverage. Invalid proposals are discarded wholesale.
- Financial computations receive only validated request objects and historical or clearly synthetic returns.
- A SHA-256 digest records the market return snapshot and provider/period label.
- An optional LLM explanation is never used as input for portfolio mathematics.
- Failed live-market downloads return an error, **never fabricated market values**.
- SQLite keeps data and research history locally. The PDF path is saved after report generation.

## Key source files

| File | Responsibility |
|---|---|
| `src/startshield/models.py` | Validated request contracts |
| `src/startshield/catalog.py` | 40-stock/ETF research universe and fixed allocation |
| `src/startshield/matching.py` | Offline qualitative public twin matching |
| `src/startshield/llm.py` | Optional validated Groq matching and narrative |
| `src/startshield/market.py` | Historical yfinance or explicitly synthetic market returns |
| `src/startshield/engine.py` | Deterministic modeled stresses, asset screening and total wealth comparison |
| `src/startshield/reporting.py` | PDF with source labels, table and scenario chart |
| `src/startshield/storage.py` | SQLite runs and reports |
| `src/startshield/api.py` | FastAPI, demo, analysis, reports and history |
| `static/` | Standalone financial-services dashboard |
| `tests/` | Automated unit, integration and end-to-end tests |

## API contracts

- `GET /api/health` — application health
- `GET /api/demo` — fictional Sarah scenario
- `GET /api/catalog` — approved assets
- `POST /api/analyze` — calculation and report, returns `run_id`, `result`, `pdf_url`
- `GET /api/runs` — saved analysis metadata
- `GET /api/runs/{run_id}` — saved evidence
- `GET /api/report/{run_id}` — PDF download

## Next production steps

Data licensing, rigorous private-comp calibration, factor model, liquidity-aware allocation, user suitability, independent validation, backtesting multiple regimes, stronger authentication, encryption, and controlled asynchronous data ingestion. The MVP intentionally excludes all of these rather than pretending they exist.
