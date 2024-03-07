# Cosine Similarity

Tags: [[distance metrics]], [[linear algebra]]

A measure of the distance between vectors in terms of the angle (specifically, the cosine of that angle) between them (rather than the euclidean distance between their endpoints)

For the cosine similarity between two vectors $\hat{v}$ and $\hat{w}$:

The dot product between the two vectors is equal to the product of their norms times $cos(\beta)$.

$$
\hat{v}\cdot\hat{w}=\|\hat{v}\|\ \|\hat{w}\|\ cos(\beta)
$$

Therefore, $cos(\beta)$ is equal to the dot product of the vectors over the product of their norms.

$$
cos(\beta)=\frac{\hat{v}\cdot\hat{w}}{\|\hat{v}\|\ \|\hat{w}\|}
$$


Unlike [[Euclidean Distance]], which scales with the difference between numbers of elements in the two vectors you are comparing, cosine similarity is robust to differences in the number of elements between the vectors. 
