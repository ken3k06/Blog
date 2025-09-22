![[Pasted image 20250922200755.png]]

*Solve*
Mọi người có thể tìm từ khóa number of maximal self-avoiding walks from nw to sw corners of a 4-by-n grid để xem công thức truy hồi của $\displaystyle T( n)$. Cụ thể thì công thức truy hồi của $\displaystyle T( n)$ sẽ là $\displaystyle T( n) =2T( n-1) +2T( n-2) -2T( n-3) +T( n-4)$ và ta sẽ sử dụng thuật toán nhân ma trận như bình thường để giải. Cụ thể ta có 

$$
\begin{pmatrix}
2 & 2 & -2 & 1\\
1 &  &  & \\
 & 1 &  & \\
 &  & 1 & 
\end{pmatrix}\begin{pmatrix}
T( n-1)\\
T( n-2)\\
T( n-3)\\
T( n-4)
\end{pmatrix} =\begin{pmatrix}
T( n)\\
T( n-1)\\
T( n-2)\\
T( n-3)
\end{pmatrix}
$$

$$\Longrightarrow \begin{pmatrix}
T( n)\\
T( n-1)\\
T( n-2)\\
T( n-3)
\end{pmatrix} =...=\begin{pmatrix}
2 & 2 & -2 & 1\\
1 &  &  & \\
 & 1 &  & \\
 &  & 1 & 
\end{pmatrix}^{n-4}\begin{pmatrix}
8\\
4\\
1\\
1
\end{pmatrix}$$



Phần tử thứ $\displaystyle n$ của dãy mà ta cần tính sẽ là entry đầu tiên của tích 2 ma trận ở trên. 
Code như dưới đây:
Lúc đầu mình thử code bằng sage nhưng có vẻ không được hiệu quả lắm vì Sage không được thiết kế để tối ưu tính toán các ma trận với số mũ lớn vì vậy nó chạy rất lâu (Sage chạy trên giao diện symbolic)
```python
from sage.all import *
base=Matrix(4,1,[8,4,1,1])
base_exp=Matrix([[2,2,-2,1],[1,0,0,0],[0,1,0,0],[0,0,1,0]])
print(base)
print(base_exp)
mod=10**8
def return_nth_value_mod(n):
    result_matrix=base_exp**n*base
    entry=result_matrix[0,0]
    return entry % mod
n=10**12-4
print(return_nth_value_mod(n))
```
Cho nên mình thử xét một phương án khác đó chính là sử dụng thư viện `numpy` trong python để tính lũy thừa ma trận bằng phương pháp nhị phân. 
```python
from numpy import *
def matrix_multiply(A,B,mod):
    return dot(A,B) % mod


def matrix_power(A,n,mod):
    result=eye(len(A),dtype=int)
    base =  A % mod

    while n>0:
        if n%2==1:
            result=matrix_multiply(result,base,mod)
        base=matrix_multiply(base,base,mod)
        n//=2
    return result

A = array([
    [2, 2, -2, 1], 
    [1, 0, 0, 0], 
    [0, 1, 0, 0], 
    [0, 0, 1, 0]
])

B = array([
    [8], 
    [4], 
    [1], 
    [1]
])

n=int(input())
mod=10**8
A_pow=matrix_power(A,n,mod)
result=matrix_multiply(A_pow,B,mod)
print(result[0,0])
```