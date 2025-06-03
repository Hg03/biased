## Overview
Support Vector Machine (SVM) is a supervised learning algorithm used for both classification and regression. It finds the optimal hyperplane that separates classes with maximum margin.

### Key Concepts
- **Support Vectors**: Data points closest to the decision boundary
- **Hyperplane**: Decision boundary that separates classes
- **Margin**: Distance between hyperplane and nearest data points
- **Maximum Margin**: SVM objective to maximize this distance

## Linear SVM

### Optimal Hyperplane
- **Equation**: `wᵀx + b = 0`
- **Classification Rule**:
  - `y = +1` if `wᵀx + b ≥ 1`
  - `y = -1` if `wᵀx + b ≤ -1`

### Margin Calculation
- **Margin**: `M = 2/||w||`
- **Objective**: Maximize margin = Minimize `||w||²/2`

### Hard Margin SVM
**Optimization Problem:**
- **Minimize**: `(1/2)||w||²`
- **Subject to**: `yᵢ(wᵀxᵢ + b) ≥ 1` for all i

**Assumptions:**
- Data is linearly separable
- No misclassification allowed

### Soft Margin SVM
**Motivation:** Handle non-separable data with some misclassification

**Slack Variables:** `ξᵢ ≥ 0`
- `ξᵢ = 0`: Correct classification
- `0 < ξᵢ < 1`: Correct side but within margin
- `ξᵢ ≥ 1`: Misclassified

**Optimization Problem:**
- **Minimize**: `(1/2)||w||² + C∑ξᵢ`
- **Subject to**: 
  - `yᵢ(wᵀxᵢ + b) ≥ 1 - ξᵢ`
  - `ξᵢ ≥ 0`

**Hyperparameter C:**
- **Large C**: Less tolerance for misclassification (hard margin)
- **Small C**: More tolerance for misclassification (soft margin)

## Dual Formulation

### Lagrangian Dual Problem
**Primal → Dual transformation using Lagrange multipliers**

**Dual Optimization:**
- **Maximize**: `∑αᵢ - (1/2)∑∑αᵢαⱼyᵢyⱼxᵢᵀxⱼ`
- **Subject to**:
  - `∑αᵢyᵢ = 0`
  - `0 ≤ αᵢ ≤ C`

### KKT Conditions
- `αᵢ = 0` → Point is not a support vector
- `0 < αᵢ < C` → Point is on margin boundary
- `αᵢ = C` → Point violates margin (misclassified or within margin)

### Decision Function
- **Formula**: `f(x) = ∑αᵢyᵢxᵢᵀx + b`
- **Classification**: `sign(f(x))`

## Non-Linear SVM and Kernels

### Kernel Trick
Transform data to higher-dimensional space where it becomes linearly separable.

**Key Insight:** Only need dot products `xᵢᵀxⱼ` → Replace with `K(xᵢ, xⱼ)`

### Common Kernels

#### Linear Kernel
- **Formula**: `K(xᵢ, xⱼ) = xᵢᵀxⱼ`
- **Use**: Already linearly separable data

#### Polynomial Kernel
- **Formula**: `K(xᵢ, xⱼ) = (xᵢᵀxⱼ + c)ᵈ`
- **Parameters**: 
  - `d` = degree
  - `c` = constant term
- **Use**: Data with polynomial patterns

#### Radial Basis Function (RBF) / Gaussian Kernel
- **Formula**: `K(xᵢ, xⱼ) = exp(-γ||xᵢ - xⱼ||²)`
- **Parameter**: `γ = 1/(2σ²)`
- **Properties**:
  - `γ` large → Tight fit (overfitting risk)
  - `γ` small → Smooth decision boundary
- **Use**: Most popular, works well for many problems

#### Sigmoid Kernel
- **Formula**: `K(xᵢ, xⱼ) = tanh(αxᵢᵀxⱼ + c)`
- **Use**: Neural network-like behavior

### Kernel Decision Function
- **Formula**: `f(x) = ∑αᵢyᵢK(xᵢ, x) + b`

## SVM for Regression (SVR)

### ε-insensitive Loss
- **No penalty** for errors within ε-tube
- **Linear penalty** for errors outside ε-tube

### SVR Optimization
- **Minimize**: `(1/2)||w||² + C∑(ξᵢ + ξᵢ*)`
- **Subject to**:
  - `yᵢ - wᵀxᵢ - b ≤ ε + ξᵢ`
  - `wᵀxᵢ + b - yᵢ ≤ ε + ξᵢ*`
  - `ξᵢ, ξᵢ* ≥ 0`

## Multiclass SVM

### One-vs-One (OvO)
- Train `k(k-1)/2` binary classifiers
- **Decision**: Majority voting
- **Advantage**: Smaller training sets per classifier

### One-vs-Rest (OvR)
- Train `k` binary classifiers
- **Decision**: Highest confidence score
- **Advantage**: Fewer classifiers

### Direct Multiclass Methods
- **Crammer-Singer**: Single optimization problem
- **Lee-Lin-Wahba**: Modified dual formulation

## Hyperparameter Tuning

### Key Hyperparameters

#### Regularization Parameter (C)
- **Effect**: Trade-off between margin width and misclassification
- **Values**: Typically 0.1, 1, 10, 100
- **Cross-validation**: Use grid search

#### Kernel Parameters

**RBF Gamma (γ):**
- **Effect**: Controls decision boundary complexity
- **Values**: 'scale' (1/n_features), 'auto' (1/n_features), or specific values

**Polynomial Degree (d):**
- **Effect**: Complexity of decision boundary
- **Values**: Typically 2, 3, 4

### Grid Search Strategy
1. **Coarse grid**: Large intervals
2. **Fine grid**: Narrow down around best parameters
3. **Cross-validation**: Use k-fold CV for robust evaluation

## Advantages and Disadvantages

### Advantages
- **Effective** in high-dimensional spaces
- **Memory efficient** (uses subset of training points)
- **Versatile** (different kernels)
- **Works well** when #features > #samples

### Disadvantages
- **No probabilistic output** (need Platt scaling)
- **Sensitive to feature scaling**
- **Slow on large datasets**
- **Choice of kernel and parameters** crucial

## Feature Scaling

### Importance
- SVM sensitive to feature scales
- Features with larger scales dominate distance calculations

### Scaling Methods
- **Standardization**: `x' = (x - μ) / σ`
- **Min-Max Normalization**: `x' = (x - min) / (max - min)`

### When to Scale
- **Always** for RBF, polynomial, sigmoid kernels
- **Optional** for linear kernel (but recommended)

## Model Selection and Evaluation

### Cross-Validation
- **k-fold CV** for hyperparameter selection
- **Stratified CV** for imbalanced datasets

### Evaluation Metrics
- **Accuracy**: Overall correctness
- **Precision/Recall**: For imbalanced classes
- **F1-Score**: Harmonic mean of precision/recall
- **ROC-AUC**: For binary classification

### Overfitting Indicators
- **High training accuracy, low validation accuracy**
- **Very complex decision boundary**
- **Large number of support vectors**

## Practical Tips

### Data Preprocessing
1. **Scale features** (standardization/normalization)
2. **Handle missing values**
3. **Remove or treat outliers**
4. **Feature selection** if many irrelevant features

### Hyperparameter Selection
1. **Start with RBF kernel**
2. **Use grid search with cross-validation**
3. **Consider computational constraints**
4. **Try different kernel functions**

### Debugging
- **Check data scaling**
- **Visualize decision boundary** (2D data)
- **Examine support vectors**
- **Monitor training time**

## Comparison with Other Algorithms

| Aspect | SVM | Logistic Regression | Random Forest |
|--------|-----|-------------------|---------------|
| **Interpretability** | Low | High | Medium |
| **Feature Scaling** | Required | Recommended | Not Required |
| **Large Datasets** | Slow | Fast | Fast |
| **High Dimensions** | Good | Good | Moderate |
| **Probabilistic Output** | No* | Yes | Yes |
| **Hyperparameters** | Many | Few | Several |

*Requires Platt scaling for probabilities

## Key Formulas Summary

| Concept | Formula |
|---------|---------|
| Hyperplane | `wᵀx + b = 0` |
| Margin | `M = 2/||w||` |
| Soft Margin Objective | `min (1/2)||w||² + C∑ξᵢ` |
| Dual Objective | `max ∑αᵢ - (1/2)∑∑αᵢαⱼyᵢyⱼK(xᵢ,xⱼ)` |
| Decision Function | `f(x) = ∑αᵢyᵢK(xᵢ,x) + b` |
| RBF Kernel | `K(xᵢ,xⱼ) = exp(-γ||xᵢ-xⱼ||²)` |
| Polynomial Kernel | `K(xᵢ,xⱼ) = (xᵢᵀxⱼ + c)ᵈ` |

---
