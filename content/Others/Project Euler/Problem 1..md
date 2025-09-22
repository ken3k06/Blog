If we list all the natural numbers below $10$ that are multiples of $3$ or $5$, we get $3, 5, 6$ and $9$. The sum of these multiples is $23$.
Find the sum of all the multiples of $3$ or $5$ below $1000$.

*Solve*
Ý tưởng đầu tiên là mình thử brute qua hết toàn bộ các bội của $3$ và $5$ trong khoảng cho trước. Sau đó lấy giao 2 tập lại vì có một số số là bội của cả hai. 
```python
# naive
def find_mul(mod, limit):
    res = []
    for i in range(mod,limit,mod):
        if i % mod == 0:
            res.append(i)
    return res
res3 = find_mul(3,1000)
res5 = find_mul(5,1000)
r = set(res3) | set(res5)
print(sum(r))
```
Độ khó 5% 
