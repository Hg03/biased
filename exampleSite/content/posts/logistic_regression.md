---
title: "Logistic Regression"
description: Sticking to basics is always mandatory.
date: 2025-05-10
lastmod: 2025-05-10
keywords: ["logisticregression", "algorithm", "ml"]
tags: ["algorithm", "ml"]
summary: We'll learn about logistic regression. Simple, straight & forward.
toc: true
math: true
---

# Logistic Regression with Gradient Descent

## Introduction
Logistic regression is a classification algorithm used to predict binary outcomes. Despite its name, it's a classification model rather than a regression model. It estimates the probability that an instance belongs to a particular class.

## The Logistic Model
Unlike linear regression which outputs continuous values, logistic regression uses the sigmoid function to transform linear predictions into probabilities between 0 and 1:
```
p(y=1|x) = σ(z) = 1/(1 + e^(-z))
```
Where:
- z = b + w₁x₁ + w₂x₂ + ... + wₙxₙ (the linear component)
- σ is the sigmoid function
- p(y=1|x) is the probability that y=1 given input x

## Cost Function
For logistic regression, we use the Log Loss (Cross-Entropy Loss) function:
```
J(w) = -(1/n) * Σ[y * log(p) + (1-y) * log(1-p)]
```
Where:
- y is the actual class (0 or 1)
- p is the predicted probability of class 1
- n is the number of samples

## Gradient Descent for Logistic Regression
The gradient descent process is similar to linear regression but with different derivatives:

### The Update Rule
```
wⱼ = wⱼ - α * (1/n) * Σ[(p - y) * xⱼ]
b = b - α * (1/n) * Σ(p - y)
```
Where:
- p is the predicted probability
- y is the actual class
- α is the learning rate
- xⱼ is the jth feature

## Variants and Regularization
- **L1 Regularization (Lasso)**: Adds |w| to the cost function, promoting sparsity
- **L2 Regularization (Ridge)**: Adds w² to the cost function, preventing overfitting
- **Elastic Net**: Combines L1 and L2 regularization

## Decision Boundary
After training, classification is done by:
- If p ≥ 0.5, predict class 1
- If p < 0.5, predict class 0

This creates a decision boundary in the feature space.

## Evaluating the Model
- **Accuracy**: Overall correctness
- **Precision**: Accuracy of positive predictions
- **Recall**: Ability to find all positive instances
- **F1 Score**: Harmonic mean of precision and recall
- **ROC Curve and AUC**: Performance across different thresholds

## Key Differences from Linear Regression

1. **Output Type**:
   - Linear regression: Continuous values (ŷ ∈ ℝ)
   - Logistic regression: Probabilities (0 ≤ p ≤ 1)

2. **Use Case**:
   - Linear regression: Predicting quantities (e.g., house prices)
   - Logistic regression: Classification tasks (e.g., spam detection)

3. **Model Function**:
   - Linear regression: y = b + w₁x₁ + w₂x₂ + ... + wₙxₙ
   - Logistic regression: p = 1/(1 + e^(-(b + w₁x₁ + w₂x₂ + ... + wₙxₙ)))

4. **Cost Function**:
   - Linear regression: Mean Squared Error
   - Logistic regression: Log Loss (Cross-Entropy)

5. **Assumptions**:
   - Linear regression: Linear relationship between variables
   - Logistic regression: Linear relationship between log-odds and features

6. **Gradient Calculation**:
   Different formulas are used to compute gradients in each model

7. **Interpretation**:
   - Linear regression: Coefficients represent change in output per unit change in input
   - Logistic regression: Coefficients represent change in log-odds

8. **Optimization Challenge**:
   - Linear regression: Convex optimization problem with a guaranteed global minimum
   - Logistic regression: Non-linear due to sigmoid function, but still convex.
