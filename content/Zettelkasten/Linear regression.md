---
tags:
  - statistics
  - statistical-learning
  - machine-learning
  - linear-algebra
date_created: 2026-05-05 23:13
status: concept
---

# Definition
Given an input vector $X^\top = (X_1, X_2, \dots, X_p)$. The *linear regression* model:
$$
f(X) = \beta_0 + \sum_{j = 1}^p X_j \beta_j
$$
# Setting
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
# Intuition
The linear model either assumes that the regression function $E[Y \mid X]$ is linear or the linear model is a reasonable approximation [@hastieElementsStatisticalLearning2009].

The variables $X_j$ can come from different sources:
- quantitative inputs;
- transformations, e.g. $X_2 = X_1^2, X_3 = X_1^3 \to$ polynomial representation;
- numeric / "dummy" coding (e.g. one-hot) of the categories of qualitative inputs;
- interactions between variables, e.g. $X_3 = X_1 \cdot X_2$.
No matter the source of the $X_j$, the model is linear in the parameters.
# Estimating the coefficients
Given a training dataset
$$
\mathcal{D} = \{ (x_1, y_1), \dots, (x_n, y_n) \} \in \mathbb{R}^p \times \mathcal{Y}
$$
- $x_i = (x_{i1}, \dots, x_{ip}) \in \mathbb{R}^p$: The $i$th ***observed value*** of $X$. 
- $y_i \in \mathcal{Y}$: The $i$th observed value of $Y$ (simplified to just 1 feature, e.g. $Y = Y_1$ only).
- $\mathcal{Y}$: The space of possible responses
	- Rergression: $\mathcal{Y} = \mathbb{R}$.
	- Classification: $\mathcal{Y} =$ A finite set of classes.
Goal: Find $\hat{\beta}$
$$
\hat{\beta} = \arg \min_\beta  \sum_{i = 1}^N \ell(y_i, f(x_i; \beta))
$$
- $\ell$: Loss function, e.g. For OLS: $\ell = (y_i - x_i^\top \beta)^2$.
## The Ordinary least squares (OLS) method
Assume i.i.d observations $(x_i, y_i)$, we have the *residual sum of squared* as our loss function:
$$
\begin{align*}
\text{RSS} (\beta) &= \sum_{i = 1}^N (y_i - f(x_i))^2\\
&=\sum_{i = 1}^N \left( y_i - \beta_0 - \sum_{j = 1}^p x_{ij}\beta_j \right)^2\\
&= \sum_{i = 1}^N (y_i - {\beta}_0 - {\beta}_1x_{i1} - \dots -{\beta}_p x_{ip})^2
\end{align*}
$$
The goal is to find the coefficients $\beta = (\beta_0, \dots, \beta_p)^\top$ that minimizes the loss function:
$$
\hat{\beta} = \arg \min_\beta \text{RSS}(\beta)
$$
### Analytical solution
Consider the machine learning setting above. Then, we can write the *residual sum of squared* as
$$
\text{RSS}(\beta) = \sum_i^n (y_i - x_i^\top b)^2 = (\mathbf{y} - \mathbf{X}\beta)^\top (\mathbf{y} - \mathbf{X} \beta)
$$
This is a quadratic function in the $p + 1$ parameters. Differentiating w.r.t. $\beta$, we obtain:
$$
\begin{align*}
\frac{\partial \text{RSS}}{\partial \beta} &= -2 \mathbf{X}^\top (\mathbf{y} - \mathbf{X} \beta)\\
\frac{\partial^2 \text{RSS}}{\partial \beta \partial \beta^\top} &= 2 \mathbf{X}^\top \mathbf{X}
\end{align*}
$$
Assuming that $\mathbf{X}$ has **full column rank**, and hence $\mathbf{X}^\top \mathbf{X}$ is **positive definite**.
Set the first derivative to zero
$$
\mathbf{X}^\top (\mathbf{y} - \mathbf{X} \beta) = 0
$$
to obtain the unique solution:
$$
\hat{\beta} = (\mathbf{X}^\top \mathbf{X})^{-1} \mathbf{X}^\top \mathbf{y}
$$

The non-full-rank case: It might happen that the columns of $\mathbf{X}$ are linearly dependent, e.g. two of the inputs might be perfectly correlated ($\mathbf{x}_2 = 3 \mathbf{x}_1$).
Then $\mathbf{X}^\top \mathbf{X}$ is singular $\Rightarrow \hat{\beta}$ are not uniquely defined //TODO

However, the fitted values $\hat{\mathbf{y}} = \mathbf{X} \hat{\beta}$ are still the projection of $\mathbf{y}$ onto the column space of $\mathbf{X}$ but there are more than one way to express that projection in terms of the column vectors of $\mathbf{X}$.

The non-full-rank case occurs most often when one or more qualitative inputs are coded in a redundant fashion $\Rightarrow$ Resolve the non-unique representation, by recoding and/or dropping redundant columns in $\mathbf{X}$ [@hastieElementsStatisticalLearning2009].
### Gradient descent
//TODO
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
# Inference
//TODO

---
# References
[^ref]