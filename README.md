# Adidas US Sales Analysis & Interactive Power BI Dashboard (2020–2021)

[![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Cleaning-150458?logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)](https://jupyter.org/)

> End-to-end retail analytics workflow combining Python data cleaning and exploratory data analysis (`Cleaning Data.ipynb`) with an interactive Power BI executive dashboard (`Adidas US Sales 2020-2021 Dashboard.pbix`) across **9,648 US retail transactions** totaling **\$899.90M** in sales.

---

## Background & Problem Statement

In multi-channel retail operations spanning dozens of states, cities, and partner retailers, raw transactional exports rarely arrive ready for executive reporting. The raw Adidas US Sales Excel workbook (`Adidas US Sales Datasets.xlsx`) embeds title/metadata rows above the actual header, mixes string-formatted currency (`$50.00`), comma-separated quantities (`1,200`), and percentage strings (`50%`), and lacks higher-level product groupings (gender segment and product category).

Without standardized preprocessing and interactive slicing, business stakeholders cannot easily answer key commercial questions:
- Which US regions, states, and retail partners drive the highest revenue and operating profit?
- How did Adidas US sales scale between 2020 and 2021 across quarterly cycles?
- Which sales channels (`In-store`, `Outlet`, `Online`) and product lines (`Footwear` vs. `Apparel`, `Men` vs. `Women`) deliver the strongest margin and volume?

---

## Objectives & Business Impact

- **Standardize Raw Retail Data:** Parse and clean 9,648 multi-channel sales records into numeric, date-indexed, analysis-ready fields and derive `Year`, `Gender`, and `Type` dimensions.
- **Identify Revenue & Profit Drivers:** Quantify performance across 6 major US retailers, 5 geographic regions, 50 states, and 52 cities.
- **Enable Self-Service BI Exploration:** Deliver an interactive Power BI report (`Duplikat Final Dasboard`) with 7 dynamic slicers and 9 visual components so decision-makers can drill down by time, geography, channel, and product mix.

---

## Dataset Overview

- **Source File:** `Adidas US Sales Datasets.xlsx` (sheet: `Data Sales Adidas`)
- **Clean Record Count:** **9,648 rows × 13 original columns** (after removing 4 leading metadata/blank rows in the Excel sheet)
- **Time Span:** January 1, 2020 – December 31, 2021
- **Coverage:**
  - **6 Retailers:** `West Gear`, `Foot Locker`, `Sports Direct`, `Kohl's`, `Walmart`, `Amazon`
  - **5 Regions:** `West`, `Northeast`, `Southeast`, `South`, `Midwest` (covering **50 states** and **52 cities**)
  - **6 Products:** `Men's Street Footwear`, `Men's Athletic Footwear`, `Women's Street Footwear`, `Women's Athletic Footwear`, `Men's Apparel`, `Women's Apparel`
  - **3 Sales Methods:** `Online` (4,889 tx), `Outlet` (3,019 tx), `In-store` (1,740 tx)

| Column | Description |
| :--- | :--- |
| `Retailer`, `Retailer ID` | Retail partner name and numeric identifier |
| `Invoice Date` | Transaction date (`2020-01-01` to `2021-12-31`) |
| `Region`, `State`, `City` | US geographic hierarchy |
| `Product` | Product line combining target gender and category |
| `Price per Unit`, `Units Sold` | Unit retail price (USD) and volume sold |
| `Total Sales`, `Operating Profit`, `Operating Margin` | Gross sales revenue, operating profit, and profit margin |
| `Sales Method` | Distribution channel (`In-store`, `Outlet`, `Online`) |

---

## Repository Structure

```text
Data-visualization-with-power-BI/
├── Adidas US Sales 2020-2021 Dashboard.pbix   # Interactive Power BI report (19 visual components)
├── Adidas US Sales Datasets.xlsx              # Raw Adidas US retail sales dataset (2020–2021)
├── Cleaning Data.ipynb                        # Python data cleaning, feature engineering & EDA notebook
└── README.md
```

---

## Methodology & Workflow

### 1. Data Cleaning & Feature Engineering (`Cleaning Data.ipynb`)
1. **Inspection & Validation:** Verified dataset dimensions `(9648, 13)` and confirmed zero missing values across all 13 columns.
2. **Numeric Parsing:** Stripped currency symbols (`$`) and thousand separators (`,`) from `Price per Unit`, `Total Sales`, `Units Sold`, and `Operating Profit`, casting them to `float`.
3. **Date & Feature Engineering:**
   - Extracted `Year` (`2020`, `2021`) and parsed `Invoice Date` (`%d-%m-%Y`) as a `DatetimeIndex` for quarterly resampling (`resample('Q')`).
   - Derived `Gender` (`Men`, `Women`) and product `Type` (`Footwear`, `Apparel`) from the `Product` column.
4. **Exploratory Visual Analysis:** Generated Matplotlib/Seaborn breakdowns across retailers, regions, top/bottom 10 states, top/bottom 20 cities, quarterly sales vs. profit trends, product categories, gender/type splits, and a numerical correlation matrix.

### 2. Interactive Power BI Dashboard (`Adidas US Sales 2020-2021 Dashboard.pbix`)
The report page (`Duplikat Final Dasboard`) integrates **19 visual elements**:
- **7 Interactive Slicers:** `SALES METHOD`, `PRODUCT`, `GENDER`, `REGION`, `CITY`, `MONTH`, `YEAR`
- **Geographic & Channel Visuals:** `Total Sales by State`, `Total Sales by City`, `Total Sales by Method Sales`
- **Product & Segment Visuals:** `Total Sales by Product` (donut), `Total Sales by Gender` (donut)
- **Time-Series & Profitability Visuals:** `Total Sales by Year` (donut), `Total Sales by Month` (column), `Average Total Sales by Operating Profit` (line), and `Average Monthly Sales` (table)

---

## Results & Key Insights

### Overall Performance (2020–2021)

| Metric | 2020 | 2021 | Total (2020–2021) |
| :--- | :---: | :---: | :---: |
| **Total Sales** | \$182,080,675 | \$717,821,450 | **\$899,902,125** |
| **Operating Profit** | \$63,375,710 | \$268,759,412 | **\$332,135,122** |
| **Units Sold** | 462,349 | 2,016,512 | **2,478,861** |

- **Year-over-Year Surge:** Total sales grew **+294.2%** from 2020 to 2021, while units sold increased **+336.1%**.
- **Top Regions:** **West** leads with **\$269,943,182** in sales (`\$89,609,516` profit; `686,985` units), followed by **Northeast** (`\$186,324,067`), **Southeast** (`\$163,171,236`), **South** (`\$144,663,181`), and **Midwest** (`\$135,800,459`).
- **Top Retailers:** **West Gear** (`\$242.96M` sales, `625,262` units), **Foot Locker** (`\$220.09M`, `604,369` units), and **Sports Direct** (`\$182.47M`, `557,640` units) account for over 71% of total revenue.
- **Top States & Cities:** **New York** (`\$64.23M`), **California** (`\$60.17M`), **Florida** (`\$59.28M`), and **Texas** (`\$46.36M`) lead state sales; **Charleston** (`\$39.97M`) and **New York City** (`\$39.80M`) are the top-grossing cities.
- **Product & Segment Mix:** **Footwear** generates **\$597.13M** (66.4% of sales) vs. **Apparel** at **\$302.77M** (33.6%), led by `Men's Street Footwear` (**\$208.83M**). Men's products account for **\$486.23M** (54.0%) vs. Women's **\$413.67M** (46.0%).
- **Channel Dynamics:** Although `Online` has the most transactions (`4,889`), **`In-store`** produces the highest total revenue (**\$356.64M** from 1,740 transactions), ahead of `Outlet` (**\$295.59M**) and `Online` (**\$247.67M**).
- **Strong Linear Drivers:** Correlation analysis confirms `Total Sales` correlates strongly with `Operating Profit` (**0.96**) and `Units Sold` (**0.91**), while `Price per Unit` shows a moderate correlation (**0.44**).

---

## How to Run & Use

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Bimzt/Data-visualization-with-power-BI.git
   cd Data-visualization-with-power-BI
   ```
2. **Explore the Power BI Dashboard:**
   - Install **Microsoft Power BI Desktop** (Windows).
   - Open `Adidas US Sales 2020-2021 Dashboard.pbix` and use the slicers on the `Duplikat Final Dasboard` page to filter across channels, regions, years, and products.
3. **Reproduce the Python Cleaning & EDA Notebook:**
   ```bash
   pip install pandas numpy matplotlib seaborn jupyter openpyxl
   ```
   - Export sheet `Data Sales Adidas` (starting from the header row `Retailer`) in `Adidas US Sales Datasets.xlsx` to `Adidas US Sales Datasets.csv`, or update Cell 1 in `Cleaning Data.ipynb` to `pd.read_excel('Adidas US Sales Datasets.xlsx', skiprows=4)`.
   - Launch `jupyter notebook "Cleaning Data.ipynb"` and run all cells sequentially.

---

## Notes & Limitations

- `Cleaning Data.ipynb` references `Adidas US Sales Datasets.csv`, whereas the repository ships the original `Adidas US Sales Datasets.xlsx` workbook (containing 4 leading header/blank rows before column headers).
- In the raw `.xlsx`, `Operating Profit` sums to `\$332,134,761.45` (vs. `\$332,135,122.00` in the CSV loaded by the notebook due to integer rounding on export).
- Future enhancements could include adding DAX year-over-year growth cards, profit-margin heatmaps by retailer × channel, and a direct Power Query connection pointing cleanly to the `.xlsx` source.
