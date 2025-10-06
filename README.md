# 🏠 Claims Damage Ratio Prediction

A comprehensive analysis of flood damage prediction using machine learning approaches, with a focus on the limitations of deterministic ML methods for probabilistic phenomena.

## 🚀 Quick Start

### Prerequisites
```bash
# Clone the repository
git clone <repository-url>
cd claims-prediction

# Create conda environment
conda env create -f enviroment.yml
conda activate claims

# Install dependencies
pip install -r requirements.txt
```

### Running the Analysis
```bash
# Run LightGBM analysis
jupyter notebook claims-lightgbm.ipynb

# Run CatBoost analysis  
jupyter notebook claims-cat-boost.ipynb

# Explore data cleaning and exploration
jupyter notebook data-cleaning.ipynb
jupyter notebook data-exploration.ipynb
```

## 📊 Project Overview

### 🎯 Motivation & Scope

This project investigates the effectiveness of machine learning approaches for predicting flood damage ratios in insurance claims. The analysis reveals fundamental limitations of deterministic ML methods when applied to inherently probabilistic phenomena like flood damage.

**Key Questions:**
- Can sophisticated two-stage modeling frameworks improve upon single-stage approaches?
- Are traditional ML evaluation metrics appropriate for probabilistic phenomena?
- What are the fundamental limits of predictability for flood damage?

### 📈 Dataset Information

#### Raw Data Source
- **FEMA NFIP Claims Dataset**: [https://www.fema.gov/openfema-data-page/fima-nfip-redacted-claims-v2](https://www.fema.gov/openfema-data-page/fima-nfip-redacted-claims-v2)
- **FEMA Zone Mapping**: Harris County flood zone data for geospatial analysis

#### Data Processing Pipeline

**📁 Raw Data (`FimaNfipClaims.parquet`)**
- Original FEMA claims dataset with ~2.7M records
- Contains claim details, property information, and damage assessments
- Includes flood zone ratings, water depth measurements, and claim amounts

**🧹 Cleaned Data (`claims_cleaned.csv`)**
- Processed dataset with ~200K records after filtering and cleaning
- Removed incomplete records and outliers
- Engineered features for modeling (water depth, flood zones, property characteristics)
- Target variable: `damageRatio` (claim amount / building value)

**📋 Metadata (`fima-claims-metadata.csv`, `fema_zone_mapping.csv`)**
- Documentation of data fields

#### Data Cleaning & Exploration Notebooks

**🧽 `data-cleaning.ipynb`**
- Data preprocessing and feature engineering
- Handling missing values and categorical variables
- Creating derived features (damage ratios, flood zone mappings)
- Train/validation/test split preparation

**🔍 `data-exploration.ipynb`**
- Initial data analysis and visualization
- Distribution analysis of damage ratios
- Feature correlation analysis
- Outlier detection and data quality assessment

## 🤖 Model Analysis Notebooks

### 📊 `claims-lightgbm.ipynb` - Comprehensive ML Analysis

**Single-Stage LightGBM Modeling:**
- Hyperparameter optimization using Optuna (50 trials)
- Performance evaluation on test set (RMSE: 0.2065, R²: 0.3970)
- Error analysis revealing heteroscedasticity and regression-to-mean bias

**Two-Stage Modeling Framework:**
- **Stage 1**: Spline baseline model on water depth
- **Stage 2**: Residual modeling with LightGBM
- **Stage 3**: Variance modeling with inverse-variance weighting
- **Result**: No improvement over single-stage approach (0.34% worse RMSE)

**Key Findings:**
- R² = 0.40 indicates 60% of damage variation is inherently unpredictable
- Two-stage decomposition failed to improve performance
- Evidence that flood damage is fundamentally probabilistic, not deterministic

### 🐱 `claims-cat-boost.ipynb` - Probabilistic Modeling Approach

**CatBoost Implementation:**
- Probabilistic modeling with Gaussian NLL loss function
- Mean + variance prediction outputs
- Superior categorical feature handling
- Proper uncertainty quantification for risk management

**Evaluation Framework:**
- Gaussian Negative Log-Likelihood instead of RMSE

## 📁 Project Structure

```
claims-prediction/
├── 📊 data/
│   ├── claims_cleaned.csv          # Processed dataset
│   ├── fima-claims-metadata.csv    # Data documentation
│   └── fema_zone_mapping.csv       # Flood zone mappings
├── 📈 plots/                       # Generated visualizations
├── 🤖 models/                     # Trained model files
├── 📓 notebooks/
│   ├── claims-lightgbm.ipynb      # Main ML analysis
│   ├── claims-cat-boost.ipynb     # Probabilistic modeling
│   ├── data-cleaning.ipynb        # Data preprocessing
│   └── data-exploration.ipynb     # Exploratory analysis
├── 📋 requirements.txt            # Python dependencies
├── 🐍 enviroment.yml             # Conda environment
└── 📖 README.md                   # This file
```

## 🔬 Key Insights

### ❌ ML Limitations for Probabilistic Phenomena
- **High Natural Noise**: Physical damage involves quantum-level material interactions
- **Epistemic Uncertainty**: Limited knowledge of building materials and environmental conditions
- **Fundamental Limits**: 60% of damage variation is inherently unpredictable

### ✅ Recommended Solutions
- **Probabilistic Frameworks**: Bayesian models, quantile regression, stochastic processes
- **Proper Evaluation**: Gaussian NLL instead of RMSE for uncertainty-aware assessment
- **Risk Management**: Focus on prediction confidence rather than point estimates

## 🎯 Future Directions

- **CatBoost + Gaussian NLL**: Probabilistic modeling with superior categorical handling
- **Bayesian Hierarchical Models**: Explicit uncertainty quantification
- **Stochastic Process Models**: Physics-informed probabilistic modeling

## 📚 Dependencies

- **Core ML**: scikit-learn, lightgbm, catboost, optuna
- **Data Processing**: pandas, numpy
- **Visualization**: matplotlib, seaborn
- **Environment**: jupyter, ipywidgets

---

**💡 Bottom Line**: Flood damage prediction is a probabilistic problem requiring probabilistic solutions, not deterministic ML approaches.