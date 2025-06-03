## Overview
Naive Bayes is a probabilistic classification algorithm based on Bayes' theorem with the "naive" assumption of conditional independence between features.

### Key Characteristics
- **Probabilistic**: Provides probability estimates for predictions
- **Fast**: Quick training and prediction
- **Simple**: Few hyperparameters to tune
- **Baseline**: Often used as baseline classifier

## Bayes' Theorem

### Mathematical Foundation
- **Formula**: `P(y|X) = P(X|y) × P(y) / P(X)`

**Components:**
- `P(y|X)` = Posterior probability (what we want)
- `P(X|y)` = Likelihood
- `P(y)` = Prior probability
- `P(X)` = Evidence (normalizing constant)

### For Classification
- **Goal**: Find class with highest posterior probability
- **Decision Rule**: `ŷ = argmax P(y|X)`

## Naive Assumption

### Conditional Independence
**Assumption**: Features are conditionally independent given the class label

**Mathematical Expression:**
`P(X|y) = P(x₁, x₂, ..., xₙ|y) = ∏P(xᵢ|y)`

### Why "Naive"?
- Features are rarely truly independent in real data
- Despite this violation, algorithm often works well
- Simplifies computation significantly

## Naive Bayes Classifier

### Classification Formula
`P(y|X) ∝ P(y) × ∏P(xᵢ|y)`

**Steps:**
1. Calculate prior probabilities `P(y)`
2. Calculate likelihoods `P(xᵢ|y)` for each feature
3. Multiply: `P(y) × ∏P(xᵢ|y)`
4. Choose class with highest probability

### Prior Probability
- **Formula**: `P(y = c) = Count(y = c) / Total samples`
- **Laplace Smoothing**: `P(y = c) = (Count(y = c) + α) / (Total + α × classes)`

## Types of Naive Bayes

### Gaussian Naive Bayes

**Use Case:** Continuous features that follow normal distribution

**Likelihood Formula:**
`P(xᵢ|y) = (1/√(2πσ²)) × exp(-(xᵢ - μ)²/2σ²)`

**Parameters to Estimate:**
- `μᵧ` = Mean of feature x for class y
- `σᵧ²` = Variance of feature x for class y

**Parameter Estimation:**
- `μᵧ = (1/nᵧ) ∑xᵢ` (for samples in class y)
- `σᵧ² = (1/nᵧ) ∑(xᵢ - μᵧ)²`

### Multinomial Naive Bayes

**Use Case:** Discrete features (word counts, frequencies)

**Likelihood Formula:**
`P(xᵢ|y) = (Count(xᵢ, y) + α) / (∑Count(xⱼ, y) + α × features)`

**Common Applications:**
- Text classification
- Document categorization
- Spam filtering

**Laplace Smoothing Parameter:** α (typically 1)

### Bernoulli Naive Bayes

**Use Case:** Binary features (presence/absence)

**Likelihood Formula:**
- `P(xᵢ = 1|y) = (Count(xᵢ = 1, y) + α) / (Count(y) + 2α)`
- `P(xᵢ = 0|y) = 1 - P(xᵢ = 1|y)`

**Applications:**
- Text classification with binary word presence
- Binary feature classification

### Complement Naive Bayes

**Use Case:** Imbalanced datasets

**Key Idea:** Estimate parameters using complement of each class

**Advantages:**
- More stable for imbalanced data
- Often better than Multinomial NB for text classification

## Smoothing Techniques

### Laplace Smoothing (Add-one)
**Problem:** Zero probabilities when feature value not seen in training

**Solution:** Add small constant α to all counts
- **Formula**: `P(xᵢ|y) = (Count(xᵢ, y) + α) / (Count(y) + α × values)`
- **Default**: α = 1

### Lidstone Smoothing
**Generalization of Laplace:** Use any α > 0
- **α = 1**: Laplace smoothing
- **α < 1**: Less smoothing
- **α > 1**: More smoothing

## Advantages and Disadvantages

### Advantages
- **Fast**: Quick training and prediction
- **Simple**: Easy to implement and understand
- **Probabilistic**: Provides confidence estimates
- **Small data**: Works well with limited training data
- **Multiclass**: Naturally handles multiple classes
- **Irrelevant features**: Relatively robust to irrelevant features

### Disadvantages
- **Independence assumption**: Rarely holds in practice
- **Categorical inputs**: Need discretization for continuous features (except Gaussian)
- **Zero probabilities**: Need smoothing techniques
- **Skewed data**: Performance degrades with highly skewed features

## Feature Engineering

### For Text Data
1. **Tokenization**: Split text into words
2. **Lowercasing**: Convert to lowercase
3. **Remove stopwords**: Filter common words
4. **Stemming/Lemmatization**: Reduce words to root form
5. **N-grams**: Consider word combinations

### For Continuous Data
1. **Discretization**: Convert to categorical (for Multinomial/Bernoulli)
2. **Normalization**: Scale features (for Gaussian)
3. **Handle outliers**: May affect Gaussian parameters

## Model Evaluation

### Classification Metrics
- **Accuracy**: `(TP + TN) / (TP + TN + FP + FN)`
- **Precision**: `TP / (TP + FP)`
- **Recall**: `TP / (TP + FN)`
- **F1-Score**: `2 × (Precision × Recall) / (Precision + Recall)`

### Cross-Validation
- **k-fold CV**: Standard approach
- **Stratified CV**: For imbalanced datasets
- **Leave-one-out**: For small datasets

### Probability Calibration
Naive Bayes probabilities often need calibration:
- **Platt Scaling**: Sigmoid function
- **Isotonic Regression**: Non-parametric approach

## Hyperparameter Tuning

### Key Parameters

#### Smoothing Parameter (α)
- **Range**: 0 to 10 (typically 0.1 to 2)
- **Effect**: Higher α = more smoothing
- **Tuning**: Use cross-validation

#### Gaussian NB Parameters
- **var_smoothing**: Smoothing for variance calculation
- **Default**: 1e-9

### Grid Search
```
parameters = {
    'alpha': [0.1, 0.5, 1.0, 2.0],
    'fit_prior': [True, False]
}
```

## Practical Applications

### Text Classification
- **Spam detection**: Email classification
- **Sentiment analysis**: Positive/negative reviews
- **Topic classification**: News categorization
- **Language detection**: Identify document language

### Other Applications
- **Medical diagnosis**: Based on symptoms
- **Recommendation systems**: User preference prediction
- **Real-time classification**: Fast prediction requirement

## Comparison with Other Algorithms

| Aspect | Naive Bayes | Logistic Regression | SVM |
|--------|-------------|-------------------|-----|
| **Speed** | Very Fast | Fast | Slow |
| **Assumptions** | Independence | Linear boundary | Margin maximization |
| **Probabilistic** | Yes | Yes | No* |
| **Feature Scaling** | Not Required | Required | Required |
| **Interpretability** | High | High | Low |
| **Small Datasets** | Excellent | Good | Moderate |

*Requires calibration

## Common Pitfalls and Solutions

### Zero Probability Problem
- **Problem**: Unseen feature values cause zero probabilities
- **Solution**: Use Laplace or Lidstone smoothing

### Highly Correlated Features
- **Problem**: Violates independence assumption
- **Solutions**: 
  - Feature selection
  - Dimensionality reduction
  - Use other algorithms

### Continuous Features
- **Problem**: Multinomial/Bernoulli NB can't handle continuous data directly
- **Solutions**:
  - Use Gaussian NB
  - Discretize continuous features
  - Use appropriate preprocessing

### Imbalanced Data
- **Problem**: Biased toward majority class
- **Solutions**:
  - Use Complement Naive Bayes
  - Adjust class priors
  - Sampling techniques

## Implementation Tips

### Data Preprocessing
1. **Handle missing values** before training
2. **Choose appropriate variant** based on data type
3. **Apply smoothing** to prevent zero probabilities
4. **Feature scaling** (for Gaussian NB)

### Model Selection
1. **Start with appropriate variant** (Gaussian/Multinomial/Bernoulli)
2. **Tune smoothing parameter** using cross-validation
3. **Compare with baseline** methods
4. **Calibrate probabilities** if needed

## Key Formulas Summary

| Concept | Formula |
|---------|---------|
| Bayes' Theorem | `P(y\|X) = P(X\|y) × P(y) / P(X)` |
| Naive Bayes | `P(y\|X) ∝ P(y) × ∏P(xᵢ\|y)` |
| Gaussian Likelihood | `P(xᵢ\|y) = (1/√(2πσ²)) × exp(-(xᵢ-μ)²/2σ²)` |
| Multinomial Likelihood | `P(xᵢ\|y) = (Count(xᵢ,y) + α) / (∑Count(xⱼ,y) + α×V)` |
| Laplace Smoothing | `P(xᵢ\|y) = (Count(xᵢ,y) + α) / (Count(y) + α×values)` |
| Prior Probability | `P(y) = Count(y) / Total` |

---
