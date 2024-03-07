

 L2 (Ridge or Tikhonov) regularization is a method of penalizing a linear model by adding the L2 [[Norm of a vector|norm]] to the [[cost function]]. It penalizes poorly performing features by gradually pushing their weights lower.  

You can use the $L2$ norm to find the [[Euclidean Distance]] between two vectors. 

$$
d(\vec{v},\vec{w})=\sqrt{\sum_{i=1}^n(v_i-w_i)^2}
$$

CODE for euclidian distance:

```python
# create numpy vectors v and w
v = np.array([1, 6, 8])
w = np.array([0, 4, 6])

# Calculate the Euclidean distance d
d = np.linalg.norm(v-w)
```

In the context of [[regression]], L2 regression has the following *cost function*:

$J(\theta)=MSE(\theta) + \alpha\frac{1}{2}\sum_{i=1}^n\theta_i^2$

with this *closed-form solution:*

$\hat{\theta}=(X^TX+\alpha A)^{-1} \ X^T \ y$

