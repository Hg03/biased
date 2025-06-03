## Overview
Linear regression models the relationship between dependent and independent variables using a linear equation.

### Simple Linear Regression
- **Equation**: `y = β₀ + β₁x + ε`
  - `β₀` = intercept
  - `β₁` = slope
  - `ε` = error term

### Multiple Linear Regression
- **Equation**: `y = β₀ + β₁x₁ + β₂x₂ + ... + βₙxₙ + ε`

## Key Assumptions
1. **Linearity**: Linear relationship between variables
2. **Independence**: Observations are independent
3. **Homoscedasticity**: Constant variance of residuals
4. **Normality**: Residuals are normally distributed
5. **No Multicollinearity**: Independent variables not highly correlated

## Cost Function
The cost function measures how well our model fits the data.

### Mean Squared Error (MSE)
- **Formula**: `J(θ) = (1/2m) Σ(hθ(x⁽ⁱ⁾) - y⁽ⁱ⁾)²`
- **Components**:
  - `m` = number of training examples
  - `hθ(x)` = hypothesis function
  - `y⁽ⁱ⁾` = actual value

### Hypothesis Function
- **Simple**: `hθ(x) = θ₀ + θ₁x`
- **Multiple**: `hθ(x) = θ₀ + θ₁x₁ + θ₂x₂ + ... + θₙxₙ`

## Gradient Descent

### Overview
Gradient descent is an optimization algorithm used to minimize the cost function by iteratively adjusting parameters.

### Algorithm Steps
1. Initialize parameters `θ₀, θ₁, ..., θₙ`
2. Calculate cost function `J(θ)`
3. Calculate gradients (partial derivatives)
4. Update parameters using learning rate
5. Repeat until convergence

### Parameter Update Rule
**Simultaneous update for all parameters:**
- `θⱼ := θⱼ - α ∂J(θ)/∂θⱼ`

Where:
- `α` = learning rate
- `∂J(θ)/∂θⱼ` = partial derivative of cost function

### Gradient Calculations

#### Simple Linear Regression
- `∂J(θ)/∂θ₀ = (1/m) Σ(hθ(x⁽ⁱ⁾) - y⁽ⁱ⁾)`
- `∂J(θ)/∂θ₁ = (1/m) Σ(hθ(x⁽ⁱ⁾) - y⁽ⁱ⁾)x⁽ⁱ⁾`

#### Multiple Linear Regression
- `∂J(θ)/∂θⱼ = (1/m) Σ(hθ(x⁽ⁱ⁾) - y⁽ⁱ⁾)xⱼ⁽ⁱ⁾`

### Types of Gradient Descent

#### Batch Gradient Descent
- Uses entire training dataset for each update
- **Pros**: Stable convergence, finds global minimum
- **Cons**: Slow for large datasets
- **Update**: Use all `m` examples

#### Stochastic Gradient Descent (SGD)
- Uses one training example at a time
- **Pros**: Fast updates, good for large datasets
- **Cons**: Noisy convergence, may not reach exact minimum
- **Update**: Use single example per iteration

#### Mini-batch Gradient Descent
- Uses small batches of training examples
- **Pros**: Balance between batch and SGD
- **Cons**: Need to choose batch size
- **Typical batch sizes**: 32, 64, 128, 256

### Learning Rate (α)

#### Choosing Learning Rate
- **Too small**: Slow convergence
- **Too large**: May overshoot minimum, fail to converge
- **Common values**: 0.001, 0.01, 0.1, 1

#### Learning Rate Strategies
- **Fixed**: Constant throughout training
- **Decay**: Gradually decrease over time
- **Adaptive**: Adjust based on gradient magnitude

### Convergence

#### Checking Convergence
- Plot cost function vs iterations
- Stop when cost decreases by less than threshold
- Common threshold: `10⁻⁶` or `10⁻³`

#### Convergence Indicators
- Cost function decreasing consistently
- Parameters stabilizing
- Gradient magnitude approaching zero

## Normal Equation vs Gradient Descent

### Normal Equation
- **Formula**: `θ = (XᵀX)⁻¹Xᵀy`
- **Pros**: No need to choose α, no iterations
- **Cons**: Expensive for large features (O(n³))

### When to Use Each
- **Gradient Descent**: n > 10,000 features
- **Normal Equation**: n < 10,000 features

## Feature Scaling

### Why Scale Features
- Different scales can slow convergence
- Features with larger ranges dominate gradient

### Scaling Methods

#### Normalization (Min-Max)
- **Formula**: `x' = (x - min) / (max - min)`
- **Range**: [0, 1]

#### Standardization (Z-score)
- **Formula**: `x' = (x - μ) / σ`
- **Result**: Mean = 0, Std = 1

## Model Evaluation

### R-squared (R²)
- **Formula**: `R² = 1 - (SSᵣₑₛ / SSₜₒₜ)`
- **Interpretation**: Proportion of variance explained
- **Range**: 0 to 1 (higher is better)

### Root Mean Squared Error (RMSE)
- **Formula**: `RMSE = √(MSE)`
- **Units**: Same as dependent variable

## Regularization with Gradient Descent

### Ridge Regression (L2)
- **Cost Function**: `J(θ) = MSE + λΣθⱼ²`
- **Gradient Update**: `θⱼ := θⱼ(1 - αλ/m) - α(1/m)Σ(error × xⱼ)`

### LASSO Regression (L1)
- **Cost Function**: `J(θ) = MSE + λΣ|θⱼ|`
- **Effect**: Can set coefficients to exactly zero

## Common Issues & Solutions

### Gradient Descent Problems
1. **Slow Convergence**: Decrease learning rate, scale features
2. **Divergence**: Decrease learning rate
3. **Local Minima**: Use different initialization (rare in linear regression)
4. **Oscillation**: Decrease learning rate

### Debugging Tips
- Plot cost function vs iterations
- Check if cost is decreasing
- Verify gradient calculations
- Try different learning rates

## Key Formulas Summary

| Concept | Formula |
|---------|---------|
| Hypothesis (Simple) | `hθ(x) = θ₀ + θ₁x` |
| Cost Function | `J(θ) = (1/2m) Σ(hθ(x⁽ⁱ⁾) - y⁽ⁱ⁾)²` |
| Parameter Update | `θⱼ := θⱼ - α ∂J(θ)/∂θⱼ` |
| Gradient (θ₀) | `∂J/∂θ₀ = (1/m) Σ(hθ(x⁽ⁱ⁾) - y⁽ⁱ⁾)` |
| Gradient (θ₁) | `∂J/∂θ₁ = (1/m) Σ(hθ(x⁽ⁱ⁾) - y⁽ⁱ⁾)x⁽ⁱ⁾` |
| Normal Equation | `θ = (XᵀX)⁻¹Xᵀy` |

---
