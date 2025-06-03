## Overview
Logistic regression is used for binary classification problems where the output is categorical (0 or 1, Yes or No, etc.).

### Key Differences from Linear Regression
- **Output**: Probability values between 0 and 1
- **Function**: Uses sigmoid/logistic function instead of linear
- **Purpose**: Classification rather than regression

### Binary vs Multiclass
- **Binary**: Two classes (0 or 1)
- **Multiclass**: Multiple classes (One-vs-Rest or One-vs-One)

## Sigmoid Function

### Mathematical Form
- **Formula**: `σ(z) = 1 / (1 + e^(-z))`
- **Where**: `z = θ₀ + θ₁x₁ + θ₂x₂ + ... + θₙxₙ`

### Properties
- **Range**: (0, 1)
- **Shape**: S-curved
- **Interpretation**: Output represents probability
- **Decision Boundary**: `σ(z) = 0.5` when `z = 0`

### Hypothesis Function
- **Formula**: `hθ(x) = σ(θᵀx) = 1 / (1 + e^(-θᵀx))`
- **Interpretation**: `hθ(x) = P(y = 1 | x; θ)`

## Decision Boundary

### Linear Decision Boundary
- **Condition**: `θᵀx = 0`
- **Prediction**: 
  - `y = 1` if `hθ(x) ≥ 0.5` (i.e., `θᵀx ≥ 0`)
  - `y = 0` if `hθ(x) < 0.5` (i.e., `θᵀx < 0`)

### Non-linear Decision Boundary
- Add polynomial features: `x₁², x₂², x₁x₂`, etc.
- Creates curved decision boundaries

## Cost Function

### Why Not MSE?
- MSE with sigmoid creates non-convex function
- Multiple local minima make optimization difficult

### Logistic Cost Function
**For single training example:**
- `Cost(hθ(x), y) = -y log(hθ(x)) - (1-y) log(1-hθ(x))`

**For entire dataset:**
- `J(θ) = -(1/m) Σ[y⁽ⁱ⁾ log(hθ(x⁽ⁱ⁾)) + (1-y⁽ⁱ⁾) log(1-hθ(x⁽ⁱ⁾))]`

### Cost Function Intuition
- **When y = 1**: `Cost = -log(hθ(x))`
  - Cost → 0 as `hθ(x) → 1` (correct prediction)
  - Cost → ∞ as `hθ(x) → 0` (wrong prediction)
- **When y = 0**: `Cost = -log(1-hθ(x))`
  - Cost → 0 as `hθ(x) → 0` (correct prediction)
  - Cost → ∞ as `hθ(x) → 1` (wrong prediction)

## Gradient Descent for Logistic Regression

### Gradient Calculation
- **Partial Derivative**: `∂J(θ)/∂θⱼ = (1/m) Σ(hθ(x⁽ⁱ⁾) - y⁽ⁱ⁾)xⱼ⁽ⁱ⁾`

### Parameter Update Rule
- `θⱼ := θⱼ - α ∂J(θ)/∂θⱼ`
- **Vectorized**: `θ := θ - α(1/m)Xᵀ(σ(Xθ) - y)`

### Algorithm Steps
1. Initialize parameters `θ`
2. Calculate hypothesis `hθ(x) = σ(θᵀx)`
3. Calculate cost function `J(θ)`
4. Calculate gradients
5. Update parameters
6. Repeat until convergence

### Gradient Descent Variants

#### Batch Gradient Descent
- Uses entire dataset for each update
- **Update**: `θ := θ - α(1/m)Xᵀ(σ(Xθ) - y)`

#### Stochastic Gradient Descent
- Uses one example at a time
- Faster for large datasets
- More noisy convergence

#### Mini-batch Gradient Descent
- Uses small batches
- Balance between batch and stochastic

## Advanced Optimization

### Beyond Basic Gradient Descent
- **Conjugate Gradient**
- **BFGS (Broyden-Fletcher-Goldfarb-Shanno)**
- **L-BFGS (Limited-memory BFGS)**

### Advantages of Advanced Methods
- No need to manually pick learning rate
- Often faster convergence
- Automatically adjust step size

## Regularization

### Ridge Logistic Regression (L2)
- **Cost Function**: `J(θ) = Original Cost + λΣθⱼ²`
- **Gradient**: `∂J/∂θⱼ = Original Gradient + (λ/m)θⱼ`

### LASSO Logistic Regression (L1)
- **Cost Function**: `J(θ) = Original Cost + λΣ|θⱼ|`
- **Effect**: Feature selection (sets coefficients to zero)

### Elastic Net
- **Cost Function**: Combines L1 and L2 penalties
- **Formula**: `J(θ) = Original Cost + λ₁Σ|θⱼ| + λ₂Σθⱼ²`

## Multiclass Classification

### One-vs-Rest (One-vs-All)
- Train K binary classifiers (K = number of classes)
- Each classifier: "Class i vs All other classes"
- **Prediction**: Choose class with highest probability

### One-vs-One
- Train K(K-1)/2 binary classifiers
- Each classifier: "Class i vs Class j"
- **Prediction**: Majority voting

### Softmax Regression (Multinomial Logistic)
- **Hypothesis**: `hθ(x) = [P(y=1|x), P(y=2|x), ..., P(y=K|x)]`
- **Softmax Function**: `P(y=k|x) = e^(θₖᵀx) / Σe^(θⱼᵀx)`

## Model Evaluation

### Confusion Matrix
```
           Predicted
Actual    0    1
   0     TN   FP
   1     FN   TP
```

### Key Metrics
- **Accuracy**: `(TP + TN) / (TP + TN + FP + FN)`
- **Precision**: `TP / (TP + FP)`
- **Recall (Sensitivity)**: `TP / (TP + FN)`
- **Specificity**: `TN / (TN + FP)`
- **F1-Score**: `2 × (Precision × Recall) / (Precision + Recall)`

### ROC Curve and AUC
- **ROC**: Receiver Operating Characteristic
- **Plot**: True Positive Rate vs False Positive Rate
- **AUC**: Area Under Curve (0 to 1, higher is better)

## Feature Engineering

### Polynomial Features
- Add `x₁², x₂², x₁x₂` for non-linear boundaries
- Higher-order polynomials for complex patterns

### Feature Scaling
- **Standardization**: `x' = (x - μ) / σ`
- **Normalization**: `x' = (x - min) / (max - min)`
- **Important**: Logistic regression sensitive to feature scales

## Assumptions

### Key Assumptions
1. **Linear relationship** between logit and features
2. **Independence** of observations
3. **No perfect multicollinearity**
4. **Large sample size** for stable results

### Checking Assumptions
- **Linearity**: Plot logit vs continuous features
- **Multicollinearity**: Check correlation matrix, VIF
- **Outliers**: Use residual analysis

## Common Issues & Solutions

### Convergence Problems
- **Slow convergence**: Adjust learning rate, scale features
- **No convergence**: Check for perfect separation
- **Oscillation**: Reduce learning rate

### Perfect Separation
- **Problem**: Classes completely separable
- **Symptoms**: Coefficients become very large
- **Solutions**: Regularization, more data, feature engineering

### Class Imbalance
- **Problem**: Unequal class distribution
- **Solutions**: 
  - Adjust decision threshold
  - Use different evaluation metrics
  - Sampling techniques (SMOTE, undersampling)
  - Class weights

## Comparison: Linear vs Logistic Regression

| Aspect | Linear Regression | Logistic Regression |
|--------|------------------|-------------------|
| **Output** | Continuous values | Probabilities (0-1) |
| **Function** | Linear | Sigmoid |
| **Cost Function** | MSE | Log-likelihood |
| **Purpose** | Regression | Classification |
| **Assumptions** | Normality of residuals | Large sample size |

## Key Formulas Summary

| Concept | Formula |
|---------|---------|
| Sigmoid Function | `σ(z) = 1 / (1 + e^(-z))` |
| Hypothesis | `hθ(x) = σ(θᵀx)` |
| Cost Function | `J(θ) = -(1/m) Σ[y log(hθ(x)) + (1-y) log(1-hθ(x))]` |
| Gradient | `∂J/∂θⱼ = (1/m) Σ(hθ(x⁽ⁱ⁾) - y⁽ⁱ⁾)xⱼ⁽ⁱ⁾` |
| Parameter Update | `θⱼ := θⱼ - α ∂J(θ)/∂θⱼ` |
| Decision Boundary | `θᵀx = 0` |
| Odds | `odds = p / (1-p)` |
| Log-odds (Logit) | `logit(p) = ln(p / (1-p)) = θᵀx` |

---
