# ShockLab — *Fade or Cascade?* Market Stress-Testing on a Portfolio

> **How much does a real-world shock move a multi-asset portfolio?**
> A lightweight market-risk engine that **quantifies the P&L impact** of geopolitical and ecological shocks — by composing **real historical analogues**, not invented numbers.

![status](https://img.shields.io/badge/project-3%20of%203-blue) ![lang](https://img.shields.io/badge/python-3-Informational) ![domain](https://img.shields.io/badge/domain-Market%20Risk-red)

---

## TL;DR
ShockLab takes a **fictional ~$25M multi-asset portfolio** and stresses it with two scenarios, each built from **real market reactions** to past events:

| Scenario | Headline move | Portfolio P&L |
|---|---|---|
| 🛢️ **Iran–US / Strait of Hormuz** (oil shock) | **Brent +5.0%** | **+$0.14M (+0.54%)** |
| 🌡️ **Ecological shock** (heatwave / drought) | commodities hit | **−$0.05M (−0.18%)** |

**The core insight:** most shocks **fade** (the market reverts within 20 days); only shocks that hit the **credit/liquidity channel** truly **cascade**. So the real question isn't *"will it fade?"* — it's *"will it break the credit channel?"*

---

## The question
> *When a shock hits, does the market **fade** it (forget it, like the Soleimani strike — reverted in 3 days) or **cascade** (collapse, like COVID or Lehman)? And for a shock that hasn't happened — an Iran–US escalation — what would it do to a portfolio?*

Rather than predicting prices (the student trap that fails), ShockLab **classifies the type of reaction** and then **composes a scenario from real analogues**.

---

## Method (no invented numbers)
1. **SQL database** of 25 real shocks (2001→2025): geopolitical, financial, oil, climate, **Trump announcements**, **Russia–Ukraine**.
2. **Real market data** (yfinance): S&P 500, VIX, **Brent**, gold, USD, Treasuries (TLT), high-yield credit (HYG), commodities (DBC).
3. For each shock, measure the **move from the day before → the shock day** (the true spike).
4. **Compose** each scenario by averaging the closest analogues → apply to the portfolio → **P&L per line**.
5. **ML (scikit-learn):** logistic regression reveals the **drivers of a cascade** — severity + credit/liquidity channel.

<p align="center">
  <img src="images/trajectoires.png" width="48%">
  <img src="images/drivers_ml.png" width="48%">
</p>

*Left — trajectories: Soleimani fades (flat), COVID dives then V-recovers, Lehman keeps sinking. Right — ML drivers: severity + credit → cascade; energy → fade.*

---

## Results

### 🛢️ Iran–US / Strait of Hormuz
Composed from **Abqaiq 2019** (largest oil shock in decades), **Iran–Israel 2024**, **Soleimani 2020**, **Russia–Ukraine 2022**.

<p align="center"><img src="images/scenario_hormuz.png" width="70%"></p>

→ **Brent +5.0%**, commodities +1.5%, gold +0.9%, equities −0.2%. The long-oil book gains; equities & credit give back.

### 🌡️ Ecological shock
Composed from **Russia heatwave 2010**, **Europe droughts 2018 & 2022**, **Canada wildfires 2023**, **Australia 2019**.

<p align="center"><img src="images/scenario_ecologique.png" width="70%"></p>

→ A **regional** shock: global equities hold up, but **commodities/energy** take the hit.

---

## How to run
```bash
git clone https://github.com/<your-username>/ShockLab.git
cd ShockLab
pip install -r requirements.txt
jupyter notebook ShockLab.ipynb   # then Run All
```
Open the rendered version without installing anything: see `ShockLab.html`.

---

## Tech stack
`Python` · `pandas` · `scikit-learn` (ML) · `SQLite` (SQL) · `yfinance` (real data) · `matplotlib` · `Jupyter`

## Honesty / limits
- Small sample (25 shocks) → **interpretable** models only (logistic regression), no black box.
- Moves are **composed from analogues**, not extrapolated — like a desk stress-test.
- No claim of causation: conditional associations that are robust enough to *inform* a scenario.

---

## Part of a 3-project portfolio
| # | Project | Role | Tech |
|---|---|---|---|
| ① | **CalvinX Market Terminal** | *Present* — monitor where the risk is | JavaScript / Excel |
| ② | **Greeks au max** | *Mechanism* — how a derivatives book blows up | VBA / Excel |
| ③ | **ShockLab** *(this repo)* | *Future* — P&L of scenarios on a portfolio | Python / SQL / ML |

**One question across all three:** *How does a desk avoid losing everything?*

---

## Author
**Calvin Minang** — MSc Corporate Financial Management, SKEMA Business School · FRM Candidate
Markets & Market Risk · [LinkedIn](https://www.linkedin.com/in/calvin-minang) · calvin.minang@skema.edu
