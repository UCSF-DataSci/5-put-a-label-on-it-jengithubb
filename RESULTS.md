# Assignment 5: Health Data Classification Results

This file contains your manual interpretations and analysis of the model results from the different parts of the assignment.

## Part 1: Logistic Regression on Imbalanced Data

### Interpretation of Results

In this section, provide your interpretation of the Logistic Regression model's performance on the imbalanced dataset. Consider:

- Which metric performed best and why?
- Which metric performed worst and why?
- How much did the class imbalance affect the results?
- What does the confusion matrix tell you about the model's predictions?

*Interpretation*
The metric that performed best is accuracy (0.9168).The model is very good at predicting the majority class (True Negatives = 1301), which inflates the overall accuracy due to the class imbalance.

The metric that performed worst is recall (0.3007). This means that the model only correctly identified about 30% of the actual positive cases. It shows the model only identified 43 out of 143 actual positive cases (TP + FN = 43 + 100). That’s why recall is low, it missed 100 positive cases (high false negatives).

The imbalance impact score is 0.361, which signals that the difference between precision and recall is non-negligible. Precision is moderate, but recall suffers, suggesting the model tends to favor predicting the majority class.

The model is biased toward predicting negative outcomes. It rarely mislabels negatives (only 22 FP), but frequently misses positives (100 FN). This is a classic sign of class imbalance, where the minority class (positive) is under-represented and under-predicted.

## Part 2: Tree-Based Models with Time Series Features

### Comparison of Random Forest and XGBoost

In this section, compare the performance of the Random Forest and XGBoost models:

- Which model performed better according to AUC score?
- Why might one model outperform the other on this dataset?
- How did the addition of time-series features (rolling mean and standard deviation) affect model performance?

*Interpretation*
XGBoost performed better (AUC = 0.9953) compared to Random Forest (AUC = 0.9735).

XGBoost often outperforms Random Forest because it uses gradient boosting, which optimizes errors sequentially and handles complex patterns more effectively. It’s more sensitive to subtle patterns in data and better at reducing bias.

Adding time-series features provided additional temporal context, improving model discrimination ability. These features likely helped the models capture trends and variability, contributing to higher AUCs overall.


## Part 3: Logistic Regression with Balanced Data

### Improvement Analysis

In this section, analyze the improvements gained by addressing class imbalance:

- Which metrics showed the most significant improvement?
- Which metrics showed the least improvement?
- Why might some metrics improve more than others?
- What does this tell you about the importance of addressing class imbalance?

*Interpretation*
Recall showed the biggest improvement: from 0.3007 to 0.8531 (+183.72%). This confirms that handling class imbalance helped the model detect far more true positives.

Precision dropped by 41.26%, and F1 score stayed nearly the same (0% change). Accuracy also decreased slightly (−6.77%).

Balancing the data with SMOTE helped the model focus more on the minority class, boosting recall. But this increased false positives, lowering precision. F1 (harmonic mean of both) didn’t change much because gain in recall was offset by drop in precision.

It shows that ignoring class imbalance leads to models that miss critical minority cases. Fixing imbalance greatly improves recall (sensitivity), which is essential in medical or fraud detection contexts. However, trade-offs like reduced precision must be managed based on the application.

## Overall Conclusions

Summarize your key findings from all three parts of the assignment:

- What were the most important factors affecting model performance?
- Which techniques provided the most significant improvements?
- What would you recommend for future modeling of this dataset?

*Interpretation*
Class imbalance and feature engineering (time-series features) had the biggest impact on model performance.

Balancing the dataset drastically improved recall. XGBoost with engineered features achieved the best AUC.

Use tree-based models with engineered time-series features and always address class imbalance for better sensitivity.
