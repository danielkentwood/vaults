# Inverse of a matrix
related:: [[linear algebra]]

- brief description
    
    The inverse of matrix $A$ is the matrix $A^{-1}$ such that $A^{-1}A=I$, where $I$ is the identity matrix.
    
    - They only exist for square matrices.
    - Not every square matrix is invertible; sometimes they are singular (i.e., when the determinant is zero)
- why is the matrix inverse useful?
    
    You can use the inverse to solve a system of linear equations. For example, if you have a system in matrix form as AX = B, you can multiply both sides by the inverse of A, giving you $X=A^{-1}B$
    
- how do you find the inverse?
    - gauss-jordan (row operations)
        1. Create an augmented matrix by placing the identity matrix alongside matrix A.
            
            ![Inverse%20of%20a%20matrix%20ab7d0b1e9dc5437da558e7d274f81da8/Untitled.png](Untitled%2018.png)
            
        2. Creatively perform row operations in order to transform A into the identity matrix. Whatever you do to row i in matrix A, you also have to do to row i in matrix I. You can use other rows (subtract, add, multiply, divide, swap) or you can perform operations on a single row. For example:
            
            ![Inverse%20of%20a%20matrix%20ab7d0b1e9dc5437da558e7d274f81da8/Untitled%201.png](Untitled%201%206.png)
            
        3. Matrix A is now the identity matrix, and matrix I is now the inverse of A. 
    - minors, cofactors, and adjugate
        
        Suppose we have matrix A:
        
        ![Inverse%20of%20a%20matrix%20ab7d0b1e9dc5437da558e7d274f81da8/Untitled%202.png](Untitled%202%201.png)
        
        1. **From matrix A, create a Matrix of Minors.** 
            
            For each element in the matrix:
            
            1. ignore values on the current row and column
            2. calculate the determinant of the remaining values
            3. put those determinants into a matrix
            
            ![Inverse%20of%20a%20matrix%20ab7d0b1e9dc5437da558e7d274f81da8/Untitled%203.png](Untitled%203%201.png)
            
        2. **Matrix of cofactors**
            
            ![Inverse%20of%20a%20matrix%20ab7d0b1e9dc5437da558e7d274f81da8/Untitled%204.png](Untitled%204%201.png)
            
        3. **Adjugate (also called adjoint)**
            
            Transpose all elements of the previous matrix (i.e., swap their positions over the diagonal, while the diagonal stays the same)
            
            ![Inverse%20of%20a%20matrix%20ab7d0b1e9dc5437da558e7d274f81da8/Untitled%205.png](Untitled%205%201.png)
            
        
        4. **Multiply by 1/determinant**
        
        1. Find the determinant of the original matrix. 
            - Shortcut: multiply each element in the top row by its cofactor.
            - Determinant of A = 3(2) + 0(-2) + x(2) = 10
        2. multiply the adjugate by 1/determinant
            
            ![Inverse%20of%20a%20matrix%20ab7d0b1e9dc5437da558e7d274f81da8/Untitled%206.png](Untitled%206%201.png)