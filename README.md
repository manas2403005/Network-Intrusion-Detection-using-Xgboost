# Network Intrusion Detection using XGBoost

This repository contains the solution developed for a competitive machine learning challenge focused on detecting and classifying malicious network behavior using a rich feature-based dataset.

## Overview

The objective of this project is to build a multi-class classification model capable of identifying various types of network intrusions based on session-level features. The problem required careful attention to data preprocessing, class imbalance, and model interpretability to ensure robust performance, especially for rare and harmful attack classes.


## Problem Statement

The dataset consists of session-level network traffic data, including statistics like packet counts, byte volumes, protocol types, and timing features. A major challenge in this task was the extreme class imbalance — most sessions belonged to benign classes like `Normal` and `Generic`, while the harmful attack classes such as `Worms`, `Shellcode`, and `Backdoor` were significantly underrepresented.

## Approach

### Data Preprocessing

- Missing values were handled using KNN Imputer (multivariate approach).
- Label encoding was applied to categorical features using consistent mappings across train and test sets.
- Target labels were encoded numerically for compatibility with multi-class classification.
- All preprocessing steps were encapsulated into a pipeline for consistent transformations.

### Class Imbalance Handling

- Class weights were computed inversely proportional to class frequencies and passed to the model.
- SMOTE oversampling was applied to enhance representation of minority attack classes.

### Model

- Used XGBoost with objective set to `multi:softprob` for multi-class probability outputs.
- Key hyperparameters tuned:
  - `max_depth`, `learning_rate`, `n_estimators`
  - `subsample`, `colsample_bytree`
  - `scale_pos_weight`, `reg_lambda`, `reg_alpha`
- Early stopping used on stratified validation sets to prevent overfitting.

### Evaluation Metrics

- Weighted F1 Score (primary evaluation metric)
- Multiclass Log Loss (mlogloss)
- Multiclass ROC AUC
- Per-class precision, recall, and F1-score
- Confusion matrix analysis

### Error Analysis

- SHAP values used to interpret model behavior and identify feature importance per class.
- Confusion observed between specific classes such as DoS and Exploits due to overlapping feature patterns.
- Binary XGBoost model trained separately to better distinguish between these confusing class pairs.

## Results

- Achieved significant improvement in recall and precision for minority attack classes.
- Reduced false negatives for critical classes like DoS, Exploits, Shellcode, and Worms.
- Final model demonstrated balanced performance as measured by weighted F1 score.

## Future Improvements

- Apply dimensionality reduction (e.g., PCA) to improve class separability.
- Explore alternate encoding strategies for categorical variables (e.g., one-hot encoding).
- Experiment with stacked ensembles combining XGBoost, LightGBM, and CatBoost with meta-model voting.

## Repository Structure

- `notebook/` – Jupyter notebook with complete preprocessing, modeling, and evaluation.
- `report/` – PDF summary of the approach and results.
- `data/` – Placeholder for dataset (not included).
- `README.md` – Project overview and documentation.

## License

This project is shared for educational purposes and is not licensed for commercial use. Dataset was provided as part of a competition and is subject to its original terms of use.
