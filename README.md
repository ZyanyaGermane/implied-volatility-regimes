# Implied volatility and future US index returns across market regimes

Full empirical pipeline for my MSc Finance dissertation (Cardiff University, 2026): does implied volatility predict next-month US equity returns, and does that predictability change inside crises?

## Question

Implied volatility indices summarise the market's expectation of near-term risk. This project tests whether end-of-month implied volatility predicts the following month's excess index return, and whether that relationship differs during the Global Financial Crisis and the COVID-19 crash compared with calm markets.

## Headline result

The predictive relationship is regime-dependent. Implied volatility positively and significantly predicts next-month returns only inside the acute COVID-19 window (Feb–Apr 2020). There is no significant predictability during the GFC or in calm periods, and widening the COVID window to Feb–Dec 2020 removes the effect — the signal is specific to the acute phase of that crisis.

## Data

- Three index–volatility pairs: S&P 500 / VIX, NASDAQ-100 / VXN, Russell 2000 / RVX
- Daily Bloomberg closes aggregated to monthly, January 2004 – June 2026 (sample start set by the RVX inception date, giving a common sample across all three pairs)
- Controls: MOVE index, gold and WTI oil returns
- Risk-free rate: 3-month US Treasury bill (FRED series TB3MS), embedded in the notebook — public data
- The raw Bloomberg extracts are **not** redistributed in this repository for licensing reasons. The notebook keeps its saved outputs, so the results are readable without the data.

## What the notebook does

1. **Load** the daily Bloomberg exports, including handling two files that store dates as Excel serial numbers.
2. **Construct monthly series**: month-end levels, monthly log returns, and annualised realised volatility (252-day scaling, in % p.a., directly comparable to the implied volatility indices).
3. **Align with no look-ahead**: predictors are measured at the end of month *t*; the dependent variable is the month *t+1* excess log return over the T-bill.
4. **Define crisis regimes** on NBER recession dates — GFC: Dec 2007 – Jun 2009; COVID: Feb – Apr 2020 — with interaction terms between implied volatility and each regime.
5. **Estimate** OLS regressions with Newey–West (HAC, 6 lags) standard errors, per index and pooled across the three indices with index dummies: a baseline IV model, the crisis-interaction model, implied versus realised volatility, and a robustness model adding MOVE, gold and oil.
6. **Extensions**: IV persistence (AR(1)), correlation structure, joint F-tests on the interaction terms, alternative crisis definitions (a wide COVID window and a high-volatility IV>30 regime), the pooled model re-estimated with date-clustered standard errors, and out-of-sample R² (Campbell–Thompson).

## Contents

| File | What it is |
|---|---|
| `dissertation_code_notebook.ipynb` | The full pipeline in three sections: base analysis, figure and export, extensions |
| `requirements.txt` | Python dependencies |

## Running it

Developed in Google Colab (Python 3). To re-run: install the requirements, place the Bloomberg exports listed at the top of the notebook in the working directory, and run top to bottom. Without the data files, the notebook still displays its saved results.

## Author

Zyanya Germane — MSc Finance, Cardiff University
