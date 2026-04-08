# 🏀 March Madness Prediction using XGBoost

## 📌 Overview
This project predicts the winning probability of NCAA March Madness games for both **Men’s and Women’s tournaments** using machine learning.

The model is built using **XGBoost** and leverages multiple engineered features such as:
- Elo ratings  
- Box score statistics  
- Massey Ordinal rankings  
- Weighted historical team performance  

The final output is the **probability of Team A winning against Team B**.

---

## ⚙️ Features Used

### 1. Elo Rating
- Measures team strength based on past performance  
- Dynamically updated after each match  
- Helps capture team skill evolution  

---

### 2. Box Score Statistics
- Derived from match-level data:
  - Points scored  
  - Shooting efficiency  
  - Rebounds, assists, etc.  
- Aggregated to team-level metrics  

---

### 3. Massey Ordinal Rankings
- External ranking system  
- Provides global ranking of teams  
- Helps incorporate expert-based evaluation  

---

### 4. Weighted Historical Performance (Custom Feature ⭐)

This feature captures **team consistency and strength over the last 3 seasons**, giving more importance to recent performance.

#### Method:
- Use data from:
  - (season - 1)
  - (season - 2)
  - (season - 3)

- For each team, compute:
  - **Win Percentage (`WinPct`)**
  - **Average Point Differential (`AvgPtDiff`)**

#### Weighting Scheme:
- Recent seasons are more important:
  - (t-1) → weight = 3  
  - (t-2) → weight = 2  
  - (t-3) → weight = 1  

#### Final Output Features:
- `WinPct` → weighted win rate  
- `AvgPtDiff` → weighted scoring dominance  

#### Benefit:
- Captures **long-term team quality**
- Reduces noise from older seasons  
- Improves model generalization  

---

### 5. Derived Features
- Elo difference (`EloDiff`)  
- Seed difference (`SeedDiff`)  
- Interaction features (e.g., `elo_seed`)  

---

## 🤖 Model

We use **XGBoost Classifier** because:
- Works well with tabular data  
- Captures non-linear relationships  
- Handles feature interactions automatically  

### Objective
Predict:

P(Team A wins)

---

## 📊 Evaluation Metric

The model is evaluated using **Brier Score**:

Brier Score = (1/N) * Σ (y_true - y_pred)²

- Lower score is better  
- Measures accuracy of predicted probabilities  

---

## 🧪 Training Pipeline

1. Load historical match data  
2. Generate features:
   - Elo ratings  
   - Box statistics  
   - Massey rankings  
   - Weighted historical performance  
3. Merge all features into training dataset  
4. Train XGBoost model  
5. Validate using Brier Score  

---

## 📁 Project Structure
