# 13-week-rolling-cashflow-forecast
# Meridian Fabrication Co. - 13 Week Rolling Cash Flow Forecast

A formula-driven Excel model that forecasts weekly cash for a mid-size manufacturer, tests it against a minimum-cash loan covenant, stress-tests it with Best / Base / Worst scenarios, and measures how accurate earlier forecasts were.
Dashboard
<img width="575" height="429" alt="image" src="https://github.com/user-attachments/assets/0af56ea5-b61c-44e2-85e2-2ec147fdf748" />
> **Data note:** all figures are synthetic and created for this portfolio project. No real company, customer, vendor or bank data is used.
> 

## What it answers
| Question | Where |
| --- | --- |
| How much cash will we have each week for the next 13 weeks? | `Live Model`, `Dashboard` |
| Do we stay above the $1.2M minimum-cash covenant? | `Live Model` (headroom row), `Dashboard` |
| What happens in a downside or upside case? | `Scenario` |
| How wrong were previous forecasts, and does accuracy fall with horizon? | `Variance Calc`, `Snapshot Log` |
## Headline results (as of Week 4 close, 11 Sep 2026)

| Metric | Value |
| --- | --- |
| Cash today | $3.27M |
| Week 17 ending cash - Base / Best / Worst | $3.44M / $4.45M / $1.93M |
| Minimum covenant headroom -Base / Worst | $2.06M / $0.63M |
| Average weekly net cash flow (Base) | +$13K |
| Average 1-week-ahead receipts forecast error | 6.1% |

The deepest single-week outflow is Week 12, when the Q4 estimated tax payment coincides with payroll. Capex in Weeks 7, 10 and 14 adds further pressure. Even in the Worst case the covenant is not breached.

## How the model works

1. **Drivers.** Weekly sales = base sales × (1 + weekly growth)^(week−1) × seasonality index. Purchases = COGS ratio × sales.
2. **Working-capital lags.** AR collections in a week = Σ sales(week − k) × collection %(k) for k = 0…4, with 2% written off as bad debt. AP payments use the same structure on purchases.
3. **Cash build.** Receipts = AR collections + other receipts. Disbursements = AP + payroll + opex + capex + debt service + taxes. Ending cash = beginning cash + receipts − disbursements.
4. **Covenant test.** Headroom = ending cash − minimum cash covenant.
5. **Scenarios.** Receipts and disbursements are scaled by levers on the `Scenario` tab (Best +5% / −3%, Worst −8% / +4%) and cash is re-chained.
6. **Forecast accuracy.** `Snapshot Log` stores every weekly forecast vintage plus every actual in one long table. `Variance Calc` uses `SUMIFS` to compare each closed week’s actuals with the forecast made 1-4 weeks earlier.

## Workbook tabs

| Tab | Purpose |
| --- | --- |
| `Overview` | Purpose, live headline numbers, clickable tab guide, method, colour key |
| `Dashboard` | KPI tiles and five charts |
| `Assumptions` | Every input: AR/AP curves, drivers, seasonality, payroll/opex/capex/debt/tax schedule, covenant |
| `Driver Build` | Weekly sales and purchases, Weeks 1-17 |
| `Actuals` | Closed Weeks 1-4 by category |
| `Live Model` | The rolling 13-week forecast (Weeks 5-17) |
| `Scenario` | Best / Base / Worst comparison |
| `Variance Calc` | Actual vs prior forecast, accuracy by horizon |
| `Snapshot Log` | Append-only forecast history: every weekly 13-week forecast vintage plus every actual, stored as one long table. It is the data source for Variance Calc. |
| `KPI Summary` | Headline numbers table behind the dashboard |

**Colour convention:** blue = hard-coded input, black = formula, green = cross-sheet link, yellow fill = key assumption or lever.

## Skills demonstrated

- 13-week cash flow forecasting and covenant monitoring
- Working-capital modelling with lag-weighted AR/AP curves
- Scenario and sensitivity analysis driven by input levers
- Forecast-vs-actual variance analysis using a forecast-vintage log
- Advanced Excel: `SUMIFS`, cross-sheet formulas, dynamic titles, native charts, conditional formatting.
