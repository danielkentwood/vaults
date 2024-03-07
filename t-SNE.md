# t-SNE

Tags: [[dimensionality reduction]]

(1) The gaussian probability of observing distances between any two points (that satisfy the symmetry rule) in high-dimensional space:

$$
p_{j|i}=\frac{exp \Big(-\|x_i-x_j\|^2/2\sigma_i^2 \Big)}{\sum_{k\ne i}exp \Big(-\|x_i-x_k\|^2/2\sigma_i^2 \Big)}, \quad p_{ij}=\frac{p_{i|j}+p_{j|i}}{2N}
$$

(2) Perplexity determines optimal $\sigma$ for each sample:

$$
Perplexity = 2^{-\sum_jp_{j|i}\ log_2\ p_{j|i}}
$$

(3) The [[Student t-distribution]] for the distances between the pairs of points in the low-dimensional embedding:

$$
q_{ij}=\frac{(1+\|y_i-y_j\|^2)^{-1}}{\sum_{k\ne l}(1+\|y_k-y_l\|^2)^{-1}}
$$

(4) The [[Kullback-Leibler divergence]] loss function to project the high-dimensional probability onto the low-dimensional probability, as well as the analytical form of the gradient to be used in the [[gradient descent]] optimization:

$$
KL(P_i\|Q_i)=\sum_i \sum_j p_{j|i} \ log \frac{p_{j|i}}{q_{j|i}}, \quad \frac{\delta KL}{\delta y_i}=4 \sum_j(p_{ij}-q_{ij})(y_i-y_j)(1+\|y_i-y_j\|^2)^{-1}
$$


### disadvantages
- tSNE doesn't scale well for rapidly increasing sample sizes (it has an initial step where it uses [[k-nearest neighbors]], which struggles with large sample sizes).
- it doesn't preserve global data structure. Only within-cluster distances are meaningful; between-cluster similarities are not guaranteed.
- it can only embed in 2 or 3 dimensions, i.e., only for visualization purposes. This makes it not a great candidate for working with high-dimensional data.
