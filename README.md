# Walmart Sales Forecast Model

This repository contains a Jupyter Notebook (`Walmart_SalesForecast_Model.ipynb`) that walks through a full pipeline for forecasting weekly sales for Walmart stores. The notebook includes data ingestion, EDA, preprocessing, feature engineering, model training (Linear Regression, Random Forest, XGBoost), evaluation, and simple prediction examples.

## What is included
- `Walmart_SalesForecast_Model.ipynb` — Main notebook with step-by-step analysis and modeling.
- `.gitignore` — Ignores typical Python and notebook artifacts.
- `walmart_sales_model.pkl` (optional) — Serialized best model if saved by the notebook.

## Summary of steps performed in the notebook
1. Environment setup and dependency imports.
2. (Optional) Kaggle dataset download and extraction.
3. Load CSV files: `train.csv`, `test.csv`, `stores.csv`, `features.csv`.
4. Exploratory Data Analysis (EDA): distributions, store & department sales, holiday impact, time series plots.
5. Data preprocessing and merging: merge `train` with `stores` and `features` on `Store`, `Date`, and `IsHoliday`.
6. Feature engineering: date parts (Year, Month, Day, DayOfWeek, Quarter), store Type one-hot encoding, optional Markdown columns.
7. Train/test split and model training for multiple estimators (Linear Regression, Random Forest, XGBoost).
8. Model evaluation and comparison (MAE, RMSE, R²), hyperparameter tuning for the best model via `GridSearchCV`.
9. Save best model and feature names to `walmart_sales_model.pkl`.
10. Example prediction helper function and sample predictions.

## Results
The notebook computes evaluation metrics (MAE, RMSE, R²) and creates a `results_df` DataFrame that compares the trained models. If you've already run the notebook in your environment, add the final values below or run the short snippet to save results to a CSV and paste them here.

Example results table (fill with your numbers):

Model | MAE | RMSE | R²
---|---:|---:|---:
Linear Regression | 14561.46 | 21753.62 | 0.0925
Random Forest | 1414.53 | 3697.53 | 0.9738
XGBoost | 3560.44 | 6267.41 | 0.9247

How to save or extract `results_df` from the notebook
1. In the notebook, after evaluation (where `results_df` is defined), add and run this cell to save results:

```python
# Save results to CSV to include in README or for later use
results_df.to_csv('results_summary.csv', index=False)
print('Saved results_summary.csv')
print(results_df)
```

2. Then open `results_summary.csv` and copy the values into the Results table above.

Programmatically print saved model info (if `walmart_sales_model.pkl` exists):

```python
import pickle
with open('walmart_sales_model.pkl', 'rb') as f:
   model_data = pickle.load(f)
   print('Model name:', model_data.get('model_name'))
   print('Feature count:', len(model_data.get('feature_names', [])))
   print('Feature names sample:', model_data.get('feature_names')[:10])
```

## Reproduce locally (quick)
1. Create and activate a virtual environment (recommended):

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

2. Install dependencies:

```powershell
pip install --upgrade pip
pip install pandas numpy scikit-learn xgboost lightgbm matplotlib seaborn plotly jupyter
```

3. (Optional) If you used Kaggle in the notebook, place your `kaggle.json` in the working directory or follow Kaggle-auth steps used in the notebook.

4. Open and run the notebook in VS Code or Jupyter:

```powershell
jupyter notebook "Walmart_SalesForecast_Model.ipynb"
```


## Saved artifacts
- `walmart_sales_model.pkl` — Pickled dict with keys: `model`, `feature_names`, `model_name` (if created by notebook).
- `results_summary.csv` — (recommended) Saved metrics from the notebook for README inclusion.
