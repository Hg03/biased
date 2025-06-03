## Overview
Decision Tree is a supervised learning algorithm that creates a model predicting target values by learning simple decision rules inferred from data features. It splits data recursively based on feature values.

### Key Characteristics
- **Interpretable**: Easy to understand and visualize
- **Non-parametric**: No assumptions about data distribution
- **Handles both**: Classification and regression
- **Feature selection**: Automatically selects important features

### Tree Structure
- **Root Node**: Top node representing entire dataset
- **Internal Nodes**: Decision points based on feature tests
- **Leaf Nodes**: Final predictions (class labels or values)
- **Branches**: Outcomes of decision tests

## How Decision Trees Work

### Building Process
1. **Start** with root node containing all data
2. **Find best feature** to split on using impurity measures
3. **Create branches** for each possible value/threshold
4. **Recursively split** each subset
5. **Stop** when stopping criterion is met

### Decision Making
- **Classification**: Follow path from root to leaf based on feature values
- **Prediction**: Use majority class (classification) or mean value (regression) at leaf

## Splitting Criteria

### For Classification

#### Gini Impurity
- **Formula**: `Gini = 1 - Σpᵢ²`
- **Where**: `pᵢ` = proportion of samples belonging to class i
- **Range**: 0 (pure) to 0.5 (binary classification, maximum impurity)
- **Interpretation**: Probability of misclassifying a randomly chosen sample

#### Entropy (Information Gain)
- **Formula**: `Entropy = -Σpᵢ log₂(pᵢ)`
- **Range**: 0 (pure) to log₂(classes) (maximum impurity)
- **Information Gain**: `IG = Entropy(parent) - Σ(|Sᵢ|/|S|) × Entropy(Sᵢ)`

#### Gain Ratio
- **Formula**: `Gain Ratio = Information Gain / Split Information`
- **Split Information**: `SI = -Σ(|Sᵢ|/|S|) × log₂(|Sᵢ|/|S|)`
- **Purpose**: Penalizes splits that create many small partitions

### For Regression

#### Mean Squared Error (MSE)
- **Formula**: `MSE = (1/n) Σ(yᵢ - ȳ)²`
- **Reduction**: `MSE_reduction = MSE(parent) - Σ(nᵢ/n) × MSE(childᵢ)`

#### Mean Absolute Error (MAE)
- **Formula**: `MAE = (1/n) Σ|yᵢ - ȳ|`
- **Less sensitive**: To outliers compared to MSE

## Splitting Process

### For Continuous Features
1. **Sort** feature values
2. **Consider splits** between consecutive values
3. **Evaluate** each potential split point
4. **Choose** split with best criterion improvement

### For Categorical Features
- **Binary splits**: Each category vs others
- **Multi-way splits**: One branch per category
- **Subset splits**: Group categories optimally

### Best Split Selection
- **Exhaustive search**: Try all possible splits
- **Greedy approach**: Choose locally optimal split
- **No backtracking**: Once split is made, it's permanent

## Stopping Criteria

### Common Stopping Rules
1. **Maximum depth**: Limit tree depth
2. **Minimum samples per leaf**: Ensure adequate sample size
3. **Minimum samples to split**: Required samples for internal node
4. **Minimum impurity decrease**: Split must improve impurity significantly
5. **Maximum leaf nodes**: Limit total number of leaves

### Early Stopping Benefits
- **Prevents overfitting**: Avoids overly complex trees
- **Reduces training time**: Fewer splits to evaluate
- **Improves generalization**: Simpler models often generalize better

## Pruning

### Why Prune?
- **Overfitting**: Large trees may memorize training data
- **Complexity**: Simpler trees are more interpretable
- **Generalization**: Pruned trees often perform better on test data

### Pre-pruning (Early Stopping)
- **Apply during** tree construction
- **Stop splitting** when criteria are met
- **Risk**: May stop too early and underfit

### Post-pruning
**Process after** tree is fully grown

#### Cost Complexity Pruning (Minimal Cost-Complexity)
- **Cost function**: `R_α(T) = R(T) + α|T|`
- **Where**: 
  - `R(T)` = misclassification rate
  - `|T|` = number of leaves
  - `α` = complexity parameter
- **Process**: Find sequence of trees with increasing α values

#### Reduced Error Pruning
- **Use validation set** to evaluate pruning decisions
- **Remove subtrees** that don't hurt validation performance
- **Greedy approach**: Prune node with best validation improvement

## Advantages and Disadvantages

### Advantages
- **Interpretability**: Easy to understand and explain
- **No preprocessing**: Handles numerical and categorical data
- **Feature selection**: Automatically identifies important features
- **Non-linear relationships**: Can capture complex patterns
- **Missing values**: Can handle missing data naturally
- **Fast prediction**: O(log n) for balanced trees

### Disadvantages
- **Overfitting**: Prone to creating overly complex trees
- **Instability**: Small data changes can create very different trees
- **Bias**: Favors features with more levels
- **Linear relationships**: May not capture linear patterns efficiently
- **Imbalanced data**: May be biased toward majority classes

## Handling Different Data Types

### Numerical Features
- **Binary splits**: feature ≤ threshold vs feature > threshold
- **Find optimal threshold**: Try midpoints between consecutive values
- **Missing values**: Can assign to either branch or create separate branch

### Categorical Features
- **Nominal**: Unordered categories (color, city)
  - **Binary encoding**: Each category vs others
  - **Subset splits**: Group categories optimally
- **Ordinal**: Ordered categories (size: small, medium, large)
  - **Treat as numerical**: Assign numerical values maintaining order

### Missing Values
1. **Surrogate splits**: Use alternative features for splitting
2. **Assign to majority**: Send to most common branch
3. **Probabilistic assignment**: Distribute proportionally to both branches

## Feature Importance

### Calculation
**For each feature**: Sum of impurity decreases weighted by number of samples

**Formula**: `Importance(feature) = Σ (n/N) × (impurity_before - impurity_after)`

### Interpretation
- **Higher values**: More important features
- **Relative measure**: Compare importance across features
- **Bias**: Favors features allowing more splits

## Hyperparameter Tuning

### Key Hyperparameters

#### Tree Structure
- **max_depth**: Maximum tree depth (default: None)
  - **Typical range**: 3-20
  - **Effect**: Controls overfitting
- **min_samples_split**: Minimum samples to split internal node (default: 2)
  - **Typical range**: 2-100
  - **Effect**: Prevents splits with few samples
- **min_samples_leaf**: Minimum samples per leaf (default: 1)
  - **Typical range**: 1-50
  - **Effect**: Ensures leaf nodes have adequate samples

#### Splitting Criteria
- **criterion**: Splitting criterion
  - **Classification**: 'gini', 'entropy', 'log_loss'
  - **Regression**: 'squared_error', 'absolute_error'
- **max_features**: Features to consider per split
  - **Options**: 'sqrt', 'log2', None, int, float

#### Pruning Parameters
- **min_impurity_decrease**: Minimum impurity decrease for split
- **max_leaf_nodes**: Maximum number of leaf nodes
- **ccp_alpha**: Cost complexity pruning parameter

### Tuning Strategy
1. **Start simple**: Small max_depth, higher min_samples_leaf
2. **Cross-validation**: Use k-fold CV for parameter selection
3. **Grid search**: Systematic parameter exploration
4. **Validation curves**: Plot performance vs parameter values

## Model Evaluation

### Classification Metrics
- **Accuracy**: Overall correctness
- **Precision/Recall**: For imbalanced classes
- **F1-Score**: Harmonic mean of precision/recall
- **Confusion Matrix**: Detailed error analysis

### Regression Metrics
- **Mean Squared Error**: `MSE = (1/n)Σ(yᵢ - ŷᵢ)²`
- **Mean Absolute Error**: `MAE = (1/n)Σ|yᵢ - ŷᵢ|`
- **R-squared**: Proportion of variance explained

### Cross-Validation
- **k-fold CV**: Standard approach
- **Stratified CV**: For classification with imbalanced classes
- **Time series CV**: For temporal data

## Practical Tips

### Data Preparation
1. **Handle missing values**: Decide on strategy
2. **Feature scaling**: Not required for decision trees
3. **Categorical encoding**: Not always necessary
4. **Outlier treatment**: Trees are robust to outliers

### Avoiding Overfitting
1. **Limit tree depth**: Use max_depth parameter
2. **Increase minimum samples**: Use min_samples_leaf, min_samples_split
3. **Pruning**: Apply post-pruning techniques
4. **Cross-validation**: Use for hyperparameter tuning

### Interpretability
1. **Visualize tree**: Use tree plotting tools
2. **Feature importance**: Analyze which features matter most
3. **Decision paths**: Trace individual predictions
4. **Rule extraction**: Convert tree to if-then rules

## Comparison with Other Algorithms

| Aspect | Decision Tree | Linear Models | SVM | Naive Bayes |
|--------|---------------|---------------|-----|-------------|
| **Interpretability** | Very High | High | Low | Medium |
| **Feature Scaling** | Not Required | Required | Required | Not Required |
| **Non-linear** | Yes | No | Yes (with kernels) | Limited |
| **Training Speed** | Fast | Fast | Slow | Very Fast |
| **Overfitting Risk** | High | Low-Medium | Medium | Low |
| **Missing Values** | Handles Well | Needs Preprocessing | Needs Preprocessing | Needs Preprocessing |

## Applications

### Classification Problems
- **Medical diagnosis**: Symptom-based decision making
- **Credit approval**: Loan application decisions
- **Marketing**: Customer segmentation
- **Quality control**: Defect detection

### Regression Problems
- **Price prediction**: Real estate, stock prices
- **Risk assessment**: Insurance, finance
- **Performance prediction**: Sports, academics
- **Resource planning**: Demand forecasting

## Tree Visualization and Interpretation

### Visualization Elements
- **Nodes**: Show split condition and sample information
- **Colors**: Represent class purity or target values
- **Node size**: Proportional to number of samples

### Reading Tree Rules
**Example Rule:**
```
IF feature_1 <= 5.5 AND feature_2 > 3.2 THEN class = A
```

### Feature Importance Analysis
1. **Rank features** by importance scores
2. **Focus on top features** for domain insights
3. **Validate importance** with domain knowledge

## Key Concepts Summary

| Concept | Description |
|---------|-------------|
| **Gini Impurity** | `1 - Σpᵢ²` |
| **Entropy** | `-Σpᵢ log₂(pᵢ)` |
| **Information Gain** | `Entropy(parent) - Weighted_Entropy(children)` |
| **Feature Importance** | `Σ (n/N) × (impurity_decrease)` |
| **Pruning** | Removing subtrees to reduce overfitting |
| **Stopping Criteria** | Rules to halt tree growth |

---
