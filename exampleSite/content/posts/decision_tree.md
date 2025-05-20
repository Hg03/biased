---
title: "Decision Tree Algorithm"
description: Sticking to basics is always mandatory.
date: 2025-05-10
lastmod: 2025-05-10
keywords: ["decisiontree", "algorithm", "ml"]
tags: ["algorithm", "ml"]
summary: We'll learn about decision tree classification. Simple, straight & forward.
toc: true
math: true
---

# Decision Tree Algorithm

## Introduction
Decision trees are a supervised learning method used for classification and regression. They work by recursively splitting the data based on features to create a tree-like model of decisions.

## Core Concepts

### Structure
- **Root Node**: The topmost node representing the entire dataset
- **Decision Node**: A node that splits into multiple branches
- **Leaf/Terminal Node**: A node that does not split further (final outcome)
- **Branch/Edge**: Connects nodes, represents decision rules

### Building a Decision Tree

1. **Feature Selection**: Choose the most significant feature for splitting
2. **Splitting Criteria**: Use metrics to determine optimal splits
3. **Recursive Partitioning**: Continue splitting until stopping criteria met
4. **Pruning**: Remove branches to prevent overfitting

## Splitting Criteria

### For Classification

#### Gini Impurity
Measures the probability of incorrect classification:

$$Gini(D) = 1 - \sum_{i=1}^{c} p_i^2$$

Where:
- $D$ is the dataset
- $c$ is the number of classes
- $p_i$ is the probability of class $i$

#### Entropy & Information Gain
Entropy measures uncertainty:

$$Entropy(D) = -\sum_{i=1}^{c} p_i \log_2(p_i)$$

Information Gain measures reduction in entropy:

$$IG(D, A) = Entropy(D) - \sum_{v \in Values(A)} \frac{|D_v|}{|D|} Entropy(D_v)$$

Where:
- $A$ is the attribute to split on
- $D_v$ is the subset of $D$ where attribute $A$ has value $v$

### For Regression

#### Variance Reduction
For regression trees, variance is used:

$$Variance = \frac{1}{n} \sum_{i=1}^{n} (y_i - \mu)^2$$

Where:
- $n$ is the number of samples
- $y_i$ is the target value for sample $i$
- $\mu$ is the mean target value

## Algorithms

### ID3 (Iterative Dichotomiser 3)
- Uses entropy and information gain
- Only handles categorical attributes
- Does not support pruning

### C4.5 (Successor of ID3)
- Can handle both continuous and categorical attributes
- Uses gain ratio to avoid bias toward features with many values:

$$GainRatio(D, A) = \frac{IG(D, A)}{SplitInfo(D, A)}$$

Where:

$$SplitInfo(D, A) = -\sum_{v \in Values(A)} \frac{|D_v|}{|D|} \log_2\left(\frac{|D_v|}{|D|}\right)$$

### CART (Classification and Regression Trees)
- Produces binary trees
- Uses Gini impurity for classification
- Uses variance reduction for regression

## Advantages & Disadvantages

### Advantages
- Interpretable and easy to visualize
- Handles both numerical and categorical data
- Requires minimal data preprocessing
- Automatically handles feature interactions

### Disadvantages
- Prone to overfitting
- Can create biased trees if classes are imbalanced
- Small variations in data might result in different trees
- May not be as accurate as more complex models

## Pruning Techniques

### Pre-pruning
Stop growing the tree before it perfectly classifies the training data:
- Maximum depth
- Minimum samples per leaf
- Minimum impurity decrease

### Post-pruning
Build the full tree, then remove branches:
- **Reduced Error Pruning**: Remove nodes if removal doesn't decrease accuracy on validation set
- **Cost Complexity Pruning**: Balance accuracy against tree complexity using parameter α

The cost complexity function:

$$R_α(T) = R(T) + α × |T|$$

Where:
- R(T) is the error rate of tree T on training data
- |T| is the number of terminal nodes in tree T
- α is the complexity parameter that weights the tree size

## Hyperparameter Tuning
- **max_depth**: Maximum depth of the tree
- **min_samples_split**: Minimum samples required to split a node
- **min_samples_leaf**: Minimum samples required for a leaf node
- **max_features**: Maximum number of features to consider for splitting
- **criterion**: Function to measure split quality (gini/entropy for classification, mse/mae for regression)

## Random Forests
Ensemble of decision trees to improve:
- Accuracy
- Overfitting
- Stability

The final prediction is the average of all individual tree predictions:

$$\hat{y} = \frac{1}{B} \sum_{b=1}^{B} f_b(x)$$

Where:
- B is the number of trees
- $f_b$ is the b-th decision tree
- $\hat{y}$ is the predicted value
