# Class Evaluation

```
import numpy as np
import math
```

```
# basic rule for calculating the difference, implanted in the lambda function.
# You may use it if you wish
difference = lambda y2, y1, x2, x1: (y2-y1)/(x2-x1)

def calc_div_diff(x,y):
    assert(len(x)==len(y))
    #write this function to calculate all the divided differences in the list 'b'
    n = len(x)
    coef = np.zeros((n,n))  #initializing
    #----------------------------------------------
    # YOUR CODE HERE
    coef[:, 0] = y
    for i in range(1, n):
        for j in range(n - i):
            coef[j, i] = difference(coef[j + 1, i - 1], coef[j, i - 1], x[j + i], x[j])

    #----------------------------------------------

    return coef[0]
```

```
class Newtons_Divided_Differences:

    def __init__(self, differences, data_x):
        self.differences = differences
        self.data_x = data_x

    def n(self, k, x):
        result = 1
        #----------------------------------------------
        # YOUR CODE HERE
        for i in range(k):
            result *= (x - self.data_x[i])
        #----------------------------------------------
        
        return result

    def __call__(self, x):
        '''
        this function is for calculating y from given x using all the difference coefficients
        x can be a single value or a numpy
        the formula being used:
        f(x) = f [x0] + (x-x0) f[x0,x1] + (x-x0) (x-x1) f[x0,x1,x2] + . . . + (x-x0) (x-x1) . . . (x-xk-1) f[x0, x1, . . ., xk]

        work on this after implementing 'calc_div_diff'. Then you should have
        f[x0], f[x0,x1]. . . . . ., f[x0, x1, . . ., xk] stored in self.differences

        'res' variable must return all the results (corresponding y for x)
        '''

        res = np.zeros(len(x)) #Initialization to avoid runtime error. You can change this line if you wish

        #----------------------------------------------
        # YOUR CODE HERE
        for i in range(len(self.differences)):
            res+= self.differences[i] * self.n(i,x)
        #----------------------------------------------

        return res
```

## Task

**Suppose, the given original function is sin(x) [f(x) = sin(x)]. Now, the given nodes are -π/2, 0, π/2. Calculate the value of the interpolating polynomial at x = π/4 and show the truncation error.**

**To get the value of π you can import the math library and just type in math.pi to get values of sin(x) function at any given point of x, just type math.sin(x)**

```
data_x = np.array([-(math.pi/2), 0, math.pi/2])
data_y = np.array([math.sin(-(math.pi/2)), math.sin(0), math.sin(math.pi/2)])
differences = calc_div_diff(list(data_x), list(data_y))
p = Newtons_Divided_Differences(list(differences),data_x)
test_x = np.array([math.pi/4])
test_y = p(test_x)
print("Value of the interpolating polynomial")
print(test_y[0])

actual = math.sin(math.pi/4)

truncation_error = abs(actual - test_y[0])
print("\nTruncation error")
print(truncation_error)
```

```
Output:

Value of the interpolating polynomial
0.5

Truncation error
0.20710678118654746
```