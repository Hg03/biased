---
title: "Linear Regression"
description: Sticking to basics is always mandatory.
date: 2025-05-10
lastmod: 2025-05-10
keywords: ["linearregression", "algorithm", "ml"]
tags: ["algorithm", "ml"]
summary: We'll learn about linear regression. Simple, straight & forward.
toc: true
math: true
---

# Linear Regression with Gradient Descent

## Introduction
Linear regression is a fundamental statistical and machine learning technique used to model the relationship between a dependent variable and one or more independent variables. Gradient descent is an optimization algorithm used to find the parameters (weights) that minimize the error in the model's predictions.

## The Linear Model
A linear regression model with one independent variable can be represented as:
```
y = mx + b
```
Where:
- y is the predicted value
- x is the independent variable
- m is the slope (coefficient)
- b is the y-intercept

For multiple independent variables, this extends to:
```
y = b + w₁x₁ + w₂x₂ + ... + wₙxₙ
```

## Cost Function
We need a way to measure how good our model is. For linear regression, we typically use the Mean Squared Error (MSE):
```
MSE = (1/n) * Σ(y_actual - y_predicted)²
```

This measures the average squared difference between the actual values and the predicted values.

## Gradient Descent Algorithm
Gradient descent is an iterative optimization algorithm that:
1. Starts with initial values for the parameters (often set to zeros or random values)
2. Computes the gradient (direction of steepest increase) of the cost function
3. Takes a step in the opposite direction of the gradient (since we want to minimize the cost)
4. Repeats until convergence

### The Update Rule
For each parameter θⱼ:
```
θⱼ = θⱼ - α * ∂J/∂θⱼ
```
Where:
- α is the learning rate (a hyperparameter that controls step size)
- ∂J/∂θⱼ is the partial derivative of the cost function with respect to parameter θⱼ

For linear regression, the update rules are:
```
b = b - α * (1/n) * Σ(y_predicted - y_actual)
wⱼ = wⱼ - α * (1/n) * Σ((y_predicted - y_actual) * xⱼ)
```

## Gradient Descent Variants
1. **Batch Gradient Descent**: Uses the entire dataset to compute the gradient for each update
2. **Stochastic Gradient Descent (SGD)**: Uses only one sample per update
3. **Mini-Batch Gradient Descent**: Uses a small random subset of data for each update

## Implementation Steps
1. Initialize parameters (weights and bias)
2. For a set number of iterations (or until convergence):
   - Calculate predictions using current parameters
   - Calculate the error/loss
   - Calculate gradients
   - Update parameters using the gradient descent rule
   - Repeat

## Challenges and Solutions
- **Learning Rate**: If too large, may overshoot; if too small, convergence is slow
- **Feature Scaling**: Standardize features for faster convergence
- **Local Minima**: Generally not an issue for linear regression as the cost function is convex

## Evaluating the Model
Common metrics include:
- Mean Squared Error (MSE)
- Root Mean Squared Error (RMSE)
- R-squared (coefficient of determination)

<!--
## Details

{{< details summary="See the details" >}}
This is a **bold** word.
{{< /details >}}

## Highlight

{{< highlight go-html-template >}}
{{ range .Pages }}
  <h2><a href="{{ .RelPermalink }}">{{ .LinkTitle }}</a></h2>
{{ end }}
{{< /highlight >}}

With emphasize lines:

```go {linenos=inline hl_lines=[3,"6-8"] style=dracula}
package main

import "fmt"

func main() {
    for i := 0; i < 3; i++ {
        fmt.Println("Value of i:", i)
    }
}
```

## Images

{{< figure src="https://images.unsplash.com/photo-1560032779-0a8809186efd?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1350&q=80" title="Dave Herring" >}}

{{< figure src="https://images.unsplash.com/photo-1560032779-0a8809186efd?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=500&q=80" title="Dave Herring" >}}


## Github Gist

{{< gist imgios f587d813ec6c851d700054f89230fb42 >}}

## Youtube video

{{< youtube w7Ft2ymGmfc >}}

## Tweet

{{< tweet user="GoHugoIO" id="877500564405444608" >}}

## Vimeo

{{< vimeo id="146022717" >}}

## Instagram

{{< instagram BWNjjyYFxVx >}}

-->
