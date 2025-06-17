# Data-analysis-project

Date: Date of transaction
Product: Product sold
Category: Product category
Quantity: Number of units sold 
Price: Price per unit
Revenue: Calculated as Quantity × Price


Summary statistics (mean, max, min, etc.)
Total revenue by category
Top 5 best-selling products
Revenue trend over time (line chart)


code ---

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Set up visualization
sns.set(style="whitegrid")

# Generate sample data
np.random.seed(42)
dates = pd.date_range(start="2024-01-01", periods=100)
products = ['Laptop', 'Phone', 'Tablet', 'Monitor', 'Headphones']
categories = {'Laptop': 'Electronics', 'Phone': 'Electronics', 'Tablet': 'Electronics',
              'Monitor': 'Accessories', 'Headphones': 'Accessories'}

data = {
    'Date': np.random.choice(dates, 100),
    'Product': np.random.choice(products, 100),
}

df = pd.DataFrame(data)
df['Category'] = df['Product'].map(categories)
df['Quantity'] = np.random.randint(1, 10, size=100)
df['Price'] = df['Product'].map({
    'Laptop': 1000,
    'Phone': 700,
    'Tablet': 400,
    'Monitor': 200,
    'Headphones': 100
})
df['Revenue'] = df['Quantity'] * df['Price']

# 1. Summary statistics
print("\nSummary Statistics:")
print(df.describe())               

# 2. Total revenue by category
revenue_by_cat = df.groupby('Category')['Revenue'].sum()
print("\nTotal Revenue by Category:")
print(revenue_by_cat)

# 3. Top 5 best-selling products
top_products = df.groupby('Product')['Quantity'].sum().sort_values(ascending=False).head(5)
print("\nTop 5 Best-Selling Products:")
print(top_products)

# 4. Revenue trend over time
df_daily = df.groupby('Date')['Revenue'].sum().reset_index()

plt.figure(figsize=(10, 5))
sns.lineplot(data=df_daily, x='Date', y='Revenue')
plt.title('Daily Revenue Trend')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()


to run this  
Install the necessary libraries if you haven’t already:Install the necessary libraries if you haven’t already:

  (pip install pandas matplotlib seaborn)
