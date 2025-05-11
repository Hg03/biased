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

## Linear Regression

Sure! Let’s break down **Linear Regression using Gradient Descent** in a fun and clear way—with emojis to keep it interactive! 😄📉📈

---

## 📌 What is Linear Regression?

Linear regression is a way to model the relationship between a **dependent variable** (target) and **one or more independent variables** (features). It finds a straight line (📏) that best fits the data points.

The general form of the line:

```
y = mx + b
```

or in machine learning terms:

```
ŷ = w*x + b
```

* `ŷ` = predicted value
* `w` = weight (slope)
* `x` = input feature
* `b` = bias (intercept)

---

## 🎯 Goal

Find the best values for **`w`** and **`b`** so the predicted values (ŷ) are as close as possible to the real target values (y).

We do this by **minimizing the error** 📉 using a method called **gradient descent**! 🔽

---

## 🧮 Step-by-Step: Gradient Descent

### 1️⃣ Define the **Loss Function**

We use **Mean Squared Error (MSE)** to measure how far off our predictions are:

$$
\text{MSE} = \frac{1}{n} \sum_{i=1}^{n}(y_i - \hat{y}_i)^2
$$

It tells us how "wrong" our line is on average. 🎯

---

### 2️⃣ Compute Gradients (Partial Derivatives)

We calculate how much the error would change if we tweaked `w` or `b`. These are our **gradients**:

$$
\frac{\partial}{\partial w} = -\frac{2}{n} \sum x_i (y_i - \hat{y}_i)
$$

$$
\frac{\partial}{\partial b} = -\frac{2}{n} \sum (y_i - \hat{y}_i)
$$

📐 These tell us the slope of the error function with respect to `w` and `b`.

---

### 3️⃣ Update Parameters 🔁

We update our parameters in the **opposite direction** of the gradient (because we want to minimize):

$$
w := w - \alpha \cdot \frac{\partial}{\partial w}
$$

$$
b := b - \alpha \cdot \frac{\partial}{\partial b}
$$

Here, **`α` (alpha)** is the **learning rate** 🧠—a small step we take toward the optimal value.

---

### 4️⃣ Repeat Until Convergence 🔁

Loop through steps 2 and 3 until:

* The changes in loss become tiny 🧘‍♂️
* Or you reach a fixed number of iterations

---

## 🔍 Visual Intuition

Imagine you're on a hill ⛰️ (the loss function), and you want to get to the lowest point (minimum error). Each gradient step is like walking downhill—step by step—towards the bottom.

---

## ✅ Summary

| Step | Description            | Emoji |
| ---- | ---------------------- | ----- |
| 1️⃣  | Initialize `w` and `b` | 🛠️   |
| 2️⃣  | Calculate predictions  | 📈    |
| 3️⃣  | Compute loss (MSE)     | ⚖️    |
| 4️⃣  | Compute gradients      | 🧮    |
| 5️⃣  | Update parameters      | 🔁    |
| 🔁   | Repeat until done      | ⏳     |


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
