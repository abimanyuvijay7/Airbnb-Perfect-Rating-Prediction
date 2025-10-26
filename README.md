# Airbnb Perfect Rating Prediction

This project predicts whether an **Airbnb listing will achieve a perfect (100%) rating score** using data on listing features, host behavior, and property characteristics.  
It was completed as part of the **BUDT 758T: Data Mining and Predictive Analytics** course at the University of Maryland.

---

## Project Overview

Airbnb listings are evaluated by guests across multiple factors such as cleanliness, accuracy, communication, and location.  
Perfect ratings (100%) indicate exceptional guest satisfaction and can significantly impact listing visibility and host revenue.

This project builds machine learning models to predict **which listings are most likely to receive perfect ratings** and identifies the most influential features driving those outcomes.

---

## Business Objective

**Goal:**  
To predict listings that are likely to earn a perfect rating while keeping the **False Positive Rate (FPR) below 10%**.

**Use Cases:**
- **Hosts & Property Managers:** Identify which listings need improvements to increase the chances of earning perfect ratings.  
- **Airbnb’s Internal Analytics Teams:** Detect underperforming listings early, improve host guidance, and enhance guest experience.

---

## Data Understanding and Preparation

We processed **42 fields** and engineered **20 final features** used in the models.  
Data preparation involved extensive cleaning, transformation, and feature engineering.

### Key Engineered Features
| Feature | Description |
|----------|--------------|
| `bed_category` | Consolidated bed types into fewer groups |
| `property_category` | Simplified property type categories |
| `host_response_rate`, `host_acceptance_rate` | Cleaned and converted to numeric |
| `has_cleaning_fee`, `has_security_deposit` | Binary flags derived from raw data |
| `host_tenure_days` | Derived from host start date and first review date |
| `days_from_first_review` | Time since listing’s first review |

### Data Cleaning Summary
- Filled missing numeric values with mean.
- Replaced missing categorical values with `"Not available"`.
- Applied one-hot encoding for categorical variables.
- Normalized rates and prices.
- Reduced multicollinearity through categorical consolidation.

---

## Modeling and Evaluation

We tested three models: Logistic Regression, Random Forest, and XGBoost.  
Performance was evaluated using True Positive Rate (TPR), False Positive Rate (FPR), and Accuracy.

| Model | Accuracy | TPR | FPR | Notes |
|--------|-----------|-----|-----|-------|
| Logistic Regression | 0.73 | 0.20 | 0.06 | Low recall, conservative predictions |
| Random Forest | 0.73 | 0.30 | 0.09 | Better recall but near FPR limit |
| **XGBoost (Final)** | **0.65** | **0.35** | **0.099** | Best tradeoff between recall & precision |

### Final Model (XGBoost)
- **n_estimators:** 300  
- **max_depth:** 3  
- **min_child_weight:** 7  
- **learning_rate:** 0.2  
- **Threshold:** 0.78 (optimized for <10% FPR)  
- **Final Performance:**  
  - **TPR:** 0.3487  
  - **FPR:** 0.0991  
  - **AUC:** 0.68  

---

## Visual Insights

- **Price vs Rating:** Listings with slightly higher median prices tend to receive more perfect ratings.  
- **Room Type:** Entire homes/apartments are more likely to achieve perfect ratings than shared rooms.  
- **Cancellation Policy:** Flexible policies correlate with higher guest satisfaction.  
- **Cleaning Fee:** Listings without a cleaning fee perform better.  
- **Response Time:** Faster host responses correlate positively with ratings.

---

## Techniques & Tools

**Languages & Libraries**
- Python  
- pandas, numpy, matplotlib, seaborn  
- scikit-learn, xgboost, scipy  

**Methods**
- Feature engineering and encoding  
- Hyperparameter tuning  
- Threshold optimization (tradeoff between TPR and FPR)  
- ROC curve and fitting curve visualization  

---

## Key Takeaways
- **Feature engineering** significantly impacts predictive performance.  
- **Threshold tuning** is essential when optimizing for both recall and FPR.  
- **XGBoost** effectively handled class imbalance and produced the most reliable predictions.  
- Business insights from this model can help Airbnb and hosts improve listing quality and customer satisfaction.

---

## 👥 Team Members
- **Abimanyu Vijay Krishnamoorthy**  
- Maitreyee Tiwari  
- Rohan Vasudevan  
- Pranav Bharatwaj Manikantan  
- Aditya Kaushik  

---

## 📜 License
This project is open-sourced under the [MIT License](LICENSE).
