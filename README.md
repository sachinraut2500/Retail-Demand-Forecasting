# Retail Demand Forecasting
---
Predict product demand to improve inventory planning. This repo contains a small pipeline: feature engineering, model training (XGBoost), prediction, and evaluation.
-----------
## Included scripts
- `src/features.py` — load raw sales and create lag + calendar features
- `src/train.py` — train an XGBoost model and save artifact
- `src/predict.py` — load model and produce forecasts
- `src/evaluate.py` — compute RMSE and MAPE
--------
## Data format
Input CSV should have:
- `date` (YYYY-MM-DD)
- `store` (string or id)
- `item` (string or id)
- `sales` (numeric; daily sales)
---------------
---------------
## Quickstart
```bash
# 1. Setup environment
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
pip install -r requirements.txt

# 2. Preprocess
python src/features.py --input data/raw/sales.csv --out data/processed/sales.csv

# 3. Train
python src/train.py --processed data/processed/sales.csv --out models/xgb_model.joblib

# 4. Predict
python src/predict.py --model models/xgb_model.joblib --input data/processed/sales.csv --out data/preds.csv

# 5. Evaluate
python src/evaluate.py --actuals data/processed/sales.csv --preds data/preds.csv
