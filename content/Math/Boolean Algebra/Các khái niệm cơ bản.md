## Biểu diễn của hàm Boolean 

Ta đã biết $\displaystyle GF( 2)$ là một trường hữu hạn với số lượng phần tử nhỏ nhất có thể có đó là $\displaystyle \{0,1\}$. Phần tử đơn vị đối với phép cộng là $\displaystyle 0$ và phần tử đơn vị đối với phép nhân là $\displaystyle 1$. Phép cộng trên trường này tương đương với phép XOR khi làm việc với các giá trị nhị phân và phép nhân chính là phép AND. 

Bây giờ, cho $\displaystyle GF^{n}( 2)$ là một không gian vector $\displaystyle n$ chiều trên trường hữu hạn $\displaystyle GF( 2)$. Một hàm $\displaystyle f:GF^{n}( 2)\rightarrow GF( 2)$ được gọi là một hàm Boolean $\displaystyle n$ biến. Ta viết $\displaystyle f( x) =f( x_{1} ,x_{2} ,...,x_{n})$ và quy ước $\displaystyle x=( x_{1} ,x_{2} ,...,x_{n})$ kể từ bây giờ. Một vector chứa tất cả các đầu ra của $\displaystyle f( x)$ được gọi là bảng chân trị của $\displaystyle f( x)$. Có tổng cộng $\displaystyle 2^{n}$ đầu vào khác nhau cho nên bảng chân trị cũng là một vector có số chiều là $\displaystyle 2^{n}$. Ngoài ra ta có thể xem mỗi vector $\displaystyle x$ là biểu diễn nhị phân duy nhất của một số nguyên trong khoảng từ $\displaystyle 0$ tới $\displaystyle 2^{n} -1$. 
$$
\begin{equation*} x=( x_{1} ,...,x_{n}) =\sum _{i=1}^{n} x_{i} 2^{n-i} \end{equation*} 
$$

$\displaystyle Supp( f)$ là tập hợp các đầu vào của hàm $\displaystyle f$ mà tại đó có giá trị bằng 1. Tức là
$$
\begin{equation*} 
Supp( f) =\{x:f( x) =1\} 
\end{equation*}
$$ Ngược lại với $\displaystyle \text{Supp}$ thì ta có tập $\displaystyle \overline{Supp}( f) =\{x:f( x) =0\} =Supp( 1\oplus f( x))$. Số lượng các giá trị 1 trong vector chân trị của hàm $\displaystyle f$ được gọi là khoảng cách Hamming của nó và kí hiệu là $\displaystyle wt( f)$. Hiển nhiên thì $\displaystyle wt( f)$ chính là số lượng các phần tử trong tập $\displaystyle Supp( f)$. Hàm $\displaystyle f$ được gọi là cân bằng nếu như $\displaystyle wt( f) =2^{n-1}$ tức là số lượng các đầu ra bằng 1 bằng với các đầu ra bằng 0. Một hàm $\displaystyle f$ được gọi là hàm affine nếu như tồn tại các giá trị $\displaystyle a_{0} ,a_{1} ,...,a_{n} \in GF( 2)$ sao cho
$$
\begin{equation*} 
f( x) =a_{0} \oplus a_{1} x_{1} \oplus ...\oplus a_{n} x_{n} 
\end{equation*}
$$
Nếu $\displaystyle a_{0} =0$ thì $\displaystyle f( x)$ là hàm tuyến tính (linear function).

Tiếp theo ta kí hiệu $\displaystyle \mathcal{F}_{n}$ là tập tất cả các hàm boolean $\displaystyle n$ biến, $\displaystyle \mathcal{L}_{n}$ là tập hợp tất cả các hàm tuyến tính và $\displaystyle \mathcal{A}_{n}$ là các hàm affine. Như vậy 
$$
\begin{equation*} 
\mathcal{L}_{n} \subset \mathcal{A}_{n} \subset \mathcal{F}_{n} 
\end{equation*}
$$
Và đây đều là các vành giao hoán (commutative rings)
Ngoài ra ta có 
$$
| \mathcal{F}_n| = 2^{2^n}
$$
Vì có tổng cộng $2^n$ giá trị đầu vào và với mỗi giá trị đầu vào như vậy sẽ có $2$ trường hợp cho giá trị đầu. 
Tương tự $\displaystyle |\mathcal{A}_{n} |=2^{n+1}$ và $\displaystyle |\mathcal{L}^{n} |=2^{n}$.

Với $\displaystyle f( x) ,g( x)$ là hai hàm boolean $\displaystyle n$ biến, ta định nghĩa khoảng cách giữa $\displaystyle f( x)$ và $\displaystyle g( x)$, kí hiệu bởi $\displaystyle d( f,g)$ là số các tọa độ khác nhau trong biểu diễn bảng chân trị giữa $\displaystyle f( x)$ và $\displaystyle g( x)$. Như vậy 
$$
\begin{equation*} 
d( f,g) =wt( f\oplus g) 
\end{equation*} 
$$
Vì $\displaystyle a\oplus b=0$ nếu như $\displaystyle a=b$ và tương tự $\displaystyle a\oplus b=1$ nếu như $\displaystyle a\neq b$. Ngoài ra ta còn có 
$$
\begin{equation*} 
wt( f\oplus g) =wt( f) +wt( g) -2wt( fg) 
\end{equation*}
$$
Tính phi tuyến của $\displaystyle f( x)$ kí hiệu là $\displaystyle nl( f)$, là khoảng cách nhỏ nhất giữa $\displaystyle f( x)$ và tất cả các hàm
affine.
$$
\begin{equation*} 
nl( f) =\min\{d( f( x) ,l( x)) \ :\ l( x) \in \mathcal{A}_{n}\} 
\end{equation*}
$$

### Dạng chuẩn tắc đại số - ANF

ANF - Algebraic normal form hay còn gọi là dạng chuẩn tắc đại số. Mỗi hàm $f$ đều có thể được biểu diễn duy nhất dưới dạng sau
$$
\begin{equation*} 
f( x) =c_{0} \bigoplus _{1\leqslant i\leqslant n} c_{i} x_{i} \bigoplus _{1\leqslant i< j\leqslant n} c_{ij} x_{i} x_{j} \bigoplus \dotsc \bigoplus c_{1,...,n} x_{1} x_{2} ...x_{n} 
\end{equation*}
$$
Trong đó $\displaystyle c_{0} ,c_{i} ,c_{ij} ,...,c_{1,...,n} \in GF( 2)$. Ví dụ: $\displaystyle f( x_{1} ,x_{2} ,x_{3}) =x_{1} \oplus x_{2} x_{3}$. Mỗi bộ $\displaystyle x_{1} ,x_{2} x_{3}$ như vậy được gọi là các multiplicative term. Số lượng các biến trong multiplicative term được gọi là bậc đại số của term đó. Và bậc đại số của hàm $\displaystyle f$ chính là bậc đại số lớn nhất của các term mà có hệ số khác 0. Trong đại số boolean thì mỗi biến độc lập $\displaystyle x_{i}$ có bậc tối đa là 1 vì $\displaystyle x_{i}^{2} =x_{i}$, bất kể giá trị của $\displaystyle x_{i}$ là gì. Như trong ví dụ trên thì bậc của $\displaystyle f$ là 2 vì bậc đại số lớn nhất trong số các term là $\displaystyle 2$, là bậc của $\displaystyle x_{2} x_{3}$. Ví dụ
```python
from sage.crypto.boolean_function import BooleanFunction
B = BooleanPolynomialRing(names=('x0', 'x1', 'x2', 'x3',)); (x0, x1, x2, x3,) = B._first_ngens(4)
f = BooleanFunction(x1*x2 + x1*x2*x3 + x1)
print(f.algebraic_degree())
```

Nếu $\displaystyle f$ có bậc đại số là 1 thì $\displaystyle f$ chính là hàm affine. Nếu $\displaystyle f( 0) =0$ thì $\displaystyle f( x)$ chính là hàm tuyến tính, hay nói cách khác $\displaystyle f$ tuyến tính khi biến tự do của nó bằng 0. Khi $\displaystyle f$ tuyến tính thì ta có tính chất  sau 
$$
\displaystyle f( x\oplus y) =f( x) \oplus f( y)
$$
### Biểu diễn theo bảng chân trị
Ngoài cách biểu diễn ở trên ra thì ta còn có thể biểu diễn hàm $\displaystyle f$ dưới dạng vector chân trị của nó. Chẳng hạn với $\displaystyle f( x) =x_{1} \oplus x_{2} x_{3}$ thì vector chân trị của nó là $\displaystyle 00011110$ ứng với thứ tự các biến là $\displaystyle 000,001,010,011,100,101,110,111$.
Có thể kiểm tra như sau:
```python
from sage.all import *
import sage.logic.propcalc as propcalc
f = propcalc.formula("x1 ^ (x2&x3)")
g = f.truthtable()
print(g)
'''
x1     x2     x3     value
False  False  False  False  
False  False  True   False  
False  True   False  False  
False  True   True   True   
True   False  False  True   
True   False  True   True   
True   True   False  True   
True   True   True   False  
'''
```

### Support Representation

Biểu diễn hàm $\displaystyle f$ theo tập $\displaystyle \text{Supp}( f)$ của nó tức là ta sẽ biểu diễn thông qua một tập hợp chứa các vector đầu vào mà tại đó $\displaystyle f( x) =1$. Cách biểu diễn này hiệu quả đối với những hàm có Hamming weight thấp.

## Walsh transforms and Walsh Spectrum 

Walsh transform hay còn gọi là biến đổi Walsh là một phép biến đổi trực giao, có vai trò khá quan trọng trong việc phân tích các tính chất của hàm số Boolean.
Cụ thể như sau

### Walsh functions and walsh transforms

**Định nghĩa 1.** Họ các hàm Walsh trực giao trên $GF^n(2)$ được xác định bởi:
$$
W(w,x) = \displaystyle ( -1)^{\langle w,x\rangle }
$$
Trong đó $w=(w_1,...,w_n)$ và $x=(x_1,...,x_n)$ là các vector nhị phân và $\langle w,x \rangle= \sum_{i=1}^{n} w_ix_i$ là tích trong của hai vector. 
Một số tính chất 
1/ Tính đối xứng: $\displaystyle W( w,x) =W( x,w)$ 
2/ Tính trực giao: $\displaystyle \sum _{w=0}^{2^{n} -1} W( w,x) W( w,t) =\begin{cases} 2^{n} ,\ x=t\\ 0 \end{cases}$ 
Từ tính trực giao của họ các hàm Walsh trực giao thì ta có
$$
\begin{equation*} 
\sum _{w=0}^{2^{n} -1} W( w,x) =\sum _{w=0}^{2^{n} -1}( -1)^{\langle w,x\rangle } =\begin{cases} 2^{n} ,x=0 & \\ 0,x\neq 0 & \end{cases} 
\end{equation*}
$$
Tổng quát hơn ta có: 

**Bổ đề.** 
Cho $\displaystyle V$ là một vector thuộc không gian con của $\displaystyle GF^{n}( 2)$ và
$$
\begin{equation*}
V^{\perp } =\{y:\forall x\in V,\ \langle x,y\rangle =0\} 
\end{equation*} 
$$
là không gian vector trực giao của $\displaystyle V$. Khi đó ta có 
$$
\begin{equation*}
\sum _{w\in V} W( w,x) =\begin{cases} |V| & ,\ w\in V^{\perp }\\ 0 & ,w\notin V^{\perp } \end{cases} 
\end{equation*}
$$
