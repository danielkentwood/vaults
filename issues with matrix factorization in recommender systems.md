
Here are some issues with [[matrix factorization]] in [[recommendation systems]]

* It will usually be a very sparse matrix
* We could train only on observed values, but then we would probably overfit
* We could impute the unobserved values, but this is computationally expensive and potentially dangerous because it might pollute the data
