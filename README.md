# Customer Personality Analysis for Targeted Marketing

Customer segmentation on the Kaggle [Customer Personality Analysis](https://www.kaggle.com/datasets/imakash3011/customer-personality-analysis) dataset. The notebook cleans the data, explores the main distributions, groups customers into 4 segments with K-Means and suggests a marketing approach for each segment. A final section compares other clustering methods and fits a logistic regression for campaign response.

## Data

`marketing_campaign.csv` from Kaggle (tab separated, 2,240 customers and 29 columns): demographics (`Year_Birth`, `Education`, `Marital_Status`, `Income`, kids/teens at home), spending per product category (`MntWines`, `MntMeatProducts`, ...), purchase channels (`NumWebPurchases`, `NumStorePurchases`, ...), `Recency` (days since last purchase) and responses to five earlier campaigns plus the last one (`Response`).

The CSV is not included in this repository. Download it from Kaggle and place it next to the notebook.

## Approach

1. **Cleaning**
   - Missing `Income` values filled with the median.
   - Income outliers removed with a 3 * IQR rule (2,240 -> 2,239 rows).
   - `Education` and `Marital_Status` one-hot encoded.
   - New features: `Age` = 2025 - `Year_Birth`, `Customer_Tenure` = days from `Dt_Customer` to 2025-03-10.
   - `Z_CostContact` and `Z_Revenue` dropped.
2. **EDA**: age and income histograms, total spending per product category, acceptance rate of each campaign, income box plots before and after outlier removal.
3. **Segmentation**: features `Income`, `Age`, `Recency`, `MntWines`, `MntMeatProducts`, `NumWebPurchases`, `NumStorePurchases`, `Customer_Tenure`, standardized, then K-Means with k = 4.
4. **Further experiments**: GMM and DBSCAN on the same features plus `Total_Spending`, elbow curve for k = 1..10, and a logistic regression predicting `Response`.

## Results

K-Means segment means (from the notebook output):

| Segment | Income | Age | Recency (days) | Wine | Meat | Web purchases | Store purchases |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | 33,832 | 52.9 | 48.1 | 37.8 | 22.0 | 2.0 | 3.1 |
| 1 | 62,269 | 60.2 | 24.7 | 473.4 | 172.8 | 6.6 | 8.3 |
| 2 | 79,121 | 53.8 | 52.4 | 713.1 | 580.2 | 4.7 | 8.3 |
| 3 | 60,382 | 61.7 | 74.7 | 399.9 | 150.1 | 5.6 | 7.1 |

How I read the segments and what each could be offered:

- **Segment 0, low income and low spending**: discounts, loyalty points for small purchases, budget bundles, social media ads for low-cost promotions.
- **Segment 1, recent and frequent buyers**: in-store events, bundle offers and a store rewards program.
- **Segment 2, high income with the highest wine and meat spending**: premium wine subscriptions, tasting events, personalized emails about premium brands.
- **Segment 3, similar spending to segment 1 but no purchase for about 75 days**: re-engagement campaigns and "welcome back" incentives.

Logistic regression for `Response` (80/20 split, standardized features including `Total_Spending`): accuracy 0.83 on the test set. The largest coefficients are `Recency` (-0.79), `NumStorePurchases` (-0.68), `Customer_Tenure` (0.53) and `Total_Spending` (0.47). No majority-class baseline was computed, so the accuracy alone does not say much about how useful the model is.

Note: cell 5 of the notebook still shows a shape of (113, 36) from an earlier run. The cells after it re-load the data, so it does not affect the results above.

## Running

```bash
pip install -r requirements.txt
jupyter notebook Customer-Personality-Analysis.ipynb
```

## Files

```
Customer-Personality-Analysis.ipynb   analysis notebook
requirements.txt
LICENSE
```

## License

MIT, see [LICENSE](LICENSE).
