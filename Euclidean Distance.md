# Euclidean Distance

parent:: [[distance metrics]]

Essentially, the length of a line segment between two points. It can be calculated using the [[pythagorean theorem]].

You can use the $L2$ norm to find the euclidean distance between two vectors. 

$$
d(\vec{v},\vec{w})=\sqrt{\sum_{i=1}^n(v_i-w_i)^2}
$$

CODE:

```python
# create numpy vectors v and w
v = np.array([1, 6, 8])
w = np.array([0, 4, 6])

# Calculate the Euclidean distance d
d = np.linalg.norm(v-w)
```

**Formula for $L2$ (Euclidean) norm, where $p=2$:**

$$
\|\vec{a}\|_2=\sqrt{\sum_{i=1}^na_i^2}
$$

Note that it is equivalent to the pythagorean theorem.

Also note that it is the square root of the dot product of the vector with itself. In other words:

$$
\|\vec{a}\|_2=\sqrt{\sum_{i=1}^na_i^2}=\sqrt{\vec{a} \cdot \vec{a}}
$$

- disadvantages

Euclidean Distance is unhelpful in high dimensions because all vectors are almost equidistant to the search query vector. You need to do dimensionality reduction first.