# Class Evaluation

```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from numpy.polynomial import Polynomial
```

```
def dh(f, h, x):
    '''
    Input:
        f: np.polynomial.Polynonimial type data.
        h: floating point data.
        x: np.array type data.
    Output:
    '''
    return (f(x+h) - f(x-h)) / (2*h)
```

## Task

**Consider the following function:**

**f(x) = 5x<sup>6</sup> - x<sup>5</sup> + 7x<sup>4</sup> + 3.75x<sup>3</sup> - 2x<sup>2</sup> + 1.5x + 15**

**Now, compute the Second Degree Richardson Extrapolation, D<sup>1</sup> at x = 1 and h = 0.4 when the formula is derived using h -> h/3. Print the answer upto 2 decimal places.**

**N.B. You can use the previously learned methods while solving the problem**

```
def dh1(f, h, x):
    return ((9 * dh(f, h/3, x)) - dh(f,h,x)) / 8

p = Polynomial([15, 1.5, -2, 3.75, 7, -1, 5])
Dh = dh(p, 0.4, 1)
print(f"Central Diff : {round(Dh, 2)}\n")
Dh3 = dh1(p, 0.4, 1)
print(f"Central Diff : {round(Dh3, 2)}")
```
