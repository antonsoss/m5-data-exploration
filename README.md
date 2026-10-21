# M5 Data Exploration and Data Understanding

**Group 2 - MIA5130A Systems Optimization and Management**

Open **M5_Data_Exploration_and_Understanding.ipynb**. It contains executed tables,
charts, interpretation, and a report-ready Data Understanding section for the team.

## Setup

Python 3.12 is recommended; the notebook was executed with this version. In a terminal
opened in this project folder:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m ipykernel install --user --name m5-exploration --display-name "Python (M5 exploration)"
jupyter lab
```

Select **Python (M5 exploration)** when opening the notebook. In VS Code, select the
same environment as the notebook kernel. Run the notebook from top to bottom.

## Data location

Obtain the data from [Kaggle](https://www.kaggle.com/competitions/m5-forecasting-accuracy/data).
Place the five CSV files in `data/`, or set `DATA_DIR_OVERRIDE` in the first code cell.
The notebook also finds `~/Downloads/m5-forecasting-accuracy` automatically.
Alternatively set `M5_DATA_DIR` to that folder before opening Jupyter.

Required files:

- calendar.csv
- sales_train_evaluation.csv
- sales_train_validation.csv
- sell_prices.csv
- sample_submission.csv

Raw CSV files are read in place; they are not copied into this project or modified.
The full audit uses the wide sales matrix; only ten selected product-store series
are converted to long format. Allow approximately 1–2 GB of available working memory.

## What is included

- File inventory, checksums, schemas, and data dictionary.
- Full overlap verification between the two sales files.
- Keys, nulls, values, dates, hierarchy, and complete historical price-join audit.
- Sales distributions, trends, seasonality, events, SNAP, and price exploration.
- An illustrative ten-product subset selected with training-period data only.
- Weekly target and inputs, chronological splits, and independent timing checks.
- Rolling-origin validation baselines; the final test window is not scored.
- Inventory and routing limitations and a generated Data Understanding draft.

## Outputs

`outputs/` contains eight figure PNGs, compact profile/quality tables, the selected
daily sales table, a weekly forecasting panel, `data_profile.json`, exact runtime
versions, and `data_understanding.md`. These are regenerated when you run all cells.
The raw dataset remains the source of truth; exported subsets are analysis products.

The ten products and simulated routing scenario are proposals for team discussion.
The notebook does not train the final ML model or solve inventory and routing problems.
M5 describes U.S. retail activity: SNAP is defined in the notebook, and prices are in USD.
