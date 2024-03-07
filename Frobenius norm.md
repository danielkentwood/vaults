# Frobenius norm

related:: [[linear algebra]]

- brief description
    
    Frobenius norm is the $L_2$ norm for a matrix (i.e., when $p=2$ for both dimensions, which technically is $p=q=2$) . You essentially take the square root of the sum of every element squared.
    
- formula
    
    
    $$
    \|A\|_F=\sqrt{\sum_{i=1}^m\sum_{j=1}^n|a_{ij}|^2}
    $$
    
- implementation
    
    ```python
    a = np.array([[2,2],
    							[2,2]])
    
    a_frobenius = np.sqrt(np.sum(np.square(a))
    ```
    
- implementation from scratch
- when should this be used?
- advantages
- disadvantages