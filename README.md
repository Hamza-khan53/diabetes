Diabetes Risk Predictor: An End-to-End Machine Learning System with a Flask Web App

A full end-to-end machine learning and Flask web application that predicts diabetes risk and explains each prediction, for individual patients or whole CSV files. Built with Python, scikit-learn, pandas, SHAP, and Flask, this project covers the whole path from raw data to an interactive tool: ingestion, training, evaluation, explainability and a redesigned dashboard.

⚙️ Two integrated components:

End-to-End Machine Learning Pipeline — data processing → training → evaluation → explainability.
Interactive Flask Dashboard — real-time single & batch prediction app powered by the trained model.

Educational project. Not a medical device and not medical advice

Highlights
Automated ML Pipeline: Modular scripts for loading, preprocessing, EDA, training, evaluation, and model explainability.
Redesigned Web Dashboard: Flask + Chart.js with a risk gauge, low / moderate / high bands, inline validation, dark mode and keyboard-friendly tabs.
Explainability: SHAP and permutation-importance charts for the model overall, plus a "what moved the estimate" breakdown for every single prediction.
Batch screening: Upload a CSV, see the risk distribution and the highest-risk patients, and download every prediction.
Resilient by design: If a saved model can't be loaded (for example, a scikit-learn version mismatch), the app falls back to another model instead of crashing.
Tested: pytest suite, GitHub Actions CI and pre-commit hooks.

Results

Measured on the Pima Indians Diabetes dataset (768 patients) with the gradient boosting model the dashboard loads:

Metric	Score
ROC AUC (held-out test data)       	0.81
ROC AUC (5-fold cross-validation)	  0.83 ± 0.03
F1 score	                           0.61

## Project Architecture

```text
Diabetes-Risk-Prediction-Project/
├── data/                          # raw dataset (diabetes.csv)
├── models/                        # saved ML model (.joblib)
├── reports/                       # generated plots, explainability & metrics
│   ├── explain/                   # SHAP/LIME visual outputs
│   └── models/                    # trained model artifacts
├── docs/screenshots/              # images used in this README
├── src/
│   ├── data_loading.py
│   ├── data_processing.py
│   ├── data_exploration.py
│   ├── data_visualisation.py
│   ├── statistical_analysis.py
│   ├── model_training.py
│   ├── model_evaluation.py
│   ├── model_explainability_interpretability.py
│   ├── dashboard/                 # Flask dashboard app
│   │   ├── app.py                 # routes
│   │   └── predict.py             # model loading, predictions, local explanations
│   ├── templates/
│   │   └── index.html
│   └── static/                    # css, js, sample CSV
├── tests/                         # unit, integration, and dashboard tests
├── main.py                        # unified pipeline runner
├── requirements.txt
└── README.md
```

## Local Run

```bash
# 1. Get the code
git clone https://github.com/Hamza-khan53/diabetes.git
cd diabetes

# 2. Create and activate a virtual environment
python -m venv venv
venv\Scripts\activate            # macOS/Linux: source venv/bin/activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Run the Flask app
python -m src.dashboard.app
```

Then open http://127.0.0.1:5000 in your browser.

To use a specific model file, set `DASHBOARD_MODEL` first:

```bash
# Windows
set DASHBOARD_MODEL=reports/models/rf_best.joblib

# macOS/Linux
export DASHBOARD_MODEL=reports/models/rf_best.joblib

python -m src.dashboard.app
```
