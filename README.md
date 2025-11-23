#### 3. Data Processing Methodology (Part 1 & 2)
A. Scraping Methodology (Part 1)
Categories: 5 categories are selected (e.g., Drones, Smart Devices, Tools, etc.).

Libraries: requests and BeautifulSoup are used for initial HTML parsing. Selenium is employed to handle JavaScript rendering and implement pagination across multiple result pages to maximize data coverage.

B. Cleaning & Transformation Steps (Part 2)
Price Cleaning: A Regular Expression is used to extract the numeric value for the Price_Clean column, handling currency symbols and price ranges.

Missing Values: Rows missing critical data (Name, Category, Price_Clean) are dropped. Missing Rating values are imputed using the mean rating of their respective category.

Derived Features:

Name_Word_Count: The total number of words in the product name (proxy for product specificity).

Price_Category_Rank: The product's relative price rank within its own category, calculated using df.groupby('Category')['Price_Clean'].rank(method='min', ascending=False).

📊 4. Analysis and Insights (Part 3 & 5)
Python Exploratory Analysis (Part 3)
The 04_eda_analysis.py script performs the following analyses with visual output:

Price Distribution per Category: Uses a Box Plot to analyze the median, spread, and outliers of prices.

Rating vs. Price Correlation: Uses a Scatter Plot to identify the strength and direction of the linear relationship between the two variables.

Top Reviewed Products: Identifies the top 10 products by review count (a strong proxy for demand).

Best Value Metric: Calculates the Rating / Price_Clean score to find products offering the best customer satisfaction relative to cost.

Stock Availability Analysis (Proxy): Uses the average Price_Category_Rank per category to simulate inventory turnover risk (lower rank = potentially faster-moving/cheaper stock).

SQL Aggregated Analysis (Part 5)
The following queries are run directly on the SQL database to extract business intelligence:

Core Metrics: Calculates the Average Price, Average Rating, and Product Count for every Category.

Top 5 Reviewed Items: Uses a CTE and ROW_NUMBER() with PARTITION BY Category to list the top 5 most-reviewed products in each group
