parent:: [[regression]], [[regularization]], [[Linear Models]]

- brief description

Lasso regression is linear regression where the [[cost function]] (usually [[Least Squares]]) has an L1 [[Norm of a vector|norm]] added. It penalizes poorly performing features by aggressively pushing their weights to zero.

- formula

*cost function:*

$$
J(\theta) = MSE(\theta) + \alpha\sum_{i=1}^n|\theta_i|
$$

- draw it

[https://app.diagrams.net/#](https://app.diagrams.net/#)

- when should this be used?

Lasso should be used when you have too many features, colinear features, or if you just generally suspect that some of your features are not helpful. Lasso will help to make your model more sparse and more generalizable. 

- advantages
- disadvantages