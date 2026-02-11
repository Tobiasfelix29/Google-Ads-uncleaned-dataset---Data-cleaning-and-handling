Google Ads Sales Data Cleaning and Preprocessing
Project Overview

This project focuses on performing comprehensive data cleaning and preprocessing on an unstructured Google Ads sales dataset using Python and Pandas. The primary objective was to transform raw, inconsistent marketing campaign data into a structured, analysis-ready dataset suitable for exploratory data analysis, reporting, and business intelligence applications.

Dataset Description:
The dataset contains 2,600 records of Google Ads campaign performance, including:

Ad_ID
Campaign_Name
Clicks
Impressions
Cost
Leads
Conversions
Conversion Rate
Sale_Amount
Ad_Date
Location
Device
Keyword

The dataset contained multiple real-world data quality issues, including missing values, inconsistent formats, mixed data types, and derived metrics stored incorrectly.

Data Cleaning Process:
The following preprocessing steps were performed:

1. Missing Value Handling
Identified null values using isnull() and column-wise inspection.Applied multiple imputation techniques based on business logic:
         Forward fill and backward fill for time-based fields.
         Median imputation for skewed numerical columns such as Cost and Impressions.
         Zero filling for count-based fields such as Leads and Conversions.
         Selective row removal using dropna() where appropriate.

2. Data Type Corrections
Converted currency fields (Cost, Sale_Amount) from string format (e.g., "$231.88") to numeric float values.
Standardized and converted mixed date formats in Ad_Date using pd.to_datetime().

3. Text Standardization
Normalized categorical fields (Device, Location) by standardizing case and removing whitespace.
Corrected inconsistencies in campaign naming for uniform reporting.

4. Derived Metric Recalculation
Recomputed Conversion Rate using: Conversion Rate = Conversions / Clicks
Ensured all performance metrics were logically consistent and analytically accurate.

Outcome
The final output is a fully cleaned, validated, and structured dataset with:
        1.Consistent data types
        2.No unresolved missing values
        3.Standardized categorical variables
        4.Accurate performance metrics

This dataset is now ready for Exploratory Data Analysis (EDA)

Tools used :
Goggle collab 
