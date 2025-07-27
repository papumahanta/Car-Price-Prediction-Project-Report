#  Car Price Prediction Project

This project involves data preprocessing, feature engineering, and regression modeling (Ridge & Random Forest) to predict car prices based on various specifications.

---

##   Dataset Overview

- Source: `CarPrice_Assignment.csv`
- Rows: 205 → Cleaned: 190 (after handling missing values and outliers)
- Target Variable: `price`

---

##  Phase 1: Data Understanding & Cleaning

###  Exploratory Data Analysis (EDA)
- Checked null values, datatypes, and statistics.
- Target variable `price` is right-skewed → `np.log(price)` recommended.
- Key predictors: `curbweight`, `enginesize`, `horsepower`

###  Data Cleaning
- Filled missing values (mode for categorical, median for numerical)
- Removed duplicates and outliers using IQR method.

---

##   Phase 2: Feature Engineering & Multicollinearity Handling

###  Engineered Features
- `size_index` = average of wheelbase, carlength, carwidth
- `power_to_weight` = horsepower / curbweight

###  Transformations
- Applied log-transform to: `enginesize`, `horsepower`, and `price`

###  Multicollinearity Detection
- Used VIF (Variance Inflation Factor)
- Removed features with VIF > 7
- Ridge Regression chosen to handle remaining multicollinearity

---

##  Phase 3: Modeling

###  Ridge Regression
- **Train R²**: 0.825
- **Test R²**: 0.806
- Selected due to its robustness against multicollinearity.

###  RidgeCV (with alpha tuning)
- Best Alpha: `0.01`
- **Train R²**: 0.830
- **Test R²**: 0.808
- Improved generalization slightly.

```output
```text
=== RidgeCV MODEL SUMMARY ===
Training R² : 0.8299
Testing R² : 0.8079
MAE        : 2849.82
RMSE       : 3894.05
MAPE       : 1.19%

=== RidgeCV Coefficients ===
Feature            | Coefficient
------------------ | -------------
power_to_weight    | 42973.222323
symboling          |   378.162378
compressionratio   |   291.657506
carheight          |   197.839627
size_index         |   157.803756
enginesize         |   132.668117
peakrpm            |     2.815105
highwaympg         |  -197.924492
```

 

###  Random Forest Regressor
- **Train R²**: 0.984
- **Test R²**: 0.953
- **MAE**: 1403
- **RMSE**: 1929
-**MAPE**: 1.19%
- Captured non-linear interactions better.

---

##  Model Evaluation

- Residuals are mostly normally distributed with slight heteroscedasticity.
- Q–Q plot confirms residual normality.
- Random Forest outperforms Ridge in prediction accuracy.

---

##  Final Model Recommendation

>  **Best Model: Random Forest Regressor**  
> Use this model for production/deployment due to its superior accuracy and ability to capture complex patterns.

---

##  Notes & Future Work

- Consider encoding categorical variables (`fueltype`, `carbody`, `drivewheel`)
- Feature interaction terms (e.g., aspiration × enginetype) may improve performance
- Explore further models like Gradient Boosting or XGBoost.

---

**Goal Achieved**: Built a robust, interpretable, and high-performing car price prediction model.
