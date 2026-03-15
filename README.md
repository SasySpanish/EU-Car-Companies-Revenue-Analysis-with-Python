# Automotive Sector Europe — Financial Analysis

Comparative analysis of key financial indicators for the major European automotive OEMs, using publicly available data from Yahoo Finance via `yfinance`.

---

## Companies analysed

| Ticker | Company | Country | Segment |
|---|---|---|---|
| `VOW3.DE` | Volkswagen Group | 🇩🇪 Germany | Mass-market |
| `STLAM.MI` | Stellantis | 🇮🇹 Italy | Mass-market |
| `MBG.DE` | Mercedes-Benz | 🇩🇪 Germany | Premium |
| `BMW.DE` | BMW Group | 🇩🇪 Germany | Premium |
| `RNO.PA` | Renault Group | 🇫🇷 France | Mass-market |
| `P911.DE` | Porsche AG | 🇩🇪 Germany | Premium |
| `VOLCAR-B.ST` | Volvo Cars | 🇸🇪 Sweden | Premium |
| `TKA.DE` | TRATON Group | 🇩🇪 Germany | Commercial |
| `IVG.MI` | Iveco Group | 🇮🇹 Italy | Commercial |

---

## Calculated indicators

## Indicators analysed

| Indicator | Category | Formula | Meaning |
|---|---|---|---|
| Revenue | Absolute profitability | Total revenues | Total value of goods and services sold |
| Gross Profit | Absolute profitability | Revenue − Cost of Goods Sold | Profit after production costs |
| EBIT | Absolute profitability | Operating income | Profit before interest and taxes |
| EBITDA | Absolute profitability | EBIT + Depreciation & Amortisation | Operating profit before non-cash charges |
| Net Income | Absolute profitability | Bottom-line profit | Final profit after all expenses |
| Gross Margin | Margins (%) | Gross Profit / Revenue | Efficiency of production and pricing |
| EBIT Margin | Margins (%) | EBIT / Revenue | Operating profitability |
| EBITDA Margin | Margins (%) | EBITDA / Revenue | Operating cash profitability |
| Net Margin | Margins (%) | Net Income / Revenue | Overall profitability |
| ROE | Returns (%) | Net Income / Equity | Return generated for shareholders |
| ROA | Returns (%) | Net Income / Total Assets | Efficiency in using assets |
| ROCE / ROI | Returns (%) | EBIT / (Total Assets − Current Liabilities) | Return on capital employed |
| Current Ratio | Liquidity | Current Assets / Current Liabilities | Ability to meet short-term obligations |
| Quick Ratio | Liquidity | (Current Assets − Inventory) / Current Liabilities | Short-term liquidity excluding inventory |
| Debt/Equity | Financial structure | Total Debt / Equity | Financial leverage |
| Net Debt | Financial structure | Total Debt − Cash | Real debt burden |
| Interest Coverage | Financial structure | EBIT / Interest Expense | Ability to pay interest |
---

## Usage

### 1. Install dependencies
```bash
pip install -r requirements.txt
```

### 2. Run the full analysis
```bash
python main.py
```

### 3. Explore available fields for a ticker
```bash
python fetcher.py
```

### Output
- Comparison table printed to the terminal
- Excel file `output/automotive_analysis.xlsx` containing:
  - One sheet per company (4-year historical data)
  - One aggregated comparison sheet for the latest available year
  - Trend sheets for key indicators
  - CAGR summary sheet
  - Market multiples sheet

---

## Project structure

```
automotive_analysis/
├── config.py          # Tickers, metadata, parameters, thresholds
├── fetcher.py         # Data download from Yahoo Finance
├── indicators.py      # Calculation of all financial indicators
├── trend_analysis.py  # Multi-year trend analysis and CAGR
├── market_data.py     # Market multiples (P/E, EV/EBITDA, P/B, Market Cap)
├── visualizer.py      # Matplotlib charts (PNG + PDF)
├── trend_dashboard.py # Interactive Plotly dashboard (HTML)
├── main.py            # Main script
├── requirements.txt
└── output/            # Generated files (gitignored)
    ├── automotive_analysis.xlsx
    ├── automotive_analysis_charts.pdf
    ├── trend_dashboard.html
    └── charts/
        ├── bar_*.png          # Per-indicator comparison (latest year)
        ├── trend_*.png        # Multi-year trend per indicator
        ├── cagr_heatmap.png   # CAGR heatmap — companies × indicators
        ├── market_bubble.png  # Bubble chart P/E vs EV/EBITDA
        └── market_*.png       # Bar chart for each market multiple
```

---

## Critical thresholds

Every bar chart with a configured threshold displays two reference lines:

| Line | Colour | Meaning |
|---|---|---|
| Red dashed | `#e63946` | Fixed industry benchmark |
| Orange dotted | `#f4a261` | Group median (dynamic) |

Bar colours: **dark blue** (`#03045e`) = above threshold (healthy), **light blue** (`#90e0ef`) = below threshold (caution).

### Thresholds used and rationale

| Indicator | Threshold | Rationale |
|---|---|---|
| **EBIT Margin** | ≥ 5% | Minimum operational health benchmark in the automotive sector. Below this level the core business struggles to generate enough profitability to cover capex and financing costs. |
| **ROE** | ≥ 10% | Commonly used as the minimum return required to adequately compensate equity shareholders. Values below this indicate the company is not creating value for investors. |
| **ROI / ROCE** | ≥ 8% | ROCE should exceed the Weighted Average Cost of Capital (WACC), estimated at 7–9% for a European automotive OEM. Below 8%, the company destroys economic value relative to its invested capital. |
| **Net Margin** | ≥ 3% | Net margins in the automotive sector are structurally compressed. A 3% floor represents the minimum level at which a company is considered to be generating sustainable after-tax profit. |
| **Debt/Equity** | ≤ 2x | A ratio above 2 signals high financial leverage. Given the heavy investment cycles typical of automotive OEMs, exceeding this threshold significantly increases insolvency risk during revenue downturns. |
| **Current Ratio** | ≥ 1x | Below 1, current liabilities exceed current assets — the company may be unable to meet short-term financial obligations without seeking additional financing. |

> All thresholds are fully configurable in `config.py → THRESHOLDS`.

---

## Interactive trend dashboard (Plotly HTML)

The file `output/trend_dashboard.html` is completely **self-contained** and can be viewed:
- **Locally**: open it in any browser, no server required
- **Online**: upload it to GitHub Pages, Netlify Drop, or any static hosting provider

Features:
- Dropdown selector to switch between 13 indicators
- Interactive trend lines per company with tooltip on hover
- Fixed threshold (red dashed) and group median (orange dotted) as reference lines
- Status table ✅ / ⚠️ for each company based on the latest available year
- Explanatory note for the chosen threshold

---

## Notes

- Data is sourced from Yahoo Finance for **educational / personal use only**
- Absolute values (Revenue, EBIT, etc.) are expressed in **millions** in the original reporting currency
- Data availability and completeness may vary by ticker
- `yfinance` may occasionally return missing data if Yahoo Finance changes its internal API

---

## Roadmap

- [ ] Segment comparison (mass-market vs premium vs commercial)
- [ ] Narrative PDF report export
- [ ] Interactive dashboard with Streamlit
- [ ] Quarterly data support (in addition to annual)

---

## Author
Developed by **[Salvatore Spagnuolo](https://github.com/SasySpanish)**  

---
