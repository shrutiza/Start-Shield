# START HERE — StartShield

## 1-minute setup (Windows PowerShell)

1. Open the extracted `startshield` folder in VS Code.
2. Activate a Python 3.11–3.14 environment. For Python 3.14, ensure compatible packages can be installed.

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m pytest -q
python -m uvicorn startshield.api:app --app-dir src --reload --port 8002
```

Open **http://127.0.0.1:8002/** in Chrome or Edge, click **Load Sarah's example**, then **Run risk analysis**. Download the PDF at the bottom.

## What to say in a 30-second demo

“StartShield examines an angel investor's illiquid startup concentration. The analyst enters private stakes. Our system proposes public-company risk proxies, retrieves 2022 adjusted market returns or uses a clearly fictional offline scenario, estimates possible concentration losses under a slider-controlled shock, and compares two hypothetical allocations of spare cash. Python computes every value and our PDF documents methods and limitations. We never pretend that public proxies are private-company share prices.”

## First use

Keep **Offline synthetic demo** selected to guarantee an immediate end-to-end demonstration. Enable **Historical Yahoo via yfinance** only when internet access is reliable and the requested securities have 2022 history. The two data modes never silently substitute for each other.

If Groq is wanted, create `.env` from `.env.example`, configure `GROQ_API_KEY`, and tick “Use Groq”. Failure falls back to allowlisted heuristic twins and a deterministic narrative. Groq never controls numerical results.

## What NOT to claim

- No live private-company valuation or verified startup-return forecast.
- No actual model-based portfolio optimizer; the 30/30/20/20 basket is fixed and capped.
- No guaranteed hedge, no portfolio suitability assessment or regulated investment advice.
- No 2022 historical facts when in **Offline synthetic demo** mode.
- No permission to redistribute Yahoo price data for commercial use.
- No investment execution or live brokerage connection.
