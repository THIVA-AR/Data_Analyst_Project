# README — Product Launch Analyst (Power BI)

## Project overview
This project analyzes five years of product launch data to provide actionable insights for stakeholders. I combined five yearly Excel files in Power BI, cleaned and preprocessed the data, and created an interactive dashboard that tracks product launches, costs, and ingredient expenses over time.

## Key goals

Combine and load multi-year Excel files into a single dataset.

Clean and preprocess data to produce an analysis-ready table.

Visualize trends year-over-year for launches, costs, and ingredient expenses.

Provide insights and recommendations to support product planning and budgeting.

## Dataset

Source: Original company dataset (confidential), provided as five separate Excel files (one per year).

Time span: 5 years.

Typical columns (example — adapt to your actual columns):

ProductID, ProductName

LaunchDate, LaunchYear

Category / Subcategory

LaunchCost, IngredientCost, PackagingCost

Region / Market

Status (Launched, Cancelled, Postponed)

Notes / Remarks

Power BI: data loading & preprocessing (steps to reproduce)

Prepare files

Place the five Excel files in a single folder. Ensure consistent column names and formats across files.

## Get data 

In Power BI Desktop: Home -> Get data -> More -> Folder.

Point to the folder containing the five Excel files.

Click Transform Data to open Power Query Editor.

Combine files

In Power Query, use the combined binaries transformation: click "Combine" -> "Combine & Load" (Power Query will create sample queries).

Inspect the combined query and the sample query to ensure data types and column names are consistent.

Clean & transform (Power Query steps to apply)

Remove unnecessary columns.

Rename columns to consistent, descriptive names (e.g., LaunchDate, LaunchCost).

Change data types: dates, numbers, text.

Parse dates and extract LaunchYear using Date.Year(LaunchDate).

Handle missing values: replace nulls, use sensible defaults for numeric columns (e.g., 0 for cost when appropriate) or filter rows as needed.

Remove duplicates by ProductID + LaunchDate (if applicable).

Standardize categorical values (trim, case normalization).

Create calculated columns: LaunchYear, TotalCost (sum of cost components), CostPerIngredientRatio (IngredientCost / LaunchCost) where meaningful.

Load the final cleaned table to Power BI data model.

Data model & measures (example DAX)

Total Launches = DISTINCTCOUNT(Table[ProductID]) or COUNTROWS for deduplicated table

Launches by Year = COUNTROWS(FILTER(Table, Table[LaunchYear] = selectedYear))

Avg Launch Cost = AVERAGE(Table[LaunchCost])

Avg Ingredient Cost = AVERAGE(Table[IngredientCost])

Avg Ingredient % = DIVIDE([Avg Ingredient Cost], [Avg Launch Cost], 0)

Total Cost = SUM(Table[TotalCost])

Visuals and dashboard components

KPI cards: Total launches (5-year), Latest year launches, Avg launch cost, Avg ingredient cost.

Time series line chart: Launches by year (year-over-year trend).

Bar chart: Total launches by category or region.

Matrix or table: Top N products by launch cost or by ingredient cost.

Scatter plot: LaunchCost vs IngredientCost (identify outliers).

Stacked column or 100% stacked column: Cost breakdown (ingredient vs other) over years.

Map visual: Launches by region (if geo data available).

Filter/slicer pane: Year, Category, Region, Status.

Drillthrough/details page: Product-level details, launch notes.

Key insights (example text — replace with your actual findings)

Year-over-year trends: e.g., launches increased by X% from Year1 to Year5, with a dip in Year3 likely due to market conditions.

Average costs: Average launch cost across five years is ₹X; ingredient cost represents Y% of total on average.

High-cost launches: A small subset (~Z%) of products account for a disproportionate share of total launch expenditure.

Category insights: Category A shows the highest average launch cost but lower average ingredient share; Category B has frequent launches with lower per-launch cost.

Regional patterns: Region 1 accounts for the majority of launches; Region 3 shows rapid growth in the most recent years.

Anomalies: Identified outlier launches with exceptionally high ingredient costs — recommend review for data quality or process changes.

## Files in this repository

/data/— sample or sanitized input files.

/powerbi/ — Power BI file(s): ProductLaunchAnalysis.pbix 

/docs/README.md — this README file

/screenshots/ — dashboard screenshots 

/scripts/ — any helper scripts used for data checks or exports (Python / R)

/notes/ — data dictionary and transformation notes

### How to open the PBIX

Install Power BI Desktop (latest version).

Open ProductLaunchAnalysis.pbix.

If data sources are offline or confidential, go to Transform Data -> Data source settings to update folder path or point to the local copies.

Refresh the dataset after updating the folder path.

### Assumptions & limitations

Dataset columns and format were assumed consistent across yearly files. If column mismatches exist, combine step needs manual mapping.

Confidential data omitted from repository. Use sanitized samples if you want a public example.

Business context (e.g., reasons for cost changes) requires domain input; dashboard highlights patterns but not causal claims.

### Recommendations & next steps

Add forecasting: use time-series forecasting (Power BI built-in forecast or export to Python/R) to predict launches and costs for the next year.

Cost driver analysis: perform regression or SHAP analysis in Python to quantify drivers of launch cost.

A/B outcome tracking: link launch data to product performance (sales, retention) to measure ROI.

Automation: schedule refresh in Power BI Service with gateway to keep the dashboard updated.

Data quality pipeline: implement validation checks at ingestion (missing costs, negative values).

### License & privacy

This repository excludes sensitive or personally identifiable data. Do not upload confidential spreadsheets to public repos.

License: specify a license you prefer (e.g., MIT) or keep repository private.
