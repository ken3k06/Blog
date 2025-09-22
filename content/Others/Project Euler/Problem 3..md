The prime factors of $13195$ are $5, 7, 13$ and $29$.
What is the largest prime factor of the number $600851475143$
*Solve*
Lời giải dưới đây làm 2 việc:
- Phân tích $n$ thành thừa số nguyên
- Kiểm tra thừa số nào là thừa số nguyên tố và lấy cái lớn nhất
```python
import random

n = 600851475143
def my_sqrt(n):
    left = 0
    right = n
    ans = 0
    while left <= right:
        mid = (left+right)//2
        if mid*mid == n:
            ans = mid
            break
        if mid * mid < n:
            ans = mid 
            left = mid +1
        else:
            right = mid -1
    return ans 
print(my_sqrt(15))
print(my_sqrt(298))
def trial_division(n):
    fac = []
    d = my_sqrt(n) + 1 
    for i in range(2,d):
        if n % i == 0:
            fac.append(i)
            fac.append(n//i)
    return fac
div = trial_division(600851475143)

def binpow(base, e, mod):
    res = 1
    base %= mod
    while e: 
        if e & 1:
            res = res * base % mod
        base = base * base % mod 
        e >>=1  
    return res

def check_composite(n, a , d , s) -> bool:
    x = binpow(a,d,n)
    if (x == 1 or x == n-1):
        return False
    for _ in range(1,s):
        x = x*x % n 
        if x == n-1:
            return False
    return True
def MillerRabin(n, iters:int = 5):
    if n < 4 :
        return n==2 or n==3
    s = 0 
    d = n-1
    while d % 2 == 0:
        d //= 2 
        s +=1
    for _ in range(iters):
        a = random.randrange(2,n-2)
        if check_composite(n,a,d,s):
            return False
    return True
primefac =[]
for d in div:
    if MillerRabin(d):
        primefac.append(d)
print(max(primefac))
```