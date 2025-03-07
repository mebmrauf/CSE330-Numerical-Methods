# Class Evaluation

```
import numpy as np
```

```
class Lagrange_Polynomial:
    def __init__(self, data_x, data_y):
        '''
        First we need to check whether the input vectors (numpy arrays) are equal
        or not.
        assert (condition), "msg"
        this command checks if the condition is true or false. If true, the code
        runs normally. But if false, then the code returns an error message "msg"
        and stops execution
        '''
        assert len(data_x) == len(data_y), "length of data_x and data_y must be equal"
        '''
        Lagrange polynomials do not use coefficeints a_i, rather the nodes
        (x_i, y_i). Hence, we just need to store these inside the object
        '''
        self.data_x = data_x
        self.data_y = data_y
        self.degree = len(data_x) - 1
        # we assume that the inputs are numpy array, so we can perform
        # element wise operations

    def __repr__(self):
        # method for string representation
        # you don't need to worry about the following code if you don't understand
        strL = f"LagrangePolynomial of order {self.degree}\n"
        strL += "p(x) = "
        for i in range(len(self.data_y)):
            if self.data_y[i] == 0:
                continue
            elif self.data_y[i] >= 0:
                strL += f"+ {self.data_y[i]}*l_{i}(x) "
            else:
                strL += f"- {-self.data_y[i]}*l_{i}(x) "
        return strL

    def l(self, k, x):
        l_k = 1.0 # Initialization
        # --------------------------------------------
        # YOUR CODE HERE
        x_k = self.data_x[k]
        for j in range(len(self.data_x)):
            if j != k:
                x_j = self.data_x[j]
                l_k *= (x-x_j)/(x_k-x_j)
        return l_k

    def __call__(self, x_arr): #[5, 10, 44, 99, 77]
        # initialize with zero
        p_x_arr  = np.zeros(len(x_arr))
        # --------------------------------------------
        # YOUR CODE HERE
        for k, f_x in enumerate(self.data_y):
            p_x_arr += f_x * self.l(k, x_arr)
        return p_x_arr
```

## Task
**Suppose you have a funnction f(x) = 5x and three nodes (3,4), (5,7), (7,10). Using Lagrange bassis, print out the value of the interpolating polynomial at x = -3.5. Also, display the actual interpolation error at x = -3.5.**

**Hint: Interpolation error = |f(-3.5) - p(-3.5)| where p is the interpolating polynommial.**

```
data_x = np.array([3, 5, 7])
data_y = np.array([4, 7, 10])

p = Lagrange_Polynomial(data_x, data_y)
print(p)

p_x = p([-3.5])
print("\nValue of interpolating polynomial")
print(p_x)

f_x = 5*(-3.5)
error = abs(f_x - p_x)
print("\nInterpolating error")
print(error)
```

```
Output:

LagrangePolynomial of order 2
p(x) = + 4*l_0(x) + 7*l_1(x) + 10*l_2(x) 

Value of interpolating polynomial
[-5.75]

Interpolating error
[11.75]
```