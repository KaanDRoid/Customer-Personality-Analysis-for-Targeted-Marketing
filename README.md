# Customer Personality Analysis for Targeted Marketing

## Overview
This project analyzes customer demographics and purchasing behavior using the [Customer Personality Analysis dataset](https://www.kaggle.com/datasets/imakash3011/customer-personality-analysis) from Kaggle. By applying machine learning techniques, the project segments customers into distinct groups and provides tailored marketing strategies to enhance customer engagement and optimize sales.

## Steps
1. **Data Cleaning and Preprocessing**:
   - Filled missing values in the 'Income' column (24 missing entries) with the median.
   - Removed outliers in 'Income' using the 3 * IQR method, reducing the dataset from 2240 to 2239 rows.
   - Encoded categorical variables ('Education' and 'Marital_Status') using one-hot encoding.
   - Created new features: 'Age' (calculated as 2025 - Year_Birth) and 'Customer_Tenure' (days since customer registration).
   - Dropped less informative columns ('Z_CostContact', 'Z_Revenue').

2. **Exploratory Data Analysis (EDA)**:
   - Visualized key patterns, including age distribution, income vs. age scatter plot, total spending by product category (e.g., wines, meat), and campaign acceptance rates.
   - Analyzed income distribution before and after outlier removal to ensure data quality.

3. **Customer Segmentation**:
   - Used K-Means clustering (with standardized features) to group customers into 4 distinct segments.
   - Selected features for clustering: 'Income', 'Age', 'Recency', 'MntWines', 'MntMeatProducts', 'NumWebPurchases', 'NumStorePurchases', and 'Customer_Tenure'.
   - Visualized segments using scatter plots (e.g., Income vs. Wine Spending).

4. **Marketing Recommendations**:
   - Developed data-driven marketing strategies for each segment based on their characteristics (see below).

## Tools Used
- Python (Pandas, NumPy, Scikit-learn)
- Data Visualization (Matplotlib, Seaborn)
- Jupyter Notebook

## How to Run
1. Clone this repository:
2. Install the required libraries: `pip install -r requirements.txt`
3. Open the Jupyter Notebook: `Customer_Personality_Analysis.ipynb`
4. Run the notebook to see the analysis.

## Results
- Identified 4 distinct customer segments using K-Means clustering with machine learning techniques.
- Visualized the segments (e.g., Income vs. Wine Spending scatter plot):
![Customer Segments: Income vs. Wine Spending](images/income_vs_wine_spending.png)
- Segment Characteristics (Mean Values):
- **Segment 0**: Low income (33,832), low wine spending (37.8), moderate recency (48.1 days).
- **Segment 1**: Middle-high income (62,269), moderate-high wine spending (473.4), low recency (24.7 days), high store purchases (8.3).
- **Segment 2**: High income (79,121), high wine spending (713.1), very high meat spending (580.2).
- **Segment 3**: Middle-high income (60,382), moderate wine spending (399.9), high recency (74.7 days).
- Provided actionable marketing strategies for each segment:
- **Segment 0**: Budget-friendly discounts, loyalty programs, and social media ads for affordable products.
- **Segment 1**: In-store events, bundled offers, and store-specific rewards programs.
- **Segment 2**: Premium wine subscriptions, exclusive events, and VIP memberships.
- **Segment 3**: Personalized re-engagement campaigns, luxury incentives, and "welcome back" discounts.

## Future Improvements
- Experiment with alternative clustering algorithms (e.g., Gaussian Mixture Models, DBSCAN) to uncover more nuanced segments.
- Use the Elbow Method to determine the optimal number of clusters for K-Means.
- Add more feature engineering, such as total spending or purchase frequency metrics, to enhance segmentation.
- Incorporate predictive modeling to forecast customer responses to proposed marketing campaigns.

## License
This project is licensed under the [MIT License](LICENSE).
