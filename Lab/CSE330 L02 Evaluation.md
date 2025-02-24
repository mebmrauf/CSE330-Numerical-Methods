# Class Evaluation

```
import numpy as np
```

```
'''
Here we implement a Polynomial class with three methods: the constructor
__init__(), the toString method __repr__(), and a method to make the objects
of the class callable, __call__() method
'''

# Polynomial Class

class Polynomial:
  # Constructor, note that it starts and ends with two underscores
  def __init__(self, coeff):
    '''
    Every internal variable of the object must be saved and initialized
    in this method: self.variable = value
    '''
    self.coeff = coeff
    self.degree = len(coeff) - 1

  # Constructor to make the object callable
  def __call__(self, x_arr):
    '''
    Here we assumed x_arr is a numpy array. Remember that a numpy array acts
    like a vector (1D matrix). So an operation x + 1 would add 1 to each element
    of the matrix (unlike python's defaule list). Simlarly, x ** 2 would return
    element wise square of the array.

    Hence, this method would return an array, where the i'th element is the
    (polynomial) interpolated value of x[i], given the coeffecients a[i].
    '''
    p_x_arr = []
    # --------------------------------------------
    # HINT: Should look like
    # for i in range(self.degree + 1):
    #     ????
    # --------------------------------------------

    # remember 1: length = degree + 1 for a polynomial
    # remember 2: range(0, a) is same as range(a)
    # remember 3: range(a, b) means a is inclusive, b is exclusive

    # --------------------------------------------
    # YOUR CODE HERE
    temp = []
    for c in range(self.degree+1):
        temp.append(self.coeff[c]*(x_arr**c))
    p_x_arr = np.sum(temp, axis=0)

    # p_x_arr = [int(x) for x in p_x_arr]

    return p_x_arr
    # --------------------------------------------

  # String representation method of the object (similar to toString() of java)
  def __repr__(self):
    # remember: a formatted string must start with f.

    str_ret = f'Polynomial of degree {self.degree}\np(x) = '
    for i in range(self.degree + 1):
        a_val = self.coeff[i]
        if i != 0:
            if a_val >= 0:
                str_ret += f'+ {a_val}x^{i} '
            else:
                str_ret += f'- {-a_val}x^{i} '
        else:
            str_ret += f'{a_val}x^{i} '

    return str_ret

  # custom method 1: to get the degree of the polynomial
  def get_degree(self):
    # --------------------------------------------
    # YOUR CODE HERE
    return self.degree
    # --------------------------------------------

  # custom method 2: to get the coefficients of the polynomial
  def get_coeffs(self):
    # --------------------------------------------
    # YOUR CODE HERE
    return self.coeff
    # --------------------------------------------
```


```
'''
Here we implement a function which takes a discrete x and y array, and returns
a Polynomial object (the one we just implemented). This polynomial object can
be used to calculate y for any other value of x (not in that list) within the
range
'''
def get_poly(data_x, data_y):
    n_nodes = len(data_x)
    # np.zeors((a, b)) returns a (a x b) matrix, i.e., a rows and b columns
    X = np.zeros((n_nodes, n_nodes)) #6*6



    # Populate the X matrix with appropriate values
    # YOUR CODE HERE
    for i in range(n_nodes):
        for j in range(n_nodes):
            X[i][j] = data_x[i]**j

    print(X)

    # --------------------------------------------
    # np.linalg.inv is used to find the inverse
    # but pinv is more efficient
    X_inv = np.linalg.pinv(X) # pseudo inverse  #a = inv(X)*y
    a = np.dot(X_inv, data_y)
    p = Polynomial(a)

    return p
```


## Task 01

**Suppose, you have three nodes (-0.75, 1.87), (0.5, 2.20), (1.5, 2.44). Using Vandermonde Matrix method, find and print the value of the interpolating ploynoial at x = 3. You have to solve the given problem using above implemented get_poly() method.**

```
data_x = np.array([-0.75, 0.5, 1.5])
data_y = np.array([1.87, 2.20, 2.44])
p = get_poly(data_x, data_y)

print('\nValue of the interpolating ploynoial at x = 3:')
print(p(3))
```

```
[[ 1.     -0.75    0.5625]
 [ 1.      0.5     0.25  ]
 [ 1.      1.5     2.25  ]]

Value of the interpolating ploynoial at x = 3:
2.7599999999999953
```

## Task 02

**Suppose, you have five nodes (-1.2, 2.15), (0.8, 3.45), (1.9, 4.12), (-0.5, 1.75), and (2.3, 5.05). Using Vandermonde Matrix method, find and print the value of the interpolating ploynoial at x = 6. You have to solve the given problem using above implemented get_poly() method.**

```
data_x = np.array([-1.2, 0.8, 1.9, -0.5, 2.3])
data_y = np.array([2.15, 3.45, 4.12, 1.75, 5.05])
p = get_poly(data_x, data_y)

print('\nValue of the interpolating ploynoial at x = 6:')
print(p(6))
```

```
Output:

[[ 1.     -1.2     1.44   -1.728   2.0736]
 [ 1.      0.8     0.64    0.512   0.4096]
 [ 1.      1.9     3.61    6.859  13.0321]
 [ 1.     -0.5     0.25   -0.125   0.0625]
 [ 1.      2.3     5.29   12.167  27.9841]]

Value of the interpolating ploynoial at x = 6:
204.67406786761623
```