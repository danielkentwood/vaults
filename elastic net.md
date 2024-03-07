# elastic net

Tags: [[regularization]]



Elastic net is a middle ground between lasso and ridge regression. The regularization term is a mix between [[L1 (Lasso) regularization]] and [[L2 (Ridge) regularization]], and you can control the mix ratio $r$. When $r=0$, Elastic net is equivalent to ridge regression. When $r=1$, it is equivalent to lasso regression.

- formula

$$
J(\theta) = MSE(\theta)+r\alpha\sum_{i=1}^n|\theta_i|+\frac{1-r}{2}\alpha\sum_{i=1}^n\theta_i^2
$$
