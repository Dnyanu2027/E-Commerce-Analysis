# Online Retail: Cleaning, Revenue & Top 10 Countries

A step-by-step Jupyter notebook that samples, cleans and analyses the **Online Retail** dataset (UK-based online gift retailer, Dec 2010 to Dec 2011) to find which countries generate the most revenue.

# Proejct URL : https://roadmap.sh/projects/ecommerce-data-analysis

## Files

| File | Description |
|---|---|
| `online_retail_analysis.ipynb` | The analysis notebook, with an explanation before every step and outputs saved |
| `Online_Retail.xlsx` | Source data (not included here; place it in the same folder as the notebook) |

## Requirements

- Python 3.9+
- `pandas`, `matplotlib`, `openpyxl` (needed by pandas to read `.xlsx`), `jupyter`

```bash
pip install pandas matplotlib openpyxl jupyter
```

## How to run

1. Put `Online_Retail.xlsx` and `online_retail_analysis.ipynb` in the same folder.
2. Start Jupyter: `jupyter notebook`
3. Open the notebook and choose **Run > Run All Cells**.

If your data file is elsewhere, change `FILE_PATH` in the first code cell.

> Loading the Excel file (about 540k rows) can take a minute.

## What the notebook does

1. **Load** the full dataset (541,909 rows, 8 columns).
2. **Sample 10%** of rows with `random_state=42` for speed and reproducibility.
3. **Inspect** nulls, data types, negative quantities and zero prices before touching anything.
4. **Clean**
   - Remove rows with missing `CustomerID` or `Description`.
   - Fix data types: `InvoiceDate` to `datetime`; `CustomerID`, `InvoiceNo` and `StockCode` to strings.
   - Filter out returns (negative `Quantity` or invoice numbers starting with `C`).
   - Filter out free items (`UnitPrice == 0`).
5. **Create `Revenue`** = `Quantity x UnitPrice`.
6. **Rank** the top 10 countries by total revenue and plot them (with and without the UK).

## Results (10% sample, GBP)

| Rank | Country | Revenue |
|---|---|---|
| 1 | United Kingdom | 768,683 (83.7%) |
| 2 | Netherlands | 27,436 |
| 3 | EIRE | 24,340 |
| 4 | France | 23,607 |
| 5 | Germany | 22,390 |
| 6 | Australia | 12,430 |
| 7 | Spain | 5,601 |
| 8 | Switzerland | 5,383 |
| 9 | Belgium | 3,594 |
| 10 | Portugal | 3,244 |

Cleaning removed 26.9% of the sampled rows (54,191 down to 39,635).

## Notes and limitations

- **Sample, not full data.** Revenue figures are about one-tenth of the true totals, and lower-ranked countries can shift between samples. For final numbers, set `frac=1` in the sampling cell.
- **Null removal is a judgement call.** Dropping missing `CustomerID` removes about 25% of rows and their revenue. If you only need country-level revenue, you could keep those rows.
- **UK dominance.** The UK accounts for most revenue, so a second chart excludes it to make the international comparison readable.
- **Currency.** Revenue is in GBP.

## Possible next steps

- Monthly revenue trend (enabled by the `datetime` conversion)
- Top products by revenue
- Revenue per customer and customer segmentation
