
## Định thức của ma trận

**Định nghĩa 1.** Mỗi song ánh từ tập $\displaystyle \{1,2,...,n\}$ vào chính nó được gọi là một phép thế bậc $\displaystyle n$. Tập hợp tất cả các phép thế bậc $\displaystyle n$ được kí hiệu bởi $\displaystyle S_{n}$. $\displaystyle S_{n}$ cùng với phép hợp thành các ánh xạ lập thành một nhóm, được gọi là nhóm đối xứng bậc $\displaystyle n$. Nhóm này có $\displaystyle n!$ phần tử. Đây cũng là số các hoán vị có thể có của một tập hợp gồm $\displaystyle n$ phần tử phân biệt.

Từ giờ, ta sẽ coi một hoán vị $\displaystyle ( a_{1} ,a_{2} ,...,a_{n})$ như là một song ánh $\displaystyle \sigma :\{1,2,...,n\}\rightarrow \{1,2,...,n\}$ cho bởi $\displaystyle \sigma ( i) =a_{i}$. Khi coi hoán vị như một song ánh, ta có thể lấy hợp thành của hai hoán vị. Để thuận tiện cho việc tính toán hợp thành của hai ánh xạ, người ta thường kí hiệu hoán vị như sau: 
$$
\begin{equation*}
\sigma =\begin{pmatrix}
1 & 2 & ... & n-1 & n\\
a_{1} & a_{2} & ... & a_{n-1} & a_{n}
\end{pmatrix}
\end{equation*}
$$
Như vậy ta có thể hiểu $\displaystyle \sigma ( 1) =a_{1} ,...,\sigma ( n) =a_{n}$. 
Khi coi hoán vị như song ánh ta có thể phân tích hoán vị như hợp thành của các hoán vị dạng đơn giản. Trong nhiều bài toán khi cần chứng minh một tính chất đúng cho hoán vị bất kì, ta chỉ cần chứng minh nó đúng với các hoán vị đơn giản. Một dạng phân tích hoán vị là phân tích thành các xích. 
Tưởng tượng như sau: Ta xét một đồ thị có $\displaystyle n$ đỉnh đánh số từ $\displaystyle 1$ đến $\displaystyle n$. Ta vẽ cạnh có hướng đi từ đỉnh $\displaystyle i$ đến đỉnh $\displaystyle \sigma ( i)$. Từ tính chất song ánh của $\displaystyle \sigma$ ta suy ra tại mỗi đỉnh có đúng 1 cạnh đi vào và một cạnh đi ra. Do đó ta nhận được một đồ thị có dạng hợp thành của các chu trình rời nhau, mỗi chu trình như vậy sẽ được gọi là một xích. Ta có thể coi mỗi xích là một hoán vị vòng quanh của một tập con $\displaystyle \{x_{1} ,x_{2} ,...,x_{k}\} \subset \{1,2,...,n\}$. Như vậy một hoán vị sẽ được phân tích một cách duy nhất thành các xích rời nhau. 
Ví dụ
$$
\begin{equation*}
\sigma =\begin{pmatrix}
1 & 2 & 3 & 4 & 5 & 6 & 7 & 8 & 9 & 10\\
8 & 6 & 5 & 9 & 3 & 10 & 4 & 7 & 1 & 2
\end{pmatrix}
\end{equation*}
$$
Ta đi bắt đầu từ $\displaystyle 1$. Lúc này ta xét 
$$
\begin{equation*}
1\rightarrow \sigma ( 1) =8\rightarrow \sigma ( 8) =7\rightarrow \sigma ( 7) =4\rightarrow \sigma ( 4) =9\rightarrow \sigma ( 9) =1
\end{equation*}
$$
Vậy ta được một xích là $\displaystyle ( 1\ 8\ 7\ 4\ 9)$. Tiếp tục xét 
$$
\begin{equation*}
2\rightarrow \sigma ( 2) =6\rightarrow \sigma ( 6) =10\rightarrow \sigma ( 10) =2
\end{equation*}
$$
Xích tiếp theo là $\displaystyle ( 2\ 6\ 10)$ và cuối cùng là $\displaystyle 3\rightarrow \sigma ( 3) =5\rightarrow \sigma ( 5) =3$. Vậy ta phân tích 
$$
\begin{equation*}
\sigma =( 1\ 8\ 7\ 4\ 9)( 3\ 5)( 2\ 6\ 10)
\end{equation*}
$$

Một xích mà chỉ có 2 phần tử thì được gọi là phép thế. 
Dấu của phép thế được tính bởi 
$$
\begin{equation*}
sgn( \sigma ) =\prod _{i\neq j}\frac{\sigma ( i) -\sigma ( j)}{i-j} \in \{\pm 1\}
\end{equation*}
$$
Cho một ma trận vuông $\displaystyle A=( a_{ij})_{n\times n}$ với các phần tử trong trường $\displaystyle K$. 
**Định nghĩa 2.** Định thức của ma trận $\displaystyle A$ được kí hiệu bởi $\displaystyle \det A$ hoặc $\displaystyle |A|$ là phần tử sau đây của trường $\displaystyle K$.
$$
\begin{equation*}
\det A=|A|=\sum _{\sigma \in S_{n}} sgn( \sigma ) a_{\sigma ( 1) 1} ...a_{\sigma ( n) n}
\end{equation*}
$$
Ở trên là định nghĩa cho định thức của ma trận vuông. Bây giờ ta sẽ tìm cách để tính nó. 
Như ta đã biết thì trong Sagemath có hàm để ta trực tiếp tính toán định thức của ma trận. 
```python
sage: M = Mat(ZZ,5,5).random_element()
sage: M.det()
-9942
sage: M.determinant()
-9942
sage: det(M)
-9942
sage: M
[ 12   2   3  -3   1]
[ -1  -3   1   1  -1]
[-25   0   1  -2  -1]
[ -4  -1   0   2  -1]
[  0   7   0  15  16]
sage:
```

Nếu như tính theo định nghĩa thì sẽ rất phức tạp vì ta cần gọi ra tổng cộng $n!$ hoán vị cho các phần tử rồi lấy tổng của chúng lại. 
