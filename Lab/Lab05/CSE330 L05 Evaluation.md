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

**f(x) = 5x<sup>6</sup>**
