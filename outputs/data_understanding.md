# Data Understanding

**Group 2 - MIA5130A Systems Optimization and Management**

We propose M5 Forecasting — Accuracy as the main dataset for the supply chain project. It contains daily Walmart unit sales for 3,049 anonymized products across 10 stores in California, Texas, and Wisconsin, organized into 3 categories and 7 departments. The dataset is available through [Kaggle](https://www.kaggle.com/competitions/m5-forecasting-accuracy/data).

## Files and structure

The main sales file, sales_train_evaluation.csv, contains 30,490 product–store rows and 1,941 daily sales columns, covering 2011-01-29 to 2016-05-22. calendar.csv contains 1,969 daily records with dates, retail-week identifiers, events, and state-specific SNAP flags. sell_prices.csv contains 6,841,121 product–store–week price records. Calendar data joins on d, while prices join on item_id, store_id, and wm_yr_wk. The shorter sales_train_validation.csv duplicates the overlapping 1,913 days and should not be appended. sample_submission.csv is a competition output template.

SNAP means Supplemental Nutrition Assistance Program, a U.S. government program that helps eligible low-income households buy food. In M5, snap_CA, snap_TX, and snap_WI mark SNAP purchasing days for the corresponding state: 1 indicates a flagged date and 0 an unflagged date. These fields describe the U.S. retail context, even though our team is based in Canada. See [USDA](https://www.ers.usda.gov/topics/food-nutrition-assistance/supplemental-nutrition-assistance-program-snap) for the program definition.

## Inputs and target

We could define the target as total observed units sold for each product and store during the next Monday–Sunday week, matching the inventory milestone's weekly decision. Candidate inputs include product and location identifiers, lagged sales, trailing sales averages, calendar events, the matching state's SNAP flag, and prices known at the forecast origin. Future observed prices must not be treated as known inputs unless supplied as a declared price plan. Holding the last observed price constant is an explicit assumption.

## Initial data quality findings

The longer sales file contains 59,181,090 daily observations, with 0 missing sales cells, 0 negative counts, and 0 duplicate product–store keys. Zero sales account for 68.0% of observations. Calendar dates are consecutive and cover all observed sales days. Optional event fields are blank when no event is listed. The price file has no missing cell values or duplicate product–store–week keys, but 20.8% of historical product–store-days have no matching price record; all have zero sales. Within days with a listed price, 59.6% of sales observations are zero. These distinctions matter for handling selling-history coverage and sparse demand.

## Preparation and proposed scope

We could use ten food products at CA_1 for the assignment's 100-unit inventory scenario. The illustrative subset in this notebook uses only training-period coverage and volume; the team still needs to agree on the final products and routing scope. Sales will be reshaped for the selected subset, joined to calendar and price data, and aggregated into complete seven-day targets. Training, validation, and test targets follow time order. The illustrative training cutoff is 2016-03-27, followed by 28 validation days and 28 test days. Lag and rolling features use only observations available at each forecast origin.

## Limits for inventory and routing

Observed sales are a proxy for demand because stockouts and unmet demand are not measured. Selling prices support revenue calculations but not profit without cost assumptions. Inventory allocations and routes are optimization outputs, not supervised labels. M5 provides store codes but no exact coordinates, depot, road network, vehicle capacities, or emissions factors. We could define a documented simulated routing network with multiple destinations and clearly distinguish those assumptions from observed M5 data. The dataset's U.S. prices and SNAP context would require adaptation for a Canadian operational setting.
