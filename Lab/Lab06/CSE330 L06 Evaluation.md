# Class Evaluation

```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from numpy.polynomial import Polynomial
```

## Task

**Let f(x) be a function of x.**

  **f(x) = x<sup>5</sup> + 2.5x<sup>4</sup> - 2x<sup>3</sup> - 6x<sup>2</sup> + 0.5x + 2**

**a. Find the actual roots of f(x) and print them.**

```
# The polynomial and the range is defined for you
f = Polynomial([2.0, 0.5, -6.0, -2.0, 2.5, 1.0])
a = -0.5
b = 1.3
m = (a + b) / 2
e = 1e-6

root = 0.0  # You need to update this value

# Populate the following lists in each iteration
list_a = []
list_b = []
list_m = []
list_f = []

while (b-a)>e:
    m = (a + b) / 2
    fm=f(m)

    list_a.append(a)
    list_b.append(b)
    list_m.append(m)
    list_f.append(fm)

    if f(a)*fm < 0:
        b=m
    elif f(a)*fm > 0:
        a=m

root=m
print(f"Actual root: {root}")
```
```
Output:
Actual root: 0.618034839630127
```

**b. Given,**

  **g<sub>1</sub>(x) = ((-x<sup>5</sup> + 2x<sup>3</sup> + 6x<sup>2</sup> - 0.5x - 2)/2.5)<sup>1/4</sup>**

**Apply Fixed Point Method on the g<sub>1</sub>(x) and find the appropriate root, show 20 iterations for x<sub>0</sub> = 0.8 and show the convergence table using data from each iteration.**

```
g1 = Polynomial([-2, -0.5, 6, 2, -1])

x0 = 0.80
g1_a = [x0]

for i in range(20):
    xNext1 = np.power((g1(g1_a[-1])*(1/2.5)), 1/4)
    g1_a.append(xNext1)

print(pd.DataFrame({'g1(x)':g1_a,}))
```

```
Output:
       g1(x)
0   0.800000
1   0.952108
2   1.115246
3   1.251470
4   1.347338
5   1.407611
6   1.442906
7   1.462714
8   1.473562
9   1.479424
10  1.482568
11  1.484247
12  1.485143
13  1.485619
14  1.485873
15  1.486008
16  1.486080
17  1.486118
18  1.486138
19  1.486149
20  1.486155
```
