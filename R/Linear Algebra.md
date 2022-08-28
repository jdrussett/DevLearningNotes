# Linear Algebra

## General

---

- `%*%` does matrix multiplication
- `t()` takes the transpose of a matrix
- `solve()` finds the inverse of a matrix, if it exists
- Following commands can both be used to find Moore-Penrose pseudo-inverse:
  - `solve(t(matrix) %*% matrix) %*% t(matrix)`
  - `MASS::ginv(matrix)`
- `det()` finds the determinant of a matrix
- `eigen()` returns eigenvalues of a matrix
  - matrixcalc library also has some useful stuff for eigen stuff
  - Eigen objects have useful properties, like $values and $vectors
- `chol()` returns upper-rectangular matrix
- `pracma::rref()` finds row-reduced echelon form of a matrix
- `pracma::Diag()` generates a diagonal matrix or returns the diagonal of a matrix
- `svd()` returns singular value decomposition of a matrix
