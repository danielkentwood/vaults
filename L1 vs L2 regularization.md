# L1 vs L2 regularization

Tags: [[L1 (Lasso) regularization]], [[L2 (Ridge) regularization]]

## Question:

What is L1 and L2 regularization? What are the differences between the two?

## Answer/Discussion:

L1 and L2 regularization are methods for avoiding overfitting in machine learning. During gradient descent, the regularization terms will add an extra penalty for weights that For a typical regression model, assume that there is a loss function $L$:

$$
\begin{aligned} Loss(L_1)=L+\lambda|w_i| \\ Loss(L_2)=L+\lambda|w_i^2| \end{aligned}
$$

Where the loss function $L$ is the sum of errors squared:

$$
L=\sum_{i=1}^n(y_i-f(x_i))^2=\sum_{i=1}^n(y_i-\sum_{j=1}^p(x_{ij}w_j))^2
$$

Regression with L1 regularization is often called Lasso regression. During gradient descent, it will often force any weight closer to 0, irrespective of magnitude. Therefore, smaller weights often get completely zeroed and dropped from the model with L1. 

Regression with L2 regularization (or Tikhonov regularization) is often called Ridge regression. During gradient descent, it will bring weights closer to zero, but the rate that it does so is proportional to the weight itself.