# Determinant of a matrix

related:: [[linear algebra]]

- brief description
    
    A determinant is a scalar value that encodes properties of the linear transformation described by the matrix. 
    
    Geometrically, it is the *volume scaling factor* of the linear transformation described by the matrix. 
    
- formula
    
    For a 2x2 matrix:
    
    $$
    |A|= \begin{vmatrix} a & b\\ c & d\end{vmatrix} = ad-bc
    $$
    
    For a 3x3 matrix, you can do Laplace Expansion:
    
    $$
    |A|= \begin{vmatrix} a&b&c\\ d&e&f\\g&h&i \end{vmatrix} = a\begin{vmatrix} e&f\\h&i \end{vmatrix} - b\begin{vmatrix} d&f\\g&i \end{vmatrix} + c\begin{vmatrix} d&e\\g&h \end{vmatrix}
    $$