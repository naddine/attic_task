# Customer Purchase Behavior Analysis

# Project Background

This repository contains an analysis of customer purchase behavior data to build simplified customer digital twins for marketing decision-making. The project explores shopping trends, creates customer profiles, and develops predictive models to support strategic marketing initiatives.

# Data Structure

The dataset contains 3,900 customer records and 19 features that may be categorized into:

### Customer Details

1. **Customer ID**: Unique identifier
2. **Age**: Customer age
3. **Gender**: Customer gender
4. **Location**: Geographic location
5. **Subscription Status**: Active subscription (Yes/No)

### Purchase Behavior

1. **Purchase Amount (USD)**: Transaction value
2. **Season**: Purchase season
3. **Preferred Payment Method:** Preferred payment type
4. **Payment Method**: Payment type used
5. **Previous Purchases**: Historical purchase count
6. **Frequency of Purchases**: Purchase frequency category

### Product Details and Preferences

1. **Shipping Type**: Delivery preference
2. **Color**: Product color
3. **Item Purchased**: Specific product bought
4. **Category**: Product category
5. **Size**: Product size
6. **Review Rating**: Customer satisfaction (1-5 scale)
7. **Discount Applied**: Discount received (Yes/No)
8. **Promo Code Used**: Promotional code usage (Yes/No)

| **No.** | **Column** | **Dtype** |
| --- | --- | --- |
| 0 | Customer ID | int64 |
| 1 | Age | int64 |
| 2 | Gender | object |
| 3 | Item Purchased | object |
| 4 | Category | object |
| 5 | Purchase Amount (USD) | int64 |

| **No.** | **Column** | **Dtype** |
| --- | --- | --- |
| 6 | Location | object |
| 7 | Size | object |
| 8 | Color | object |
| 9 | Season | object |
| 10 | Review Rating | float64 |
| 11 | Subscription Status | object |
| 12 | Payment Method | object |

| **No.** | **Column** | **Dtype** |
| --- | --- | --- |
| 13 | Shipping Type | object |
| 14 | Discount Applied | object |
| 15 | Promo Code Used | object |
| 16 | Previous Purchases | int64 |
| 17 | Preferred Payment Method | object |
| 18 | Frequency of Purchases | object |

# Overview of Findings

Customers from the southern US States drive the highest total revenue amounting to ~$75k. Moreover, there are zero female subscribers in the customer base, while 39.7% of male customers are subscribed. This represents a completely untapped market segment worth $29,449 in potential annual revenue. Weekly shoppers are more valuable despite lower per-purchase spending, suggesting that long-run marketing efforts may be target towards weekly timing.

In predictive modeling, Logistic Regression performed best in determining the likelihood of a customer to purchase in the next month.

# Methodology and Approach

- **Exploratory Data Analysis**
    - **Seasons as proxy for time.** Temporal analysis is crucial in business studies. While the dataset lacks detailed time variables—which makes sense since this is a customer database—I used seasons as a proxy to identify purchasing trends.
    - **Standardization and encoding values.**
        - Upon preliminary analysis in Excel, I noticed redundant terms in frequency categories, so I standardized them first before further analysis.
        - The location values are too granular, mapping them into regions might help with patterns and analysis.
        - Since this is marketing focused, it might be more helpful to group customer ages according to "generation".
- **Digital Twins**
    - For the digital twins task, I attempted using K-Means clustering approach, which I realized would be a complicated task given the nature of the dataset being almost perfectly uniform. Therefore, I switched to a more algorithm-based approach with the help of AI.
    - **Profiling.** For this part, I used common profiling algorithms in aggregating the features: psychographic, behavioral, demographic, geographic.
- **Predictive Modeling**
    - The likelihood of a customer to purchase within the next month can be answered by "Yes" or "No", however, this information is not provided by the dataset. In that case, proxy variables can be used by prioritizing features that would contribute to purchase likelihood.
    - Predictive models for classification tasks (Yes, No) were performed:
        1. Logistic Regression
        2. SVM
        3. KNN
        4. Naive Bayes
        5. Random Forest
- **Use of AI.** I used Claude AI and ChatGPT for these analyses.

# EDA Deep Dive

Customers from the South drive the highest total revenue with a total of ~$75k. This is followed by the West USA, Midwest USA, then Northeast USA.

Exploring further the regionality of the customer base, we uncover that:

1. **Southern USA has the highest total number of customers**, with 1,271, unique customers, and the highest subscription rate among the four identified regions with 28.4% subscribed.
2. Despite being the largest contributor to revenue, customers from the South have a lower-than-average customer value (ACV) with $59. **West USA customers has the highest ACV with $61**, a dollar above the average.
3. Across the regions, all item categories perform consistently in terms of customer preference. The **most purchased item is Clothing**, and the least purchased is **Outerwear**.
4. The customer base is composed mainly of "**Boomers**", aged 55 to 70, at ~30%. This is true for all regions except the West, where majority is "Millennials". "GenZers" make up only about 9% of the entire customer base.
5. **Most customers purchase Quarterly or Bi-Weekly, composing 29.4% and 28%** of the customer base, respectively. This purchase frequency behavior is consistent for both genders.

# Predictive Modeling

Despite substandard metrics, **Logistic Regression** performed best in predicting the likelihood of a customer to purchase within the next month.

```
+---------------------+--------------+------------+---------+------------+---------------+---------------+
| Model               |    Pseudo R² |     Adj R² |     AIC |   Accuracy |   Sensitivity |   Specificity |
|---------------------+--------------+------------+---------+------------+---------------+---------------|
| Random Forest       | -0.168449    | -2.26244   | 2250.75 |   0.476923 |      0.587156 |     0.337209  |
| Logistic Regression | -0.00878682  | -0.016617  | 1091.84 |   0.561538 |      0.988532 |     0.0203488 |
| SVM                 |  0.000662233 |  1.33254   | 7309.72 |   0.542308 |      0.949541 |     0.0261628 |
| K-Nearest Neighbors | -0.358738    | -0.367516  | 1464.44 |   0.475641 |      0.5      |     0.444767  |
| Naive Bayes         | -0.00881575  | -0.0219343 | 1099.87 |   0.552564 |      0.979358 |     0.0116279 |
+---------------------+--------------+------------+---------+------------+---------------+---------------+
```

![Screenshot 2025-08-28 at 10.40.35 PM.png](attachment:ee889dc7-99d0-4d6d-af21-271915433978:Screenshot_2025-08-28_at_10.40.35_PM.png)

![Screenshot 2025-08-28 at 10.40.18 PM.png](attachment:14e09ca3-9bba-4a8a-8317-23817cc06f82:Screenshot_2025-08-28_at_10.40.18_PM.png)

# Business Reasoning:

- If you had to design one marketing campaign for the majority of customers, how would you choose the target segment and why?
    - To design a marketing campaign for the majority of customers, I would analyze the dataset to identify the largest customer segment with common characteristics and behaviors. If I were to use choose solely out of the “raw” features, I would pick a customer base that would contribute a large revenue, such as those with highest average spending.
    - As performed in the digital twin section of the activity, I would cluster them according to features that would show high correlation to the company’s metrics. For example, using purchase behavior, I would use **frequency of purchases, preferred payment methods,** and **seasonal trends** to understand when and how this customer base likes to shop⁠⁠.
- Imagine the CEO insists on focusing only on customers with the highest purchase amounts. What risks could this strategy have?
    - Looking at the data at the granular level, there is no consistency in the characteristics of the highest spenders—they cannot be clustered into a customer segment. High spenders are distributed in the customer dataset. If marketing efforts were focused on customers with the highest purchase amounts, it could be a futile effort since the campaigns cannot be tailored or designed to match their behaviors or preferences.
- If two different customer groups respond equally to a campaign in the short term, how could you determine which one is better for the business in the long term?
    - First, I would focus on the long-term goals and KPIs of the business. Customers may respond equally to a short-term campaign, but companies would care more about business success over marketing success. I would analyze the customer groups according to their performance in the business’s long-term metrics for success such as retention rate and lifetime value.
- Suppose your analysis finds that a certain payment method correlates strongly with higher spending. What’s one non-obvious reason this correlation might not mean causation?
    - This could be a case of confounding. The payment method might be the natural preference of customers who are wealthier or those who shop premium. The payment method is not causing high spending, rather, the customers who use the method happen to belong in a segment that spends more due to other factors like lifestyle or economic class.
- Provide 2–3 actionable ideas for how marketing could use the digital twin insights to improve targeting, retention, or revenue.
    - **Targeting**: Marketing teams can use the digital twins to “simulate” how they would react to different campaigns or channels. For example, the customer data can be “fed” to an AI chatbot who will be asked to “role play”.
    - **Retention**: The digital twins can help marketing spot the touch points in which buyers would drop off the customer journey. In the same manner, they can also help identify which parts of the journey buyers would, say, subscribe to a loyalty program. More importantly, the twin can help provide other possible touch points that could drive customer retention.
    - **Revenue**: The digital twins can be utilized to anticipate supply and demand of certain offerings depending on either customer-based features or external factors. For example, if external data is incorporated, the twins can predict which items might be in-demand due to trends in social media or among different age-based generations.

# Assumptions and Caveats:

Throughout the analysis, multiple assumptions were made to manage challenges with the data. These assumptions and caveats are noted below:

- “Bi-Weekly” and “Fortnightly” under the “Frequency of Purchases” column both mean “every two weeks” or “twice a month”.
- Further analysis should be applied for KMeans Clustering, since the data is almost perfectly uniform, which eliminates any natural clusters.
