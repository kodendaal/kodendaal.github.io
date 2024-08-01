---
title:  "Exploration of Various Supervised Learning Algorithms"
mathjax: true
layout: post
categories: 
  = github
  - website
---

In this project, I explored various supervised learning problems by evaluating three algorithms: **k-Nearest Neighbors (kNN), Support Vector Classifier (SVC), and Multi-Layer Perceptron (MLP)**. Using two distinct datasets, NASA and Wine, I aimed to assess each algorithm's performance and computational efficiency. The data was split into training and hold-out test sets with an 80/20 split, and a 5-fold cross-validation within the training set was used to optimize hyperparameters. Stratified sampling maintained class distribution, ensuring consistency.

For pipeline evaluation, data standardization was applied for uniform assessments. Hyperparameter tuning was conducted using a grid search with 5-fold cross-validation, and learning curves were analyzed to understand the bias-variance trade-off. Performance metrics such as accuracy, precision, recall, and F1-score were used to evaluate the models on the hold-out test dataset, with results compared visually through confusion matrices.

The MLP model demonstrated superior performance on the NASA dataset across all metrics: accuracy (0.99), precision (0.97), recall (0.98), and F1-score (0.98). Its ability to model complex non-linear relationships made it highly effective for this dataset. However, all models struggled with the Wine dataset due to class imbalance and dataset complexity, with no significant outperformance observed among the models, highlighting the need for advanced techniques to handle imbalance.

Each model had specific strengths and limitations. kNN performed well with local learning but was sensitive to high dimensionality, requiring careful tuning of the number of neighbors and distance metrics. SVC was effective in high-dimensional spaces and robust with appropriate regularization but was computationally expensive and less efficient for multi-class problems. MLP, while capable of capturing complex patterns, required extensive data and computational resources for training but showed fast prediction times due to parallelism.

Regarding time complexity, kNN had fast training times but slow prediction times. SVC was computationally expensive in both training and prediction. MLP required significant training time but offered fast predictions. 

Future research should integrate advanced techniques like boosting and ensemble methods. Further hyperparameter tuning and feature engineering are essential to improve model performance. Addressing dataset imbalance through oversampling and synthetic data generation could yield better results. These findings provide valuable insights into the strengths and limitations of each supervised learning algorithm, emphasizing the need for tailored approaches based on the specific characteristics of the datasets.


<embed src="https://kodendaal.github.io/assets/supervised_learning.pdf" type="application/pdf" width="100%" height="1050" />

