---
title:  "Supervised Learning Exploration"
mathjax: true
layout: post
categories: 
  = github
  - website
---

# Summary

The study explores various supervised learning problems by evaluating three algorithms: **k-Nearest Neighbors (kNN), Support Vector Classifier (SVC), and Multi-Layer Perceptron (MLP)**. The study is conducted using two distinct datasets: NASA and Wine, with the aim to assess each algorithm's performance and computational efficiency.

## Data Partitioning and Training Strategy:

* Data is split into training and hold-out test sets (80/20 split).
* A 5-fold cross-validation within the training set is used to optimize hyperparameters.
* Stratified sampling is employed to maintain class distribution.

## Pipeline Evaluation:

* Data standardization is applied for consistent evaluations.
* Hyperparameter tuning is conducted using a grid search with 5-fold cross-validation.
* Learning curves are analyzed to understand the bias-variance trade-off.

## Model Evaluation:

* Performance metrics include accuracy, precision, recall, and F1-score.
* kNN, SVC, and MLP models are evaluated on the hold-out test dataset.
* Results are compared visually through confusion matrices.

# High-Level Conclusions

### MLP Outperforms Others:

* The MLP model shows superior performance on the NASA dataset across all metrics: accuracy (0.99), precision (0.97), recall (0.98), and F1-score (0.98).
* Its ability to model complex non-linear relationships makes it highly effective for this dataset.

### Challenges with Wine Dataset:

* All models struggle with the Wine dataset due to class imbalance and dataset complexity.
* No significant outperformance is observed among the models, highlighting the need for advanced techniques to handle imbalance.


### Model-Specific Insights:

* kNN: Performs well with local learning but is sensitive to high dimensionality and requires careful tuning of the number of neighbors and distance metrics.
* SVC: Effective in high-dimensional spaces and robust with appropriate regularization but computationally expensive and less efficient for multi-class problems.
* MLP: Capable of capturing complex patterns but requires extensive data and computational resources for training. It shows fast prediction times due to parallelism.

### Time Complexity:

* kNN has fast training times but slow prediction times.
* SVC is computationally expensive in both training and prediction.
* MLP requires significant training time but offers fast predictions.


### Future Directions
* Future research should integrate advanced techniques like boosting and ensemble methods.
* Further hyperparameter tuning and feature engineering are essential to improve model performance.
* Addressing dataset imbalance through oversampling and synthetic data generation could yield better results.


These findings provide valuable insights into the strengths and limitations of each supervised learning algorithm, emphasizing the need for tailored approaches based on the specific characteristics of the datasets.


<embed src="https://kodendaal.github.io/assets/supervised_learning.pdf" type="application/pdf" width="750" height="1050" />
