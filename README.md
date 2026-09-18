# cricket-score-forecasting
Forecasting final T20 innings scores using Exponential Smoothing, Multiple Linear Regression, and XGBoost with in-innings match features.
# 🏏 T20 Innings Score Forecasting

A machine learning project for **forecasting the final score of a T20 cricket innings** using information available at an intermediate point in the innings.

The project compares a traditional time-series forecasting approach with regression and gradient-boosting models to understand how well the final innings score can be estimated from the current match situation.

## Project Overview

In T20 cricket, the eventual innings score depends on several factors such as the number of overs already played, wickets lost, current scoring rate, opponent strength, pitch conditions, weather, and home/away advantage.

This project uses these in-innings features to forecast the **final innings score** and compares the performance of three approaches:

* **Simple Exponential Smoothing (SES)**
* **Multiple Linear Regression (MLR)**
* **XGBoost Regressor**

The models are evaluated using multiple regression forecasting metrics.

---

## Objective

Given the state of a T20 innings at a particular point, estimate:

> **What will be the final score of the innings?**

The project focuses on understanding:

1. How strongly different match variables are associated with the final score.
2. Whether simple statistical forecasting can provide a reasonable baseline.
3. How linear regression performs on engineered cricket features.
4. Whether XGBoost can capture more complex relationships between match conditions and final score.
5. Which features contribute most to the XGBoost predictions.

---

## Dataset

The dataset contains **1,500 observations** and the following variables:

| Feature             | Description                                       |
| ------------------- | ------------------------------------------------- |
| `Match ID`          | Identifier for the match/innings                  |
| `Overs Played`      | Number of overs completed at the prediction point |
| `Wickets Lost`      | Wickets lost at the prediction point              |
| `Run Rate`          | Current scoring rate                              |
| `Home/Away`         | Whether the team is playing at home or away       |
| `Opponent Strength` | Numerical representation of opponent strength     |
| `Pitch Condition`   | Bowling, Balanced, or Batting                     |
| `Weather`           | Weather condition during the match                |
| `Predicted Score`   | Dataset target representing the final score       |

In the notebook, `Predicted Score` is renamed to **`Final Score`** for clarity.

---

## Exploratory Data Analysis

The notebook performs several exploratory analyses:

### Final Score Distribution

The distribution of final innings scores is examined to understand the range and concentration of scores.

### Overs Played vs Final Score

The relationship between the number of overs played and eventual final score is visualized, with wickets lost used as an additional dimension.

### Correlation Analysis

A correlation matrix is used to examine relationships between numerical variables including:

* Overs Played
* Wickets Lost
* Run Rate
* Opponent Strength
* Final Score

---

## Feature Engineering

### Overs Remaining

```text
Overs Remaining = 20 - Overs Played
```

### Wickets in Hand

```text
Wickets in Hand = 10 - Wickets Lost
```

### Current Runs Estimate

The current scoring rate is combined with overs played:

```text
Current Runs Est = Run Rate × Overs Played
```

### Home Indicator

The categorical `Home/Away` variable is converted into a binary feature:

```text
Home → 1
Away → 0
```

### Pitch Score

Pitch conditions are encoded as:

```text
Bowling  → -1
Balanced →  0
Batting  →  1
```

### Weather Encoding

Weather categories are converted into dummy variables using one-hot encoding.

---

## Train Test Split

The data is first sorted by `Match ID`.

An **80/20 chronological split** is then used:

```text
80% → Training Set
20% → Test Set
```

A chronological split is used rather than randomly shuffling the observations, keeping the evaluation closer to a forecasting setting.

---

# Models

## 1. Simple Exponential Smoothing

Simple Exponential Smoothing is used as a statistical baseline.

The model assigns greater importance to recent observations through an optimized smoothing parameter `α`.

The forecast is then updated sequentially as actual test observations become available.

---

## 2. Multiple Linear Regression

Multiple Linear Regression models the final score as a linear combination of the engineered features.

Conceptually:

```text
Final Score =
β₀
+ β₁(Overs Played)
+ β₂(Overs Remaining)
+ β₃(Wickets Lost)
+ ...
+ ε
```

The fitted coefficients are also examined to understand the direction and relative contribution of individual features within the linear model.

---

## 3. XGBoost Regressor

An **XGBoost regression model** is used to capture nonlinear relationships and interactions between match variables.

The model configuration used in the notebook includes:

```text
n_estimators = 300
max_depth = 4
learning_rate = 0.05
subsample = 0.9
colsample_bytree = 0.9
```

XGBoost feature importance is also analyzed to identify which engineered variables contribute most strongly to the model's predictions.

---

# Visualizations

The notebook includes:

* Final score distribution
* Overs played vs final score
* Correlation matrix
* Actual vs forecasted scores
* Model error comparison
* XGBoost feature importance
* XGBoost predicted vs actual scatter plot

---

# Tech Stack

* **Python**
* **NumPy**
* **Pandas**
* **Matplotlib**
* **Scikit-learn**
* **Statsmodels**
* **XGBoost**
* **Jupyter Notebook**

---

# Repository Structure

```text
t20-innings-score-forecasting/
│
├── t20-cricket-forecast.ipynb
├── t20_cricket_match_score_prediction.csv
└── README.md
```

---

# Key Takeaways

The project provides a comparison between:

| Approach                     | Type                        |
| ---------------------------- | --------------------------- |
| Simple Exponential Smoothing | Statistical baseline        |
| Multiple Linear Regression   | Linear ML model             |
| XGBoost                      | Nonlinear ensemble ML model |

The comparison demonstrates how increasingly flexible models can be applied to the problem of forecasting a T20 innings score from match state information.

---

# Possible Future Improvements

The current project can be extended in several ways:

* Use **ball by ball cricket data** instead of aggregated observations.
* Incorporate **batsman and bowler statistics**.
* Add current batting pair information.
* Include recent over scoring trends.
* Include venue specific historical scoring patterns.
* Add innings phase information such as Powerplay, Middle Overs, and Death Overs.
* Tune XGBoost hyperparameters using cross validation.
* Compare additional models such as Random Forest, LightGBM, CatBoost, and Random Forest.
* Build an interactive dashboard for real time score forecasting.
* Develop a model that updates predictions **ball by ball during a live innings**.

---


**SHAMITHA**

IIT Kharagpur

---

##  Project Focus

**Machine Learning · Regression · Time Series Forecasting · Feature Engineering · XGBoost · Cricket Analytics**
