# Huber loss

Huber Loss is a type of [[cost function]]

From HOML p. 293:

Huber loss is quadratic when the error is smaller than a threshold $\delta$ (typically 1) but linear when the error is larger than $\delta$. The linear part makes it less sensitive to outliers than the [[mean squared error (MSE)]], and the quadratic part allows it to converge faster and be more precise than the [[mean absolute error]].