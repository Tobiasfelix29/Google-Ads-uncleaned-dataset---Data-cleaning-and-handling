import pandas as pd
# 1. Load Dataset
df = pd.read_csv("GoogleAds_DataAnalytics_Sales_Uncleaned.xlsx")

print("Initial Shape:", df.shape)
print("\nInitial Missing Values:\n", df.isnull().sum())

# 2. Clean Currency Columns
df['Cost'] = (
    df['Cost']
    .astype(str)
    .str.replace('$', '', regex=False)
    .str.replace(',', '', regex=False)
)

df['Sale_Amount'] = (
    df['Sale_Amount']
    .astype(str)
    .str.replace('$', '', regex=False)
    .str.replace(',', '', regex=False)
)

df['Cost'] = pd.to_numeric(df['Cost'], errors='coerce')
df['Sale_Amount'] = pd.to_numeric(df['Sale_Amount'], errors='coerce')

# 3. Convert Date Column
df['Ad_Date'] = pd.to_datetime(df['Ad_Date'], errors='coerce')

# 4. Standardize Text Columns
df['Location'] = df['Location'].str.lower().str.strip()
df['Device'] = df['Device'].str.lower().str.strip()
df['Campaign_Name'] = df['Campaign_Name'].str.strip()

# 5. Handle Missing Values
# Median imputation for numeric columns
df['Clicks'].fillna(df['Clicks'].median(), inplace=True)
df['Impressions'].fillna(df['Impressions'].median(), inplace=True)
df['Cost'].fillna(df['Cost'].median(), inplace=True)

# Zero fill for count-based columns
df['Leads'].fillna(0, inplace=True)
df['Conversions'].fillna(0, inplace=True)
df['Sale_Amount'].fillna(0, inplace=True)

# Forward fill for date column
df['Ad_Date'].fillna(method='ffill', inplace=True)

# 6. Recalculate Conversion Rate
df['Conversion Rate'] = df['Conversions'] / df['Clicks']

# 7. Final Validation
print("\nMissing Values After Cleaning:\n", df.isnull().sum())
print("\nFinal Shape:", df.shape)
print("\nFinal Preview:\n", df.head())

# 8. Export Cleaned Dataset
df.to_csv("GoogleAds_DataAnalytics_Sales_Cleaned.csv", index=False)


