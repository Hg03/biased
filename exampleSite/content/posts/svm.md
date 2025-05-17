

# Support Vector Machines (SVM)

## Introduction
Support Vector Machines (SVMs) are powerful supervised learning models used for classification, regression, and outlier detection. SVMs are particularly effective in high-dimensional spaces and cases where the number of dimensions exceeds the number of samples.

## Core Concept
The fundamental idea behind SVM is to find the optimal hyperplane that maximizes the margin between different classes. The margin is the distance between the hyperplane and the nearest data points from each class, called support vectors.

## Linear SVM Classification
### The Decision Boundary
For a binary classification problem:
```
f(x) = w·x + b
```
Where:
- w is the weight vector
- x is the feature vector
- b is the bias term

The decision rule:
- If f(x) ≥ 0, classify as positive class
- If f(x) < 0, classify as negative class

### Optimization Problem
SVM seeks to maximize the margin by minimizing:
```
(1/2)||w||² subject to y_i(w·x_i + b) ≥ 1 for all i
```
Where:
- y_i is either 1 or -1 (class label)
- x_i is the feature vector for the ith sample

## The Kernel Trick
For non-linearly separable data, SVMs use the "kernel trick" to transform the original feature space into a higher-dimensional space where a linear separator may exist.

Common kernels include:
1. **Linear**: K(x,y) = x·y
2. **Polynomial**: K(x,y) = (x·y + c)^d
3. **Radial Basis Function (RBF)**: K(x,y) = exp(-γ||x-y||²)
4. **Sigmoid**: K(x,y) = tanh(α(x·y) + c)

## Soft Margin SVM
In practice, perfect separation may not be possible or desirable (risk of overfitting). Soft margin SVMs allow some misclassifications by introducing slack variables:
```
minimize (1/2)||w||² + C∑ξ_i
subject to y_i(w·x_i + b) ≥ 1 - ξ_i and ξ_i ≥ 0
```

Where:
- C is the regularization parameter (controls the trade-off between margin size and classification error)
- ξ_i are slack variables allowing for misclassification

## Training with Gradient Descent
While traditional SVMs are trained using quadratic programming, they can also be trained using gradient descent variants:

### Hinge Loss Function
```
L(y, f(x)) = max(0, 1 - y·f(x))
```

### Overall Cost Function
```
J(w) = (λ/2)||w||² + (1/n)∑max(0, 1 - y_i(w·x_i + b))
```

### Gradient Update
```
If y_i(w·x_i + b) < 1:
    w = w - α(λw - y_i·x_i)
    b = b - α(y_i)
Else:
    w = w - α(λw)
```

## Multi-class SVM
Two common approaches:
1. **One-vs-Rest (OvR)**: Train n different binary classifiers
2. **One-vs-One (OvO)**: Train n(n-1)/2 binary classifiers

## Key Features of SVMs
- Maximum margin classifier
- Effective in high-dimensional spaces
- Memory efficient (only support vectors matter)
- Versatile (different kernel functions)
- Robust against overfitting in high-dimensional spaces

## Comparing SVMs to Logistic Regression and Linear Regression

### SVM vs. Logistic Regression
1. **Objective**:
   - SVM: Maximizes margin between classes
   - Logistic Regression: Maximizes probability estimates

2. **Decision Boundary**:
   - SVM: Only support vectors influence the boundary
   - Logistic Regression: All data points influence the boundary

3. **Output**:
   - SVM: Hard class assignments
   - Logistic Regression: Probability estimates

4. **Handling Non-linearity**:
   - SVM: Kernel trick
   - Logistic Regression: Requires explicit feature engineering

5. **Robustness**:
   - SVM: More robust to outliers
   - Logistic Regression: More sensitive to outliers

### SVM vs. Linear Regression
1. **Purpose**:
   - SVM: Classification (or regression with SVR)
   - Linear Regression: Regression

2. **Loss Function**:
   - SVM: Hinge loss
   - Linear Regression: Squared error loss

3. **Output Range**:
   - SVM: Discrete classes or real numbers (SVR)
   - Linear Regression: Unbounded real numbers

4. **Sensitivity to Outliers**:
   - SVM: More robust
   - Linear Regression: Very sensitive

Would you like me to delve deeper into any particular aspect of SVMs?
