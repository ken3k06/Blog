---
title: CTF Archive
---
## Chall 1. 
```python
from itertools import count
from hashlib import sha256

for prout in count(start = 1):
  for zgeg in range(1, prout + 1):
    for fouf in range(1, prout + 1):
      if prout ** 3 + zgeg ** 3 == 94 * fouf ** 3:
        h = sha256(str(fouf).encode()).hexdigest()
        print(f"W1{{{h}}}")
        exit(1)
```

