# <font size=5> **Fast Fraud Screening** </font> <br> <font size=3> _Using Lightweight Models to Flag Risk Before Deep Analysis_ </font>

Team members: [Abdullah Ahmed](https://github.com/abdullah5523p), [Noimot Bakare Ayoub](https://github.com/unomics20), [Cyril Cordor](https://github.com/cyril-cordor), [Brandon Owens](https://github.com/Brandon-Owens)

**Disclosure:** Documents, code, etc. displayed in this repository includes or references data provided by J.P. Morgan Chase & Co.


# Contents

1. [Introduction](#Introduction)
2. [Dataset](#Dataset)
3. [Methods, Models, Engineered Features
](#Methods, Models, Engineered Features)
4. [Performance Metrics and KPIs](#Performance Metrics and KPIs)
5. [Results](#Results)
6. [Challenges and Future Work](#Challenges and Future Work)


## Introduction
Financial fraud is a growing challenge. This project proposes a two-stage fraud detection framework: a lightweight "surrogate model" screens transactions, prioritizing high recall, then flagged transactions go to intensive models/human analysts for verification. This reduces computational load, speeds detection, and focuses resources. Using J.P. Morgan & Co's synthetic data, our XGBoost model achieved 7x Lift and 70% recall, flagging 1 in 4 fraud cases while incorrectly flagging less than 1% of legitimate transactions. We propose a "Lift" metric (recall and predicted positive rates) for efficiency, finding traditional metrics misleading.

## Dataset

We utilize the [J.P. Morgan Chase & Co. Payment Data for Fraud Protection](https://www.jpmorganchase.com/about/technology/research/ai/synthetic-data), a synthetic dataset for privacy. This subject-centric data contains over 1.49 million transactions (electronic transfers, bill payments, deposits, withdrawals) spanning approximately 50 years. Each entry details the transaction amount in U.S. dollars, involved accounts (sender, beneficiary, or both), and other identifying features.

## Methods, Models, Features Engineered

### Methods

We engineer both transaction and graph-derived features to train a lightweight, high-recall fraud screening model.

To analyze the complex network of over 300,000 customer and merchant accounts, we used Python’s NetworkX package to construct a multi-directed graph. A multi-directed graph is a network structure composed of nodes, representing sender or beneficiary accounts, and the edges represent transactions. Edge direction shows fund flow – who is sending versus who is receiving the funds – and multiple edges indicate repeated transfers. Fraud often occurs in clusters of accounts cycling funds among themselves, making the graph view effective for uncovering hidden connections and identifying potential fraud rings (Figure #).

### Features Engineered

_Models and Tools Used:_ Logistic Regression, XGBoost, Linear Discrimination Analysis, PCA



## Performance Metrics and KPIs


### Key Performance Metric



### Model Performance KPI

Our Key Performance Indicators include the percentage of fraud transactions correctly flagged (Recall),  and a measure of how much better the model is at identifying fraud compared to random guessing (Lift).
Figure 4 shows the trade-off between recall and lift for our XGBoost model across different thresholds. The optimal threshold is 0.5, where the model achieves 70% recall, balancing detection coverage and precision. 

### Business KPI

We use synthetic data to create realistic fraud risk KPIs, evaluating the model on false positives, analyst workload savings, simulated loss-avoidance scores, total loss avoided (USD), and total review cost. Key takeaways:

- Our lightweight model offers high speed and low computational overhead, suitable for real-time deployment.
- Initially, the model showed a low false positive rate (~1%).
- However, it currently has a high fraud miss rate (~66%), requiring threshold tuning for recall-first performance.
- With adjustments, we anticipate achieving high recall, aligning with bank fraud pre-screening strategies.


## Results

Initial results show strong computational performance and low false positive rate, demonstrating feasibility for real time screening. At the current decision threshold fraud detection remains limited, resulting in a high miss rate. Future iterations will adjust model tuning, and thresholding to increase recall, the primary objective of the model, while maintaining manageable volume alert. This stage validates the model architecture and provides a foundation for a high-recall optimization in subsequent experiments.

## Challenges and Future Work

Developing a fraud detection model using the J.P. Morgan dataset presents three main challenges:

1. **Feature Engineering:** New features must be generated from raw transaction data to uncover fraudulent patterns.

2. **Imbalanced Data:** Fraudulent transactions (2.06% of 1.49 million+) are significantly outnumbered by non-fraudulent ones, making it difficult for a model to learn.

3. **Synthetic Data Artifact:** Transaction timestamps in this synthetic dataset may follow a pattern, potentially lacking predictive information about fraud, as fraudulent labels were assigned using predefined probabilities.
