# customer-churn-analysis
Lookng at data:
customers with long gap since their last purchase show a strong churn signal, which may introduce label leakage. 
Therefore we test models with and without this feature. 
avg "days sice last order" when churn=yes => 81.433
avg "days sice last order" when churn=No => 20.101

shown moderate correlation:
avg "total orders" when churn=yes => 7.07
avg "total orders" when churn=no => 8.84

avg "satisfaction score" when churn=yes => 7.68
avg "satisfaction score" when churn=yes => 8.140

avg "browsing frequency" when churn=yes => 2.55
avg "browsing frequency" when churn=yes => 3.172

avg "engagement_score" when churn=yes => 2.36
avg "engagement_score" when churn=yes => 5.34


not strong predictors:
avg "discount usage rate" when churn=yes => 0.295
avg "discount usage rate" when churn=yes => 0.283

avg "return rate" when churn=yes => 0.836
avg "return rate" when churn=yes => 0.069

avg "cart abandonment rate" when churn=yes => 0.596
avg "cart abandonment rate" when churn=yes => 0.603

# data imbalance rate 
The dataset is moderately imbalanced with a churn rate of 15.48%. if we build a model that classify all the samples n no churn, the accuracy would be 85.52%.
Therefore accuracy alone would be misleading; evaluation will focus on recall and F1-scor

# plotting
We focused on behavioral features likely to correlate with churn (engagement, activity, satisfaction, loyalty).
Boxplots were used to compare distributions between churned and active users, while categorical features were analyzed using churn rate bar charts.
The goal was to visually identify separation between groups before modeling.

# churn vs engagement 
Churned users show significantly lower engagement scores with minimal distribution overlap, suggesting engagement is a strong predictor of churn.


# heatmap and correlations 
highly correlated eatures:
discount_usage_rate & price_sensitivity_index (0.96)

product_review_score_avg & satisfaction_score (0.82)

customer_support_tickets & satisfaction_score (-0.79)
(+ optional: days_since_last_purchase & engagement_score (-0.85))



Correlation insights:
The correlation heatmap shows that some features carry very similar information.

days_since_last_purchase and engagement_score are strongly negatively correlated. Customers who are more engaged tend to purchase more recently. These features describe related behavior, so we should be careful about redundancy.

discount_usage_rate and price_sensitivity_index are almost perfectly correlated. They essentially measure the same concept. Keeping both may introduce multicollinearity in simple models, so we may test models with only one of them.

customer_support_tickets is strongly negatively correlated with satisfaction_score. More support tickets are associated with lower satisfaction, which is intuitive. Either feature may already capture most of this signal.

There are also moderate relationships: product review scores align with satisfaction, browsing frequency contributes to engagement, and older accounts tend to have more total orders. These patterns are consistent with expected customer behavior.


Three pairs of features show strong correlation and may contain redundant information:

discount_usage_rate ↔ price_sensitivity_index (very strong positive correlation)

product_review_score_avg ↔ satisfaction_score (strong positive correlation)

days_since_last_purchase ↔ engagement_score (strong negative correlation)

These pairs likely describe overlapping customer behavior, so we will consider testing models with only one feature from each pair to reduce redundancy.
