# 3次スプライン補間：　時系列データの平均化

**3次スプライン補間は、時系列データを平均値化する際に使用される手法である。**
例えば、ランニング接地期中の地面反力を30歩分記録し、これらを平均値化したい場合、基本的に一歩ごとの地面反力の時間は同じではない。
そのため、時系列データを平均するためには、時間を100％に規格化しデータ数を合わせる必要がある。

この手法の問題点としては、時間の情報が無くなるという点が挙げられる。
接地時間（秒）が大きく異なる場合や、左右脚の比較をする場合に、時間を規格化し平均値化したデータを観察することは注意すべきである。


## Python
``` python
import pandas as pd
import numpy as np
from scipy.interpolate import interp1d

def Spline_func(VAR):
    Num = VAR.size
    x = np.arange(Num)
    y = VAR
    f = interp1d(x, y, kind='cubic')
    k = np.linspace(0, Num-1, num = 101)
    spline = f(k)
    return spline
```

`VAR` は、pd.Dataframe形式のシグナルデータを入力（例. ランニング接地期中の地面反力など）。
`k = np.linspace(0, Num-1, num = 101)`内の`num = 101` は、スプライン補間のデータ数である。デフォルト設定は101点としている。
