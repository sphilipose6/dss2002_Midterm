# Walmart Hurricane Analytics

DS-2002 Midterm, Fall 2026 | Ethan, Steve, Henry

We acted as Walmart's data science consultants for Hurricane Helene (landfall in Florida's Big Bend on the night of Sep 26, 2024). We cleaned five messy data files, pulled real weather from the Open-Meteo API, and answered five questions about what sold, where, and whether the signal is real.

## Headline results

- **Demand tripled before landfall.** Daily volume peaked at 3.6x the Sep 1-14 baseline on Sep 24-25, one to two days before landfall.
- **Pop-Tarts surged the most.** Breakfast (strawberry Pop-Tarts) rose +410% in the 7 days before landfall (Sep 19-25) and peaked at 9.2x normal. Emergency supplies rose +182%.
- **Pop-Tarts were hidden in 4 SKUs.** Consolidated, they are 5,005 units, the #2 product and 3.8x any single SKU. The largest single SKU ranked #8 of 45.
- **People buy on the forecast, not the weather.** Sales correlate best with wind and pressure two days later (r = 0.71 with wind gust overall, up to -0.69 with pressure for Emergency).
- **Every store surged.** All 12 stores rose 2.6x-3.2x, with no relationship to distance from landfall (rank correlation -0.08).
- **Board games are a real signal.** Monopoly rose +157% and the database agrees with point-of-sale (r = 0.96). Shelves ran below reorder point on Sep 21-26. We recommend stocking extra, planning for about 2.5x normal volume.

## Repository structure

```
walmart-hurricane-project/
|-- CHARTER.md
|-- README.md
|-- data/
|   |-- walmart_transactions.csv
|   |-- store_locations.csv
|   |-- product_catalog.csv
|   |-- distribution_centers.csv
|   `-- inventory_and_sales.db
`-- notebooks/
    |-- team_notebook.ipynb     <- deliverable
```

## How to run

1. Install Python 3 with `pandas`, `numpy`, `matplotlib`, `seaborn`, and `requests` (`sqlite3` is in the standard library).
2. Keep the five data files in `data/`, next to the `notebooks/` folder. The notebook reads them from `../data/`.
3. Open `notebooks/team_notebook.ipynb` in Jupyter, VS Code, or Colab, with the working folder set to `notebooks/`.
4. Run **Restart and Run All**. The weather API needs no key, and an internet connection is required.

## Notebook contents

1. Setup and profile
2. Cleaning pipeline and decision log
3. SKU consolidation
4. Weather API and join
5. Q1 Demand surge
6. Q2 SKU consolidation
7. Q3 Weather correlation
8. Q4 Stores and geography
9. Q5 Signal or artifact
10. Recommendations
11. Reflection

## Data cleaning

Every cleaning decision is logged with the number of rows it touched (see the decision log table in the notebook). Main steps:

- Transactions: 25,562 rows reduced to 24,521. We dropped 30 exact duplicates, 130 negative quantities, and the rows with no usable timestamp (blank, NULL, N/A, NaN).
- Store IDs: 60 spellings normalized to 12 stores (`FL-239`, `FL_239`, `fl-239` and so on).
- Timestamps: five formats parsed as local store time.
- Prices: `$` and spaces removed, converted from text to numbers.
- Categories: 37 spellings mapped to 10 categories.
- SKUs: 45 SKUs mapped to 20 canonical products by keyword, with an assert that each SKU matches exactly one product.
- Database: compact dates fixed in SQL, and rows for 4 SKUs not in the catalog dropped.

## Weather data

Source: Open-Meteo historical weather API, `https://archive-api.open-meteo.com/v1/archive` (no key required).

We pull hourly temperature, precipitation, wind speed, wind gusts, and sea-level pressure for each store's latitude and longitude, with retries on failure. The API returns GMT, so each hour is converted to the store's local time (Eastern for 11 stores, Central for Pensacola) before rolling up to daily values. The join to sales is checked at 360 store-days (12 stores x 30 days).

## Limitations

- This is one storm and one month of data, and the stores are not independent (they all saw the same forecast), so the weather correlations describe this event and are not a forecasting model.
- Distance in Q4 is measured to the landfall point, not the full storm track.
- The database's category totals do not match point-of-sale, so we use it only for daily totals and curve shape. The Sep 12-20 inventory jump is treated as an artifact.
- Board game inventory has only 3 SKUs and about 7-14 sampled rows a day, so daily reorder percentages move in large steps.
- The data is synthetic, designed to mirror the patterns in the Walmart case.

## Team

| Person | Primary role |
|--------|--------------|
| Ethan | Cleaning and decision log |
| Steve | Weather API and join |
| Henry | Analysis Q1-Q5 |

Charts, the presentation, and the reflection were shared. See `CHARTER.md` for roles, question owners, and how we worked.
