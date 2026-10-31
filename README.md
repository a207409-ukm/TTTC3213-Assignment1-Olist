# UNIVERSITI KEBANGSAAN MALAYSIA (UKM)
TTTC3213 DATA ENGINEERING - ASSIGNMENT 1
CLASS: 3Int CS-IM

## GROUP MEMBERS

| Name | Matric Number |
|---|---|
| LI ZEHAO | A207409 |
| WU ZHUXI | A207359 |
| LYU HAOWEN | A206795 |
| HAN HAOZHENG | A207411 |

ASSIGNMENT: Data Profiling (EDA) Report (10 marks)  
PROJECT: Olist E-commerce Order and Delivery Data Quality  
CAPSTONE TOPIC: E-commerce Sales & Delivery Analytics Pipeline

## FILES

| File / Folder | Description |
|---|---|
| `Assignment1.ipynb` | Main Jupyter Notebook with the scenario, data source, profiling, cleaning, charts, PII/bias discussion, and conclusion. |
| `README.md` | Project information, data source, requirements, and run instructions. |
| `requirements.txt` | Python libraries needed to run the notebook. |
| `.gitignore` | Prevents downloaded and cleaned data files from being committed. |
| `data/raw/` | Three original Olist CSV files are downloaded here during the run (not included in GitHub). |
| `data/processed/` | Four cleaned CSV files are saved here at the end (not included in GitHub). |

## REQUIREMENTS

- Python 3.10 or newer, with Jupyter Notebook or Google Colab.
- Packages: pandas, numpy, matplotlib, and notebook (see `requirements.txt`).
- Internet access for the first automatic data download, unless you supply the CSV files manually.
- For local Jupyter, run the notebook from the repository root so `data/raw/` and `data/processed/` are created in the project folder. In Google Colab, these folders are created in the Colab runtime, which is temporary.

## DATA SOURCE

Original dataset: [Brazilian E-Commerce Public Dataset by Olist (Kaggle)](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)  
Public CSV source: [Olist's GitHub datasets folder](https://github.com/olist/work-at-olist-data/tree/master/datasets)

The notebook uses these three public CSV files:

1. `olist_orders_dataset.csv` - order status, purchase date, and delivery dates.
2. `olist_order_items_dataset.csv` - product item prices and freight values.
3. `olist_customers_dataset.csv` - customer identifiers and location information.

The notebook downloads the CSV files from Olist's GitHub repository using Python and reads them with pandas. It does not need a Kaggle API key.

## SETUP

Install the libraries (if needed):

```bash
python -m pip install -r requirements.txt
```

Open the notebook from the project folder:

```bash
jupyter notebook Assignment1.ipynb
```

Alternatively, open `Assignment1.ipynb` in Google Colab using **File > Upload notebook** (or open it from GitHub). Select **Runtime > Run all** (or **Run All** in Jupyter). The first code cell downloads the CSVs into `data/raw/` if they are missing. Colab files are temporary: download any cleaned CSVs you need before the session ends.

If automatic download fails: Download the three CSV files from the links in DATA SOURCE and put them into `data/raw/`, keeping the exact filenames. Then run all cells again.

## REPRODUCE PART 1 - SCENARIO AND DATA SOURCE

Read Sections 1 and 2 in the notebook. These describe the Olist delivery-data scenario, the questions to check, the public source URLs, and how the files were obtained.

Expected: A table showing the row and column counts for the three CSV files, followed by their column names.

## REPRODUCE PART 2 - DATA PROFILING AND CLEANING

Run Section 3 in the notebook.

- Missing values: Count missing values in each column. Keep missing delivery dates instead of making up dates.
- Duplicates and keys: Check duplicate rows and keys. Use (`order_id`, `order_item_id`) as the item key because an order may have several items.
- Types and invalid values: Convert dates and monetary values, check invalid values, standardise text formats, and flag or exclude problematic rows where explained.
- Outliers: Use the IQR method on `price` and `freight_value`. Keep and flag valid high amounts rather than deleting them without evidence.

Expected: Missing-value summary, duplicate/key summary, quality-issue summary, and IQR outlier summary. Actual counts are printed when the notebook runs.

## REPRODUCE PART 3 - DIAGNOSTIC CHARTS

Run Section 4 in the notebook.

- Chart 1: Missing values (%) in the original orders table.
- Chart 2: Boxplots to check unusual prices and freight values.
- Chart 3: Order counts by customer state to inspect group balance.

Expected: Three charts with titles and axis labels. These charts show data-quality and coverage issues, not a sales dashboard.

## REPRODUCE PART 4 - PII, BIAS, AND CONCLUSION

Read Sections 5 and 6, then run the final checks.

- PII risk: Customer IDs and location fields may create linking or re-identification risks even in anonymised data. Avoid posting customer-level CSVs.
- Bias risk: Orders may be unevenly distributed across states and are historical, so the data may not represent all Brazilian regions or current customers.
- Conclusion: A delivery-ready subset uses delivered orders with real, valid dates; the notebook explains the data still has limitations.

Expected: A final table with raw and cleaned row counts and a printed delivery-ready order count. Data-quality assertions must complete without an error.

## OUTPUT FILES

The final code cell saves these files locally to `data/processed/`:

- `olist_orders_clean.csv`
- `olist_order_items_clean.csv`
- `olist_customers_clean.csv`
- `olist_delivery_ready.csv`

The original data in `data/raw/` is left unchanged. Both data folders are ignored by Git.

## GITHUB SUBMISSION

1. Create a GitHub repository for this assignment (for example, `Assignment1-Data-Profiling`).
2. Upload `Assignment1.ipynb`, `README.md`, `requirements.txt`, and `.gitignore` from this project. The `data` folders and `.gitkeep` placeholders are optional; do not upload downloaded or cleaned customer-level CSV files.
3. Commit the uploaded files. Open `Assignment1.ipynb` on GitHub to confirm the notebook and charts display correctly.
4. Submit the **repository URL** (for example, `https://github.com/YOUR-USERNAME/Assignment1-Data-Profiling`), not the ZIP file.
