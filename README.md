# Bridging AI forecasts and fuzzy optimization: code for the numerical results

This repository reproduces every number and table of the paper
"Bridging AI Forecasts and Fuzzy Optimization: Joint Price and Inventory Decisions for Defective Items in Sports Retail"
from the raw public data. The figures of the paper are drawn in LaTeX from the numbers in `outputs/results.json`.

## What the notebook does
`Bridging_Fuzzy_Inventory.ipynb` runs the full pipeline:

1. cleans the Olist data (sports categories, weekly demand, review-based defect proxy);
2. estimates price sensitivity within products and calibrates the linear demand curve;
3. fits the Stage-1 models and builds the prediction intervals;
4. solves the crisp and the fuzzy inventory model (order quantity Q, backorder quantity B, price P);
5. compares seven policies by simulation and by a rolling backtest on real weeks, with statistical tests;
6. runs robustness checks (60 scenarios, 12 cost regimes) and writes all numbers to `outputs/results.json`.

Each section of the notebook starts with a short explanation, and the table in section 4 maps paper symbols to code.

## How to run
1. Download the Olist Brazilian E-Commerce dataset from Kaggle (`olistbr/brazilian-ecommerce`). It is not redistributed here because of its license (CC BY-NC-SA 4.0).
2. Put these five files in a folder named `olist_data/` next to the notebook:
   `olist_orders_dataset.csv`, `olist_order_items_dataset.csv`, `olist_products_dataset.csv`,
   `olist_order_reviews_dataset.csv`, `product_category_name_translation.csv`
   (zip files are also accepted).
3. `pip install -r requirements.txt`
4. Open the notebook and choose Kernel > Restart & Run All. Run time is a few minutes. Random seeds are fixed.

## Expected key results (check after running)
| quantity | value |
|---|---|
| crisp optimum | Q* = 505.148, B* = 109.866, P* = 194.293 (price at its upper bound) |
| fuzzy optimum | Q* = 742.02, B* = 265.11 |
| calibrated demand | a0 = 67.574, a1 = 0.2096, a2 = 1.1715 |
| simulated profit, proposed fuzzy minus proposed crisp | about -5.41 dollars per week |

Small differences in the last decimals can come from different library versions.

## Important notes
- The defect proxy is a dissatisfaction signal (review score <= 2), not a measured manufacturing defect.
- Cost parameters are illustrative; the dataset contains no cost data.
- The price is bounded by the highest observed weekly price, and the price effect is weakly identified (see the paper).

## AI assistance
During the preparation of this work, the authors used the AI assistant Claude (Anthropic; November 2026) to assist with writing and debugging the Python code and Jupyter notebook. The research question, the model design and the interpretation of the results are the authors' own. All model derivations, data choices and results were checked by the authors, who ran the notebook themselves and take full responsibility for the content. 
## Citation and license
If you use this code, please cite:

Gupta, N., Singh, O. (2026). Bridging AI Forecasts and Fuzzy Optimization: Joint Price and Inventory Decisions for Defective Items in Sports Retail. Manuscript under review.

Code: https://github.com/tnnidhi0409-code/bridging-fuzzy-inventory

This code is released under the MIT License (see the LICENSE file). The Olist dataset has its own license (CC BY-NC-SA 4.0) and is not included.