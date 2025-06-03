Linear Regression is a **supervised learning algorithm** used for **predicting a continuous target variable** based on one or more input features.

---

## 📈 1. What is Linear Regression?

Linear Regression models the **relationship between a dependent variable yy** and one or more **independent variables xx** using a **linear equation**.

---

## 🧮 2. Hypothesis Function

For **Simple Linear Regression** (one feature):

h(x) = θ₀ + θ₁·x

For **Multiple Linear Regression** (multiple features):

h(x) = θ₀ + θ₁·x₁ + θ₂·x₂ + ... + θₙ·xₙ

Or, in vectorized form:

hθ(x)=θTxh_\theta(x) = \theta^T x

Where:

- θ\theta = parameters (weights)
    
- xx = input features
    
- hθ(x)h_\theta(x) = predicted output
    

---

## 🎯 3. Cost Function (Mean Squared Error)

The **cost function** measures how well our model is performing:

J(θ)=12m∑i=1m(hθ(x(i))−y(i))2J(\theta) = \frac{1}{2m} \sum_{i=1}^{m} \left( h_\theta(x^{(i)}) - y^{(i)} \right)^2

Where:

- mm = number of training examples
    
- y(i)y^{(i)} = actual value
    
- hθ(x(i))h_\theta(x^{(i)}) = predicted value
    

---

## 🔁 4. Gradient Descent Algorithm

Used to minimize the cost function J(θ)J(\theta):

θj:=θj−α∂J(θ)∂θj\theta_j := \theta_j - \alpha \frac{\partial J(\theta)}{\partial \theta_j}

For Linear Regression, the partial derivative becomes:

θj:=θj−α⋅1m∑i=1m(hθ(x(i))−y(i))xj(i)\theta_j := \theta_j - \alpha \cdot \frac{1}{m} \sum_{i=1}^{m} \left( h_\theta(x^{(i)}) - y^{(i)} \right) x_j^{(i)}

Repeat until convergence.

Where:

- α\alpha = learning rate
    

---

## 📐 5. Assumptions of Linear Regression

1. **Linearity**: Relationship between inputs and output is linear.
    
2. **Independence**: Observations are independent.
    
3. **Homoscedasticity**: Constant variance of errors.
    
4. **Normality**: Errors should be normally distributed.
    

---

## 🧪 6. Evaluation Metrics

- **Mean Absolute Error (MAE)**:
    

MAE=1m∑i=1m∣y(i)−y^(i)∣MAE = \frac{1}{m} \sum_{i=1}^{m} |y^{(i)} - \hat{y}^{(i)}|

- **Mean Squared Error (MSE)**:
    

MSE=1m∑i=1m(y(i)−y^(i))2MSE = \frac{1}{m} \sum_{i=1}^{m} (y^{(i)} - \hat{y}^{(i)})^2

- **Root Mean Squared Error (RMSE)**:
    

RMSE=MSERMSE = \sqrt{MSE}

- **R-squared (Coefficient of Determination)**:
    

R2=1−∑(yi−y^i)2∑(yi−yˉ)2R^2 = 1 - \frac{\sum (y_i - \hat{y}_i)^2}{\sum (y_i - \bar{y})^2}

---

## 🧰 7. Implementation (Python Example)

```python
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error, r2_score

# Load your dataset
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# Create model
model = LinearRegression()

# Train
model.fit(X_train, y_train)

# Predict
y_pred = model.predict(X_test)

# Evaluate
mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)
```

---

## 🔚 Conclusion

Linear Regression is a powerful and interpretable model for regression tasks, especially when the relationship between features and the target is linear. For non-linear problems, consider polynomial regression or more complex models.

---

Let me know if you want this formatted specifically for a Jupyter notebook, GitHub README, or another platform.