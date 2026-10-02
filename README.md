# SunCoke Energy (NYSE: SXC) — 3-Statement & Valuation Model

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/k-sifat/SXC-Financial-Model/blob/main/SXC_Historical_Model.ipynb)

A Python-based 3-statement financial model and equity valuation for **SunCoke Energy (SXC)**, replicating the full mechanics of `SXC-historical-model.xlsx`. The model projects Income Statement, Balance Sheet, and Cash Flow Statement over a 5-year forecast horizon (FY2026E – FY2030E) and derives two independent price targets.

---

## Investment Thesis Context

SunCoke Energy is the largest independent producer of coke in the Americas, operating domestic cokemaking facilities and an industrial services (logistics) segment. The model captures key idiosyncratic risks including:

- **Granite City Contract Risk**: U.S. Steel's Granite City blast furnace contract expiration creates a binary volume outcome (±590 kt from FY27+)
- **Deleveraging Story**: $40M/year revolver paydown from $185.5M opening balance drives interest savings and equity accretion
- **Growth CapEx Normalization**: Phoenix integration spending tapers from $20M → $0M over FY26–FY30, improving FCF trajectory
- **Valuation Disconnect**: Current EV/EBITDA of ~5.4x vs. historical trading range and peer multiples

---

## Model Architecture

```
┌──────────────────────────────────────────────────────────┐
│                    9 Driver Inputs                       │
│  Tax Rate · D&A% · SG&A% · Coke Volume · EBITDA/ton    │
│  IS EBITDA · Granite Toggle · WACC · Target Multiple    │
└────────────────────────┬─────────────────────────────────┘
                         ▼
┌──────────────────────────────────────────────────────────┐
│               Revenue Build (FY26–FY30)                  │
│  DC: Volume × $430.46/ton  │  IS: EBITDA / 33.2% margin │
│  + Brazil/Other $35.7M flat                              │
├──────────────────────────────────────────────────────────┤
│            Income Statement Projection                   │
│  COGS (residual) + SG&A + D&A → EBIT → EBT → NI        │
│  D&A = da_rate × prior-year Net PP&E                    │
├──────────────────────────────────────────────────────────┤
│         Debt Schedule & Interest Expense                 │
│  Revolver: $40M/yr paydown, 6% SOFR+spread              │
│  Senior Notes: $500M @ 4.875%, held flat                 │
├──────────────────────────────────────────────────────────┤
│           PP&E Roll-Forward (Recursive)                  │
│  PPE(t) = PPE(t-1) + CapEx(t) - D&A(t)                 │
│  CapEx = $50M maint + growth taper                      │
├──────────────────────────────────────────────────────────┤
│              Cash Flow Statement                         │
│  CFO = NI + D&A + SBC                                   │
│  CFI = -CapEx                                            │
│  CFF = -Revolver paydown - Dividends - NCI dist + Other │
├──────────────────────────────────────────────────────────┤
│               Working Capital Delta                      │
│  ΔWC = (Cash + AR + Inv + Other CA) - (AP + Accrued)    │
│  Only cash varies; other items held flat from FY25       │
├──────────────────────────────────────────────────────────┤
│                  DCF Valuation                           │
│  UFCF = NOPAT + D&A + ΔWC - CapEx                      │
│  TV = FCF₅ × (1+g) / (WACC-g),  g = 0%                 │
│  EV = PV(forecast CFs) + PV(TV)                         │
│  Equity = EV - Net Debt → Price/Share                    │
├──────────────────────────────────────────────────────────┤
│             EV/EBITDA Multiple Valuation                 │
│  FY28 EBITDA × Target Multiple = EV                     │
│  Equity = EV - FY28 Net Debt → 3-Yr Price Target        │
├──────────────────────────────────────────────────────────┤
│                Blended Price Target                      │
│  = (DCF + EV/EBITDA) / 2                                │
│  3-Year IRR = (Blended PT / Current Price)^(1/3) - 1    │
└──────────────────────────────────────────────────────────┘
```

---

## Base-Case Results

> Granite City toggle = 0 (contract lost), WACC = 9.38%, Target EV/EBITDA = 7.0x

| Metric | Value |
|--------|-------|
| **Current Share Price (as of 8/31/26)** | $8.41 |
| **EV/EBITDA 3-Yr Price Target** | $12.59 |
| **DCF Intrinsic Value** | $18.56 |
| **Blended Price Target** | $15.57 |
| **3-Year Annualized IRR** | 18.79% |
| **Implied Upside (Blended)** | +67.6% |
| TEV (Today) | $1,391.1M |
| EV/EBITDA (FY25 Actual) | 5.36x |

---

## How to Run

### Option 1: Google Colab (No Setup)
Click the **"Open in Colab"** badge above. All dependencies are pre-installed in the Colab environment.

### Option 2: Run Locally
```bash
# Clone the repo
git clone https://github.com/k-sifat/SXC-Financial-Model.git
cd SXC-Financial-Model

# Install dependencies
pip install -r requirements.txt

# Launch Jupyter
jupyter notebook SXC_Historical_Model.ipynb
```

### Option 3: Streamlit Web App
```bash
pip install -r requirements.txt
streamlit run app.py
```

---

## Repository Structure

```
├── SXC_Historical_Model.ipynb   # Main model notebook (GitHub-renderable)
├── SXC Historical Model.ipynb   # Original single-cell notebook (archived)
├── app.py                       # Streamlit web app (optional deployment)
├── requirements.txt             # Python dependencies
└── README.md                    # This file
```

---

## Disclaimer

This model is for **educational and analytical purposes only**. It does not constitute investment advice. All projections are based on simplified assumptions and publicly available information. Past performance and model outputs do not guarantee future results.
