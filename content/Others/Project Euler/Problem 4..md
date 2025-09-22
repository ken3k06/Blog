![[Pasted image 20250922203911.png]]
*Solve*
```python
def is_pal(n):
    s = str(n)
    return s == s[::-1]

max_pal = 0
factors = (0, 0)
for a in range(999, 99, -1):
    for b in range(a, 99, -1):  
        prod = a * b
        if prod <= max_pal:
            break
        if is_pal(prod):
            max_pal = prod
            factors = (a, b)
print(max_pal, factors)  
```
