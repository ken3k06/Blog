
Note lại một số cú pháp hay được sử dụng trong Sage.

- Extension để chạy file Sagemath trực tiếp trong VSCode với highlight syntax: https://github.com/n-WN/sagemath-vscode-enhanced
- Doc chính thức của Sagemath: https://doc.sagemath.org/html/en/reference/index.html

Ở đây mình chỉ note lại những hàm thường hay sử dụng để tiện cho việc tra cứu. 
## Ma trận

- Cú pháp đầy đủ để tạo một ma trận trong Sage sẽ là:
```python
Matrix(base_ring, nrows, ncols, entries)
```
Trong đó `base_ring` là khai báo vành mà các phần tử của ma trận thuộc về, chẳng hạn như `QQ,ZZ,RR, GF(p)`. Kế đó ta sẽ khai báo hàng và cột và cuối cùng là các entries. 
Khi truyền các entries vào thì ta lưu ý rằng Sage sẽ mặc định danh sách ta truyền vào sẽ là các hàng.  Ví dụ ta muốn tạo một ma trận như sau: 
$$
\begin{equation*}
M=\begin{pmatrix}
1 & 2 & 3\\
4 & 5 & 6\\
7 & 8 & 9
\end{pmatrix}
\end{equation*}
$$
```python
sage: M = Matrix(ZZ, [[1,2,3],[4,5,6],[7,8,9]])
sage: M
[1 2 3]
[4 5 6]
[7 8 9]
sage:
```

- Tạo ma trận đơn vị $I$ và ma trận không:
```python
sage: M = zero_matrix(3)
sage: M
[0 0 0]
[0 0 0]
[0 0 0]
sage: M = identity_matrix(3)
sage: M
[1 0 0]
[0 1 0]
[0 0 1]
sage:
```

- Ta có thể tạo các dạng ma trận đặc biệt dựa trên chỉ số của nó.

```python
sage: # ma tran don vi 
sage: m = matrix(ZZ,3,3, lambda i, j : i==j);
sage: m
[1 0 0]
[0 1 0]
[0 0 1]
sage: n = 5
sage: # ma tran reversal 
sage: m = matrix(ZZ, 5 , 5 , lambda i,j : 1 if i+j == n-1 else  0)
sage: m
[0 0 0 0 1]
[0 0 0 1 0]
[0 0 1 0 0]
[0 1 0 0 0]
[1 0 0 0 0]
sage: 
```

- Tạo ma trận với các biến Symbolic.

```python
sage: R = PolynomialRing(QQ, 9 , 'x')
sage: A = matrix(R,3,3, R.gens()); A
[x0 x1 x2]
[x3 x4 x5]
[x6 x7 x8]
sage:
```

Trong một số trường hợp, chẳng hạn ta muốn nghiên cứu các tính chất của một ma trận cụ thể nào đó. Thay vì biến đổi trực tiếp trên ma trận này thì ta có thể khai báo nó với keywords `immutable = True` và gọi `M_ = copy(M)` để tạo một bản sao và làm việc. 

```python
sage:     M = Matrix([[1,2,3], [4,5,6], [7,8,9]], immutable=True)
sage: M[0]
(1, 2, 3)
sage: M[0,0] = 1
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
Cell In[43], line 1
----> 1 M[Integer(0),Integer(0)] = Integer(1)

File ~/miniforge3/envs/sage/lib/python3.12/site-packages/sage/matrix/matrix0.pyx:1460, in sage.matrix.matrix0.Matrix.__setitem__ (build/cythonized/sage/matrix/matrix0.c:15121)()
   1458 # If the matrix is immutable, check_mutability will raise an
   1459 # exception.
-> 1460 self.check_mutability()
   1461
   1462 if type(key) is tuple:

File ~/miniforge3/envs/sage/lib/python3.12/site-packages/sage/matrix/matrix0.pyx:422, in sage.matrix.matrix0.Matrix.check_mutability (build/cythonized/sage/matrix/matrix0.c:11908)()
    420 """
    421 if self._is_immutable:
--> 422     raise ValueError("matrix is immutable; please change a copy instead (i.e., use copy(M) to change a copy of M).")
    423 else:
    424     self._cache = None

ValueError: matrix is immutable; please change a copy instead (i.e., use copy(M) to change a copy of M).
sage: M_ = copy(M)
sage: M_[0,0]=1
sage: M_
[1 2 3]
[4 5 6]
[7 8 9]
sage: M_[0,0]=5
sage: M_
[5 2 3]
[4 5 6]
[7 8 9]
sage:
```

Để lấy phần tử ở hàng $n$, cột $m$ của ma trận thì ta gọi `M[n,m]` cách bởi dấu phẩy. 

Tiếp theo, để lấy một ma trận con của `A` thì ta dùng cú pháp 
```python
A.submatrix(row, col, nrows, ncols)
```
Nó sẽ lấy một ma trận con, có tọa độ của góc trên cùng bên trái là `[row,col]` và sẽ lấy `nrows` hàng và `ncols` cột. 

```python
sage: m = random_matrix(ZZ, 5,5)
sage: m
[ -1   1   2 -15   0]
[  1   0   0  -1  -1]
[ -1  -1   0 -27   1]
[ -3  -3   1 -14   1]
[ -1  -3   1   1   0]
sage: m.submatrix(0,0,2,2)
[-1  1]
[ 1  0]
sage: m.submatrix(3,3,1,2)
[-14   1]
sage: m.submatrix(3,3,2,2)
[-14   1]
[  1   0]
sage:
```

Ở trên thì ta cũng có thêm cú pháp `random_matrix` để sinh một ma trận ngẫu nhiên trên vành và kích thước cho trước. 

- Cho hai ma trận $A$ và $B$. Ta muốn ghép thêm ma trận $B$ vào bên phải $A$ thì có thể dùng cú pháp `A.augment(B)` (phải cùng số hàng)
```python
sage: A = random_matrix(ZZ,4,4)
sage: B = random_matrix(ZZ, 4,1)
sage: A.augment(B)
[  1 -55   0  43   0]
[ -1   1  -4   0   0]
[  0   0  -1   1   0]
[  1   1   0  -5  10]
sage:
```
- Còn nếu muốn ghép thêm vào bên dưới thì dùng cú pháp `stack` (phải cùng số cột)
```python
sage: a = random_matrix(ZZ, 2,3)
sage: b = random_matrix(ZZ, 1,3)
sage: a.stack(b)
[-32   1  -2]
[  1  -1  -1]
[ -1  39  -4]
sage: b
[-1 39 -4]
sage: a
[-32   1  -2]
[  1  -1  -1]
sage:
```
- Còn để tạo ma trận khối thì thay vì gọi `matrix` ta sẽ gọi `block_matrix`
```python
sage:     A = Matrix(QQ,2,2,[3,9,6,10])
sage: A = random_matrix(ZZ,4,4)
sage: block_matrix([[A,-A],[~A,100*A]])
[      -26         4        -2        -1|       26        -4         2         1]
[        0         1         0         3|        0        -1         0        -3]
[        2         1        -1        -2|       -2        -1         1         2]
[        1        -3        32         9|       -1         3       -32        -9]
[---------------------------------------+---------------------------------------]
[-142/4455  197/4455    76/891    1/1485|    -2600       400      -200      -100]
[   13/297    97/297   166/297      2/99|        0       100         0       300]
[  41/4455 -151/4455    91/891   52/1485|      200       100      -100      -200]
[  -13/891   200/891  -166/891    -2/297|      100      -300      3200       900]
sage:
```

## Đại số tuyến tính 
- Giải hệ phương trình:
	-  Để giải phương trình $AX = Y$, tìm $X$ thì ta dùng cú pháp `A.solve_right(Y)`
	- Để giải phương trình $XA = Y$, tìm $X$ thì ta dùng cú pháp `A.solve_left(Y)`

## Đa thức

### Đa thức đơn biến 

Để tạo vành đa thức 1 biến với ẩn $x$ chẳng hạn thì có những cách khai báo sau: 
```python
sage: R = PolynomialRing(QQ, ['t'])
sage: x = R.gen()
sage: R.random_element()
2*t^2 + t - 1
sage:
```
Khi khai báo dòng đầu tiên thì Sage không biết rõ `t` có vai trò là gì. Như vậy sage sẽ coi `t` như một `string var` dùng để in đa thức ra màn hình. 
```python
sage: R
Univariate Polynomial Ring in t over Rational Field
sage:
```
Ví dụ mọi người gõ 
```python
f=t^3-t+2
```
thì sẽ gặp ngay lỗi `name 't' is not defined`
![[Pasted image 20251201155735.png]]

Có 2 cách để xử lí. Một là ta gọi 
```python
t = R.gen()
```
hoặc bất cứ kí hiệu nào mà ta muốn rồi khai báo lại đa thức `f` là được.

Cách thứ hai là khai báo vành đa thức theo cách sau:
```python
R.<t> = PolynomialRing(QQ)
```
Hoặc 
```python
R.<t> = QQ['t']
R.<t> = QQ[]
```
### Đa thức đa biến 
Với các vành đa thức nhiều biến thì cũng có các cách khai báo sau:
```python

```




Tham khảo: https://doc.sagemath.org/html/en/reference/polynomial_rings/index.html
