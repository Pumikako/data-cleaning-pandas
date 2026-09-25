# Shark Attacks

An exploratory data analysis of the **Global Shark Attack File (GSAF)**, examining which activities and countries are most affected by shark attacks and how often those attacks are fatal.

The presentation is available in the `presentation/` folder.

---

## Dataset

| | |
|---|---|
| **Source** | [Global Shark Attack File](https://www.sharkattackfile.net) |
| **File** | `GSAF5.xls` |
| **Raw size** | 7,125 rows × 23 columns |
| **After cleaning** | 7,121 rows (`shark_clean`) |

**Key figures (cleaned data):**
- 7,121 recorded attacks
- 1,495 fatal attacks
- 1,249 attacks in the 2010s alone

## Hypotheses

1. Surfing and swimming account for the most attacks.
2. USA, Australia and South Africa are the most dangerous places, by attacks and by fatalities.
3. Most shark attacks are unprovoked and non-fatal.

## Data cleaning & transformation

All steps are wrapped in one reusable function that returns the cleaned DataFrame `shark_clean`.

| # | Step | Details |
|---|---|---|
| 1 | Harmonised column names | Stripped trailing spaces, e.g. `"Species "` → `"Species"` |
| 2 | Dropped 9 non-analytical columns | e.g. Source, pdf, href, Case Number, Unnamed: 21–22 |
| 3 | Removed undated & duplicate rows | 2 rows without a year, 2 exact duplicates |
| 4 | Standardised categories | Fatal: Y / N / Unconfirmed · Type: Provoked / Unprovoked / Unconfirmed · Sex: male / female / Unconfirmed |
| 5 | Grouped activities with keyword dictionaries | 91 keywords → 18 categories, e.g. "spearfishing" → Fishing; no match → "Other" |
| 6 | Filled missing locations | Country filled from State; otherwise "Unknown" |
| 7 | Validated every step | `isna()` and `value_counts()` after each change |

## Key findings

**H1: Activities ✅ Confirmed**
- Surfing and swimming together account for about half of all attacks (~26% each).
- Surfers are bitten about as often as swimmers, but die far less often: a fatality rate of ~12% vs. ~33% for swimmers.

**H2: Countries ⚠️ Partly confirmed**
- USA, Australia and South Africa account for about two-thirds of all recorded attacks.
- Their fatality rates differ sharply: Australia 22.6%, South Africa 20.7%, USA only 8.4% (overall: 23.1%).
- The deadliest locations are elsewhere: since 2000, New Caledonia (41.0%) and Réunion (40.0%) have the highest fatality rates among countries with ≥20 incidents.

**H3: Type & fatality ✅ Confirmed**
- 74% of all attacks are unprovoked.
- 77% of attacks with a known outcome are non-fatal.
- Unprovoked attacks are far deadlier than provoked ones: 24.5% vs. 3.3% fatal.

## Limitations

- Older records over-represent fatal cases (reporting bias), so all-time fatality rates are inflated for countries with many early entries.
- The data contains no exposure information (e.g. number of surfers or swimmers), so counts show where attacks occur, not the risk per person.
- 129 rows use Year = 0 as a placeholder for undated incidents.

## How to run

```bash
pip install pandas xlrd
jupyter notebook
```

`xlrd` is required to read the legacy `.xls` format.

## Tools

Python · pandas · Jupyter
