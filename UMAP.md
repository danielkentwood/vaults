# UMAP

Tags: [[dimensionality reduction]]



(1) UMAP uses exponential probability distribution in high dimensions; the probabilities are not normalized:

$$
p_{i|j}=e^{-\frac{d(x_i,x_j)-\rho_i}{\sigma_i}}
$$

where $\rho$ represents the distance from each i-th data point to its first nearest neighbor. This ensures the local connectivity of the manifold. It gives a locally adaptive exponential kernel for each data point, so the distance metric varies from point to point.

(2) The number of nearest neighbors $k$:

$$
k=2^{\sum_ip_{ij}}
$$

(3) Symmetrization of high-dimensional probability:

$$
p_{ij}=p_{i|j}+p_{j|i}-p_{i|j}p_{j|i}
$$

After UMAP joins points with locally varying metrics (via $\rho$), the weight of the graph between A and B nodes is not equal to the weight between B and A nodes. This makes symmetrization necessary.

