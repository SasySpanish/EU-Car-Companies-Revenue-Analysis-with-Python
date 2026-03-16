# Scripts

This folder contains all the Python modules that power the analysis pipeline.

| File                  | Main Purpose                                                                                          | Primary Role in Workflow                  |
|-----------------------|-------------------------------------------------------------------------------------------------------|-------------------------------------------|
| `main.py`             | Main execution script — orchestrates the entire workflow from data download to output generation      | Entry point / orchestrator                |
| `config.py`           | Central configuration: list of tickers, reference thresholds, analysis years, currency notes, etc.    | Global settings & thresholds              |
| `fetcher.py`          | Downloads raw financial statements (income, balance sheet, cash flow) and metadata from Yahoo Finance via `yfinance` | Data acquisition                          |
| `indicators.py`       | Computes all key financial indicators (margins, ROE, ROCE, leverage, liquidity ratios, etc.) from raw statements | Core financial logic — indicator calculation |
| `trend_analysis.py`   | Builds multi-year trend tables for each indicator and calculates CAGR (Compound Annual Growth Rate)   | Time-series analysis & growth metrics     |
| `market_data.py`      | Extracts current market valuation multiples (P/E, EV/EBITDA, P/B, Market Cap, etc.) from `.info`      | Market valuation & trading multiples      |
| `visualizer.py`       | Creates all static matplotlib charts: threshold-aware bar charts, trend lines, CAGR heatmap, market multiples + summary PDF | Static visualization & PDF export         |
| `trend_dashboard.py`  | Generates an interactive, self-contained HTML dashboard (using Plotly) with indicator selector, company lines, thresholds & group median | Interactive web visualization             |

### Typical Execution Flow (as run from `main.py`)

1. `fetcher.py` → downloads annual income statements, balance sheets, cash flows and info for all configured tickers  
2. `indicators.py` → transforms raw data into a clean set of financial indicators  
3. `trend_analysis.py` → creates historical trend tables and computes CAGR values  
4. `market_data.py` → collects current market multiples and valuation metrics  
5. `visualizer.py` → produces:
   - individual PNG charts (bars with thresholds, trends, market multiples, CAGR heatmap)
   - one consolidated PDF report with cover page + all charts
6. `trend_dashboard.py` → creates `trend_dashboard.html` — fully standalone interactive dashboard  
7. Exports structured results to Excel (`automotive_analysis.xlsx`)

### Design Notes

- **Modularity**  
  Each file follows a single responsibility principle.

- **Clear naming**  
  Functions are descriptive (`calc_ebit_margin`, `build_cagr_table`, `_clean_name`, etc.).

- **Graceful handling**  
  Missing data for a ticker or indicator is skipped rather than crashing the whole run.

- **Formatting conventions**  
  - Monetary values expressed in millions (M)  
  - Margins and returns shown as percentages (%)  
  - Company names are cleaned/shortened in outputs and visuals

- **Main dependencies**  
  - `yfinance`  
  - `pandas`  
  - `numpy`  
  - `matplotlib`  
  - `plotly` (used only for the HTML dashboard)  
  - `openpyxl` (Excel writing)

Feel free to explore the code — happy analyzing!
