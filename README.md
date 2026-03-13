# NoSQL Injection Detection with Machine Learning

This project demonstrates a lightweight machine learning pipeline for detecting potentially malicious MongoDB-style NoSQL queries. The notebook builds a synthetic dataset of **safe** and **malicious** query patterns, vectorizes the query text with **TF-IDF**, trains multiple classifiers, evaluates performance, measures inference latency, and provides an interactive widget-based demo for testing new queries.

## Project Overview

The goal of this notebook is to classify query strings as either:

- **safe**
- **malicious**

The workflow is designed as a practical proof of concept for identifying suspicious NoSQL injection patterns such as:

- `$where` abuse
- tautology-style conditions like `1==1`
- injected `$or` logic
- JavaScript execution attempts
- destructive or denial-of-service style payloads

## Features

- Builds a labeled dataset of MongoDB-style query strings
- Uses **TF-IDF** vectorization on raw query text
- Trains and compares three models:
  - Logistic Regression
  - Random Forest
  - Linear SVM
- Evaluates each model using:
  - classification report
  - confusion matrix
  - 5-fold cross-validation
- Measures approximate per-query prediction latency
- Includes helper functions for single-query inference
- Includes an **interactive Jupyter widget UI** for:
  - pasting a query
  - testing preset attack examples
  - viewing model predictions
  - inspecting top contributing terms
  - logging prediction history

## Notebook Contents

The notebook follows this sequence:

1. **Imports and configuration**
2. **Safe query pool definition**
3. **Malicious query pool definition**
4. **Dataset creation and shuffling**
5. **Train/test split and TF-IDF vectorization**
6. **Model training and evaluation**
7. **5-fold cross-validation**
8. **Prediction latency measurement**
9. **Single-query prediction helper**
10. **Interactive demo with ipywidgets**

## Tech Stack

- Python
- pandas
- scikit-learn
- ipywidgets
- Jupyter Notebook

## Installation

Clone the repository and install the required packages:

```bash
git clone <your-repo-url>
cd <your-repo-folder>
pip install pandas scikit-learn ipywidgets notebook
```

If you are running the notebook locally in Jupyter, you may also need:

```bash
jupyter nbextension enable --py widgetsnbextension
```

## How to Run

1. Open the notebook:

```bash
jupyter notebook NoSQLInjection-4.ipynb
```

2. Run all cells from top to bottom.
3. Review the model evaluation output.
4. Use the interactive widget at the end of the notebook to test custom MongoDB-style queries.

## Example Queries

### Safe

```javascript
db.users.find({ "username": "test_user" })
```

### Malicious

```javascript
db.users.find({ "$where": "this.isAdmin == true || 1==1" })
```

## Model Output

The notebook compares predictions from all three models and is structured to support a simple ensemble-style decision flow. It also includes interpretability support by showing top contributing terms from the Logistic Regression model.

## Use Cases

This project can be used as:

- a cybersecurity portfolio project
- a machine learning classification demo
- a proof of concept for secure query screening
- a starting point for research on NoSQL injection detection

## Limitations

This notebook is a proof of concept and has a few important limitations:

- The dataset is **synthetically generated**, not collected from production traffic
- The model is trained on **query text patterns**, not execution behavior
- It is focused on **MongoDB-style query syntax**
- Real-world attackers may use obfuscation or payload variations not represented in the sample pool
- A production-grade detector should include larger datasets, adversarial testing, and integration with application-layer security controls

## Future Improvements

Potential next steps for expanding this project:

- Train on real or semi-realistic traffic logs
- Add probability thresholds and alerting logic
- Expand feature engineering beyond TF-IDF
- Test deep learning or transformer-based sequence models
- Add REST API deployment with Flask or FastAPI
- Log predictions to a database for monitoring and analysis
- Integrate with SIEM or web application security workflows

## Repository Structure

```bash
.
├── NoSQLInjection-4.ipynb
└── README.md
```

## Author

**Marco Alvarado**  
Data Analyst  
[LinkedIn](https://linkedin.com/in/maaj1081775)

## License

This project is intended for educational and portfolio use.
