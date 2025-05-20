# Class Evaluation

```
import numpy as np
np.set_printoptions(precision=6, formatter={'all': lambda x: f'{x:f}'})
```

## Task

**a + 2b + 3c + 4d + 5e = 55**
**- a + 3c + 5e = 33 - 2b - 4d**
**5e + 3c - 44 = -4b + a - 4d**
**- 3c + 5e - 22 = a -4d - 4b**
**3b - a = 11 - 2d**

**Find the solution of the above system of equations using the Gauss Elimination method. Generate and print :**
**1. The augmented matrix (a 2D numpy array).
2. The row multipliers (a 2D numpy array).
3. The resulting upper triangular matrix (a 2D numpy array).
4. The solutions (a 1D numpy array).**

```
def get_result_gaussian_elimination(n, A_aug):
    A = A_aug.copy()
    x = np.zeros(n)
    row_multipliers = np.zeros((n, n))

    # Check for singular matrix
    coeff = A[:, :-1]
    if np.abs(np.linalg.det(coeff)) < 1e-10:
        return None

    # Forward elimination
    for i in range(n):
        # Pivoting
        max_row = np.argmax(np.abs(A[i:, i])) + i
        if i != max_row:
            A[[i, max_row]] = A[[max_row, i]]

        for j in range(i+1, n):
            if A[i][i] == 0:
                continue
            multiplier = A[j][i] / A[i][i]
            row_multipliers[j][i] = multiplier
            A[j] = A[j] - multiplier * A[i]

    # Back substitution
    for i in range(n-1, -1, -1):
        x[i] = A[i][-1] - np.sum(A[i][i+1:n] * x[i+1:n])
        x[i] /= A[i][i]

    return A, row_multipliers, x

# augmented matrix
A = np.array([
    [1,  2,  3,  4,  5],
    [-1, 2, 3, 4, 5],
    [-1,  4, 3, 4, 5],
    [-1, 4, -3, 4, 5],
    [-1, 3, 0, 2, 0]
], dtype=np.double)

b = np.array([55, 33, 44, 22, 11], dtype=np.double)

# 1. Augmented Matrix
augmented_matrix = np.hstack((A, b.reshape(-1, 1)))
print("1. Augmented Matrix:")
print(augmented_matrix)

n = 5
upper_triangular_matrix, row_multipliers, solution = get_result_gaussian_elimination(n, augmented_matrix)

print("\n2. Row Multipliers:")
print(row_multipliers)

print("\n3. Upper Triangular Matrix:")
print(upper_triangular_matrix)

print("\n4. Solution [a, b, c, d, e]:")
print(solution)
```

```
Output:
1. Augmented Matrix:
[[1.000000 2.000000 3.000000 4.000000 5.000000 55.000000]
 [-1.000000 2.000000 3.000000 4.000000 5.000000 33.000000]
 [-1.000000 4.000000 3.000000 4.000000 5.000000 44.000000]
 [-1.000000 4.000000 -3.000000 4.000000 5.000000 22.000000]
 [-1.000000 3.000000 0.000000 2.000000 0.000000 11.000000]]

2. Row Multipliers:
[[0.000000 0.000000 0.000000 0.000000 0.000000]
 [-1.000000 0.000000 0.000000 0.000000 0.000000]
 [-1.000000 0.666667 0.000000 0.000000 0.000000]
 [-1.000000 1.000000 -0.333333 0.000000 0.000000]
 [-1.000000 0.833333 0.333333 -0.250000 0.000000]]

3. Upper Triangular Matrix:
[[1.000000 2.000000 3.000000 4.000000 5.000000 55.000000]
 [0.000000 6.000000 6.000000 8.000000 10.000000 99.000000]
 [0.000000 0.000000 -6.000000 0.000000 0.000000 -22.000000]
 [0.000000 0.000000 0.000000 2.666667 3.333333 14.666667]
 [0.000000 0.000000 0.000000 -0.000000 -2.500000 -5.500000]]

4. Solution [a, b, c, d, e]:
[11.000000 5.500000 3.666667 2.750000 2.200000]
```
