# 🎓 Predictive Student Risk Analysis & Early Warning System
## 🎯 Problem Statement

Modern learning platforms generate rich behavioral data that, when analyzed correctly, can identify students at risk of failure or dropout **weeks before** formal assessments reveal the problem. This project builds an **Early Warning System** that:

- Classifies 2,000 student records with 93.5% accuracy (XGBoost)
- Uses 13 raw + 6 engineered behavioral and academic features
- Provides per-student intervention recommendations
- Enables educators to allocate support resources with data-backed prioritization



## 📊 Dataset

| Property | Value |
|---------|-------|
| Records | 2,000 student profiles |
| Raw Features | 13 (behavioral + academic) |
| Engineered Features | 6 (composite scores) |
| Target Classes | 3 (High / Medium / Low Risk) |
| Class Balance | ~33.5% / 33% / 33.5% |

**Raw Features:**
`student_id` · `attendance_percentage` · `assessment_score` · `assignment_completion_rate` · `login_frequency` · `study_hours` · `activity_count` · `communication_score` · `course_progress_percentage` · `forum_participation` · `video_completion_rate` · `peer_interaction_score` · `risk_category`

**Engineered Features:**
`engagement_score` · `performance_score` · `completion_score` · `study_efficiency` · `social_engagement` · `overall_risk_score`

---

## 🏗️ Architecture

```
Raw Data (dataset.csv)
        │
        ▼
┌─────────────────────┐
│  Data Preprocessing  │  Missing values · Duplicates · Outlier detection
└─────────┬───────────┘
          │
          ▼
┌─────────────────────┐
│  Feature Engineering │  6 composite features (engagement, performance, completion...)
└─────────┬───────────┘
          │
          ▼
┌─────────────────────┐
│  Scaling & Splitting │  StandardScaler · 80/20 stratified split
└─────────┬───────────┘
          │
    ┌─────┼──────┐
    ▼     ▼      ▼
   RF   XGB    SVM       ← 3 classifiers trained in parallel
    └─────┼──────┘
          │
          ▼
┌─────────────────────┐
│  Evaluation Suite    │  Accuracy · F1 · ROC-AUC · Confusion Matrix
└─────────┬───────────┘
          │
          ▼
┌─────────────────────┐
│  Intervention Engine │  Per-student risk-based recommendations
└─────────────────────┘
```

---

## 🔄 Workflow

1. **Load** → Import 2,000 student records from `dataset.csv`
2. **Clean** → Handle missing values, duplicates, and outliers
3. **Engineer** → Create 6 composite features from raw behavioral data
4. **Scale** → StandardScaler for SVM; tree models use raw features
5. **Split** → 80% train / 20% test, stratified by risk category
6. **Train** → Random Forest, XGBoost, SVM classifiers
7. **Evaluate** → Accuracy, Precision, Recall, F1, ROC-AUC, Confusion Matrix
8. **Visualize** → 9 professional charts saved to `visualizations/`
9. **Recommend** → Rule-based intervention engine per risk level

---

## 🤖 Models Used

| Model | Type | Key Hyperparameters |
|-------|------|---------------------|
| Random Forest | Ensemble (Bagging) | `n_estimators=200`, `max_depth=12`, `class_weight='balanced'` |
| XGBoost | Ensemble (Boosting) | `n_estimators=200`, `max_depth=6`, `learning_rate=0.05` |
| SVM | Kernel Method | `kernel='rbf'`, `C=10`, `gamma='scale'`, `class_weight='balanced'` |

---

## 📈 Results

| Model | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
|-------|---------|---------|------|---------|--------|
| **XGBoost** ⭐ | **93.50%** | **0.9349** | **0.9350** | **0.9349** | **0.9925** |
| SVM | 91.50% | 0.9154 | 0.9150 | 0.9152 | 0.9894 |
| Random Forest | 90.25% | 0.9052 | 0.9025 | 0.9033 | 0.9861 |

> 🏆 **XGBoost is the recommended model** for deployment — highest performance across all metrics.

---

## 🖼️ Visualizations

All charts are saved in the `visualizations/` directory:

| File | Description |
|------|-------------|
| `risk_distribution.png` | Bar chart and pie chart of risk category distribution |
| `correlation_heatmap.png` | Full feature correlation heatmap |
| `feature_importance.png` | Top 15 feature importances (Random Forest) |
| `roc_curve_comparison.png` | Macro-averaged ROC curves for all 3 models |
| `model_comparison_dashboard.png` | Side-by-side bar chart of all metrics per model |
| `risk_category_analysis.png` | Box plots of key features segmented by risk level |
| `rf_confusion_matrix.png` | Random Forest confusion matrix |
| `xgb_confusion_matrix.png` | XGBoost confusion matrix |
| `svm_confusion_matrix.png` | SVM confusion matrix |


## 🛠️ Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/Student-Risk-Analysis.git
cd Student-Risk-Analysis

# Create virtual environment
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

---

## ▶️ Run Instructions

```bash
# Option 1: Run Jupyter Notebook (recommended)
jupyter notebook risk_prediction.ipynb

# Option 2: Run as Python script
python generate_dataset.py   # Regenerate dataset
python run_ml.py             # Train models & generate visualizations

# Option 3: Execute notebook non-interactively
jupyter nbconvert --to notebook --execute risk_prediction.ipynb --output risk_prediction_executed.ipynb
```



## 📁 Repository Structure

```
Student-Risk-Analysis/
├── dataset.csv                          # 2,000 student records
├── risk_prediction.ipynb                # Complete ML notebook
├── README.md                            # This file     
├── visualizations/
│   ├── risk_distribution.png
│   ├── feature_importance.png
│   ├── correlation_heatmap.png
│   ├── roc_curve_comparison.png
│   ├── model_comparison_dashboard.png
│   ├── risk_category_analysis.png
│   ├── rf_confusion_matrix.png
│   ├── xgb_confusion_matrix.png
│   └── svm_confusion_matrix.png

