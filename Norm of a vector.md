# Norm of a vector
related:: [[linear algebra]]

- brief description
    
    A norm is a way of characterizing the magnitude of a vector.
    
- formula
    
    **Formula for generalized p-norm:**
    
    $$
    \|\vec{a}\|_p=\bigg(\sum_{i=1}^n |\vec{a}_i|^p\bigg)^{1/p}
    $$
    
    Note that when $p=0$, the $L0$ norm is equal to the number of elements in the vector (since anything to the power of 0 is equal to 1 and you're summing all of the elements raised to the power of 0)
    
    **Formula for $L1$ (taxicab) norm, where $p=1$:**
    
    $$
    \|\vec{a}\|_1=\sum_{i=1}^n |\vec{a}_i|
    $$
    
    Note that it is the sum of the absolute values of the elements of $\vec{a}$.
    
    **Formula for $L2$ (Euclidean) norm, where $p=2$:**
    
    $$
    \|\vec{a}\|_2=\sqrt{\sum_{i=1}^na_i^2}
    $$
    
    Note that it is equivalent to the [[pythagorean theorem]].
    
    Also note that it is the square root of the dot product of the vector with itself. In other words:
    
    $$
    \|\vec{a}\|_2=\sqrt{\sum_{i=1}^na_i^2}=\sqrt{\vec{a} \cdot \vec{a}}
    $$
    
- draw it
    
    [https://app.diagrams.net/#](https://app.diagrams.net/#)
    
- implementation
    
    ```python
    nparray1 = np.array([1, 2, 3, 4]) # Define an array
    norm1 = np.linalg.norm(nparray1)
    ```
    
- when should this be used?
    
    You can use a norm to regularize a [[cost function]]. For example:
    
    - [[L1 (Lasso) regularization]] for lasso regression
    - [[L2 (Ridge) regularization]] for ridge or Tikhonov regression
    
    You can use the $L2$ norm to find the [[Euclidean Distance]] between two vectors. 
    
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
    
- Some links:
    - [https://hadrienj.github.io/posts/Deep-Learning-Book-Series-2.5-Norms/](https://hadrienj.github.io/posts/Deep-Learning-Book-Series-2.5-Norms/)