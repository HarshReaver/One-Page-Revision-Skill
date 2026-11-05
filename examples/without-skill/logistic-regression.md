# Logistic Regression: Revision Sheet

## What it is
- Supervised ML algorithm for **classification** (despite the name, not regression).
- Predicts the **probability** that an input belongs to a class (binary example: 0 or 1).
- Linear regression gives continuous values, so the sigmoid function squashes the linear output into the range 0 to 1 (S-shaped curve).

## Sigmoid function
- g(z) = 1 / (1 + e^(-z)), range (0, 1)
- g(z) -> 1 as z -> +inf; g(z) -> 0 as z -> -inf; g(z) = 0.5 at z = 0
- z = theta0 + theta1*x1 = theta^T x
- Hypothesis: h(x) = 1 / (1 + e^(-theta^T x)) = probability of class 1

## Cost function
- MSE on a sigmoid output is **non-convex**, so finding the minimum is hard.
- Use **Log Loss (Binary Cross Entropy)**:
  - Per sample: -log(y_hat) if y = 1; -log(1 - y_hat) if y = 0
  - Combined: -y log(y_hat) - (1 - y) log(1 - y_hat)
  - Whole dataset: J(theta) = -(1/m) * sum[ y log(y_hat) + (1 - y) log(1 - y_hat) ]
- Why: heavily penalises confident wrong predictions (y = 0, y_hat = 0.9 gives high loss; y_hat = 0.1 gives low loss).
- It is **convex**, so a global minimum is guaranteed.

## Gradient descent
1. Initialise parameters (theta0, theta1, ...)
2. Predict using the model
3. Compute gradients
4. Update parameters
5. Repeat steps 2 to 4 until convergence

Gradients (same form as linear regression):
- dJ/dtheta1 = (1/m) * (y_hat - y) * x
- dJ/dtheta0 = (1/m) * (y_hat - y)

Derivation (chain rule): dJ/dtheta = dJ/dy_hat * dy_hat/dz * dz/dtheta
- dJ/dy_hat = -(1/m)(y/y_hat - (1 - y)/(1 - y_hat))
- dy_hat/dz = y_hat(1 - y_hat)
- dz/dtheta1 = x; dz/dtheta0 = 1

## Types
| Type | Output | Example |
|---|---|---|
| Binomial | 2 categories | Yes/No, Pass/Fail |
| Multinomial | 3+ unordered categories | cat, dog, rabbit |
| Ordinal | 3+ ordered categories | low, medium, high |

## Assumptions
1. Independent observations (no correlation between samples)
2. Binary dependent variable (for more than 2 classes, use Softmax)
3. Linear relationship between predictors and **log odds**
4. No extreme outliers
5. Large sample size

## Quick recall
- Sigmoid gives probability; log loss is the cost; gradient descent optimises.
- Log loss over MSE because it is convex and punishes confident mistakes.
- Gradient simplifies to (y_hat - y) * x.
