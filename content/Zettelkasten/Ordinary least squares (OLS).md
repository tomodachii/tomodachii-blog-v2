---
tags:
  - statistical-learning
  - regression-analysis
  - linear-algebra
  - statistics
date_created: 2026-04-14 16:13
status: concept
aliases: []
---

# Definition
A method for choosing the unknown parameters in a [[Linear regression]] model by the principle of *least squares* (minizing the *residual sum of squares*).
$$
\hat{\beta} = \arg \min_\beta \text{RSS}(\beta)
$$
# Intuition
OLS = MLE + Gaussian noise assumption.
# Setting
Given an input vector $X^\top = (X_1, X_2, \dots, X_p)$. The *linear regression* model:
$$
f(X) = \beta_0 + \sum_{j = 1}^p X_j \beta_j
$$
In a machine learning, we often subsume the $\beta_0$ by using a full one column in the design matrix $\mathbf{X}$ [@zhangDiveDeepLearning2024]:
$$
\mathbf{y} = \mathbf{X}^\top \beta
$$
with
$$
\mathbf{X} = \begin{bmatrix}  
1 & x_{11} & \cdots & x_{1p} \\  
1 & x_{21} & \cdots & x_{2p} \\  
\vdots & \vdots & \ddots & \vdots \\  
1 & x_{N1} & \cdots & x_{Np}  
\end{bmatrix}  
\in \mathbb{R}^{N \times (p+1)}, \quad

\mathbf{y} =  
\begin{bmatrix}  
y_1 \\  
y_2 \\  
\vdots \\  
y_N  
\end{bmatrix}  
\in \mathbb{R}^{N}, \quad

\beta =  
\begin{bmatrix}  
\beta_0 \\  
\beta_1 \\  
\vdots \\  
\beta_p  
\end{bmatrix}  
\in \mathbb{R}^{p+1}
$$
# Estimation
Assume
- [[Linear regression]] model.
- Loss function: the residual sum of squares as the measure of the overall model fit:
$$
\text{RSS}(\beta) = \sum_i^n (y_i - x_i^\top b)^2 = (\mathbf{y} - \mathbf{X}\beta)^\top (\mathbf{y} - \mathbf{X} \beta)
$$
The value of $\beta$ which minimizes this sum is called the **OLS estimator for** $\beta$
$$
\hat{\beta} = \arg \min_\beta \text{RSS}(\beta)
$$
This RSS is a quadratic function in the $p + 1$ parameters. Differentiating w.r.t. $\beta$, we obtain:
$$
\begin{align*}
\frac{\partial \text{RSS}}{\partial \beta} &= -2 \mathbf{X}^\top (\mathbf{y} - \mathbf{X} \beta)\\
\frac{\partial^2 \text{RSS}}{\partial \beta \partial \beta^\top} &= 2 \mathbf{X}^\top \mathbf{X}
\end{align*}
$$
Assuming that $\mathbf{X}$ has full column rank, and hence $\mathbf{X}^\top \mathbf{X}$ is Positive definite
Set the first derivative to zero
$$
\mathbf{X}^\top (\mathbf{y} - \mathbf{X} \beta) = 0
$$
to obtain the unique solution:
$$
\hat{\beta} = (\mathbf{X}^\top \mathbf{X})^{-1} \mathbf{X}^\top \mathbf{y}
$$
# Prediction
The predicted values at an input vector $x_0$ are given by:
$$
\hat{f}(x_0) = (1, x_0)^\top \hat{\beta}
$$
- $(1, x_0)$: Augmented vector.
The fitted values (optimal point estimator) at all the training inputs are:
$$
\hat{\mathbf{y}} = \mathbf{X} \hat\beta = \mathbf{X} (\mathbf{X}^\top \mathbf{X})^{-1} \mathbf{X}^\top \mathbf{y}
$$
- $\hat{y}_i = \hat{f}(x_i)$.
- $\mathbf{H} = \mathbf{X}(\mathbf{X}^\top \mathbf{X})^{-1} \mathbf{X}^\top$: The "hat" matrix (because it puts the hat on $\mathbf{y}$), the projection matrix.

//TODO: Gauss-Markov theorem
# Geometric interpretation
The columns of $\mathbf{X}$: $\mathbf{x}_0, \mathbf{x}_1, \dots, \mathbf{x}_p$ span a subspace of $\mathbb{R}^N$ (the column space of $\mathbf{X}$) with $\mathbf{x}_0 \equiv 1$; for simplicity, assume they span a plane (2D).
![[linear-regression-least-sq-othorgonal_annotated.png]]
The goal of OLS is to minimize the RSS
$$
RSS(\beta) = \lVert \mathbf{y} - \mathbf{X} \beta \rVert^2
$$
The unique vector within the column space of $\mathbf{X}$ that minimizes this distance is the orthogonal projection of $y$ onto that space. Geometrically, this means
$$
(\mathbf{y} - \hat{\mathbf{y}}) \perp \text{Column space } (\mathbf{X})
$$
This leads to the normal equation
$$
\mathbf{X}^\top (\mathbf{y} - \mathbf{X} \beta) = 0
$$
# Properties of least-squares estimators
Assumptions: uncorrelated and constant variance $\sigma^2$ of the observations $y_i$.
The variance-covariance matrix of the least squares parameter estimates:
$$
\text{Var} (\hat{\beta}) = (\mathbf{X}^\top \mathbf{X})^{-1} \sigma^2
$$
Unknown variance $\sigma^2$ can be estimated by:
$$
\hat{\sigma}^2 = \frac{1}{N - p - 1} \sum_{i = 1}^N (y_i - \hat{y}_i)^2
$$
# Related Concepts
[[Linear regression]]
# References

