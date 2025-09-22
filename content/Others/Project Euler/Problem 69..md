![[Pasted image 20250922200634.png]]

*Solve*
```python
from math import *
from sympy import factorint

def euler_totient(n):
    result = n
    p_factors = factorint(n)
    for p in p_factors:
        result *= (p - 1) / p
    return int(result)
# thiết lập hàm để tính phi hàm euler của n. sau khi tính xong ta sẽ tìm phần tử max

def max_ratio_n_phi(n):
  valid_n=[]
  max_ratio=0
  for i in range(1,n):
    ratio_value=i/euler_totient(i)
    if ratio_value>max_ratio:
      max_ratio=ratio_value
      valid_n=[i]
    elif ratio_value==max_ratio:
      valid_n.append(i)
  return valid_n,max_ratio

max_ratio_n_phi(1000000)
```
