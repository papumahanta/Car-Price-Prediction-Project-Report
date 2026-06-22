
# Car Price Prediction Project

A machine learning project to predict car prices using data preprocessing, feature engineering, and regression modeling (Ridge & Random Forest).

---

## Dataset Overview

- **Source**: `CarPrice_Assignment.csv`
- **Initial Rows**: 205 → **After Cleaning**: 190
- **Target Variable**: `price`

---

##  Phase 1: Data Understanding & Cleaning

###  Exploratory Data Analysis (EDA)
- Checked null values, data types, and summary statistics.
- Target variable `price` is right-skewed → Applied `np.log(price)`
- Strong predictors: `curbweight`, `enginesize`, `horsepower`

###  Data Cleaning
- Missing values: Filled using **mode** (categorical) and **median** (numerical)
- Removed duplicates and outliers using the **IQR method**

---

##  Phase 2: Feature Engineering & Multicollinearity

###  Engineered Features
- `size_index` = average of `wheelbase`, `carlength`, `carwidth`
- `power_to_weight` = `horsepower` / `curbweight`

###  Transformations
- Log-transform applied to: `enginesize`, `horsepower`, and `price`

###  Multicollinearity Handling
- Used **VIF (Variance Inflation Factor)** to detect multicollinearity
- Dropped features with VIF > 7
- Chose **Ridge Regression** to handle remaining multicollinearity

---

##  Phase 3: Modeling

###  Ridge Regression
- **Train R²**: 0.825
- **Test R²**: 0.806
- Robust against multicollinearity

###  RidgeCV (with Alpha Tuning)
- **Best Alpha**: `0.01`
- **Train R²**: 0.830
- **Test R²**: 0.808

####  RidgeCV Model Summary
| Metric     | Value        |
|------------|--------------|
| Train R²   | 0.8299       |
| Test R²    | 0.8079       |
| MAE        | 2849.82      |
| RMSE       | 3894.05      |
| MAPE       | 1.87%        |

####  RidgeCV Coefficients
| Feature            | Coefficient     |
|--------------------|-----------------|
| power_to_weight    | 42973.22        |
| symboling          | 378.16          |
| compressionratio   | 291.66          |
| carheight          | 197.84          |
| size_index         | 157.80          |
| enginesize         | 132.67          |
| peakrpm            | 2.82            |
| highwaympg         | -197.92         |

---

###  Random Forest Regressor
- **Train R²**: 0.984  
- **Test R²**: 0.953  
- **MAE**: 1403  
- **RMSE**: 1929  
- **MAPE**: 1.19%  
- Outperformed Ridge by capturing non-linear patterns

---

##  Model Evaluation

- Residuals show slight heteroscedasticity, but are mostly normal
- Q–Q plot confirms residual normality
- **Random Forest** performs best in prediction accuracy

---

##  Final Model Recommendation

>  **Recommended Model: Random Forest Regressor**  
> Use this model for production or deployment due to superior performance and ability to model complex interactions.

---

##  Notes & Future Work

- Encode categorical variables (`fueltype`, `carbody`, `drivewheel`)
- Add interaction terms (e.g., `aspiration × enginetype`)
- Try advanced models like **Gradient Boosting** or **XGBoost**

---

###  Goal Achieved

Built a **robust**, **interpretable**, and **high-performing** model for car price prediction.
