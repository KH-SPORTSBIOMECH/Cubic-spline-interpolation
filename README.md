# Cubic-spline-interpolation

``` python
import pandas as pd
import numpy as np
from scipy.interpolate import interp1d

def Spline_func(VAR):
    Num = VAR.size
    x = np.arange(Num)
    y = VAR
    f = interp1d(x, y, kind='cubic')
    k = np.linspace(0,Num-1, num=101)
    spline = f(k)
    return spline
```

`VAR` is set as the signal data (e.g. Ground reaction force data during running in stance phase).

`num=101` in `k = np.linspace(0,Num-1, num=101)` is the number of spline data. The default is set as 101 points.
