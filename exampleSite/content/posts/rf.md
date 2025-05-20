---
title: "Random Forest Algorithm"
description: Sticking to basics is always mandatory.
date: 2025-05-10
lastmod: 2025-05-10
keywords: ["randomforest", "algorithm", "ml"]
tags: ["algorithm", "ml"]
summary: We'll learn about random forest classification. Simple, straight & forward.
toc: true
math: true
---

# Random Forest Algorithm: Comprehensive Notes

## Introduction
Random Forest is an ensemble learning method that builds upon the foundation of decision trees. Unlike a single decision tree, Random Forest creates multiple trees and combines their predictions to improve accuracy and reduce overfitting.

## Core Concepts

### Ensemble Learning
- Random Forest is a **bagging (Bootstrap Aggregating)** ensemble technique
- Creates multiple decision trees and combines their outputs
- Final prediction is determined by majority vote (classification) or averaging (regression)

### Key Differences from Decision Trees
- Uses multiple trees instead of a single tree
- Introduces randomness in feature selection
- More robust to noise and outliers
- Less prone to overfitting
- Higher computational cost

## Algorithm Details

### Training Process
1. **Bootstrap Sampling**: Create $n$ different datasets by sampling with replacement from original data
2. **Random Feature Selection**: For each node split, consider only a random subset of features
   - Classification: Typically $\sqrt{p}$ features (where $p$ is total number of features)
   - Regression: Typically $p/3$ features
3. **Tree Building**: Grow each tree to maximum depth without pruning
4. **Aggregation**: Combine predictions from all trees

### Mathematical Representation

For a dataset with $n$ samples and $p$ features:

**Random Forest Prediction (Classification)**:
$$\hat{C}_{RF}(x) = \text{majority vote}\{\hat{C}_k(x): k = 1,...,B\}$$

Where:
- $\hat{C}_{RF}(x)$ is the predicted class from Random Forest
- $\hat{C}_k(x)$ is the prediction from the $k$-th tree
- $B$ is the number of trees

**Random Forest Prediction (Regression)**:
$$\hat{f}_{RF}(x) = \frac{1}{B}\sum_{k=1}^{B}\hat{f}_k(x)$$

Where:
- $\hat{f}_{RF}(x)$ is the predicted value from Random Forest
- $\hat{f}_k(x)$ is the prediction from the $k$-th tree
- $B$ is the number of trees

## Feature Importance

Random Forest provides a natural way to estimate feature importance:

$$\text{Importance}(X_j) = \frac{1}{B}\sum_{k=1}^{B}\sum_{t \in T_k}\Delta I(j,t)$$

Where:
- $\Delta I(j,t)$ is the decrease in impurity after splitting on feature $j$ at node $t$
- $T_k$ represents all nodes in tree $k$
- $B$ is the number of trees

## Out-of-Bag (OOB) Error Estimation

Each tree uses approximately 63.2% of samples (due to bootstrap sampling), leaving 36.8% as "out-of-bag" samples:

$$\text{OOB Error} = \frac{1}{n}\sum_{i=1}^{n}I(\hat{y}_i^{OOB} \neq y_i)$$

Where:
- $\hat{y}_i^{OOB}$ is the prediction for sample $i$ using only trees where $i$ was out-of-bag
- $I$ is the indicator function
- $n$ is the number of samples

## Hyperparameters

- **n_estimators**: Number of trees in the forest
- **max_features**: Number of features to consider at each split
- **max_depth**: Maximum depth of each tree
- **min_samples_split**: Minimum samples required to split a node
- **min_samples_leaf**: Minimum samples required at a leaf node
- **bootstrap**: Whether to use bootstrap sampling

## Advantages and Limitations

### Advantages
- Reduced overfitting compared to decision trees
- Handles high-dimensional data well
- Provides feature importance measures
- Maintains accuracy when significant portion of data is missing
- Parallelizable training process

### Limitations
- Less interpretable than a single decision tree
- More computationally expensive
- May overfit on noisy datasets if trees are too deep
- Not optimal for highly imbalanced datasets without adjustments

## Performance Metrics and Evaluation

- **Classification**: Accuracy, Precision, Recall, F1-Score, ROC-AUC
- **Regression**: MSE, RMSE, MAE, R²
- **Cross-validation**: k-fold CV to assess generalization performance

## Implementation Considerations

- Balance between number of trees and computational resources
- Feature engineering still important despite inherent feature selection
- Hyperparameter tuning crucial for optimal performance
- Consider memory limitations for large datasets
