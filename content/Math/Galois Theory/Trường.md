Để có thể giải quyết được vấn đề giải phương trình bằng căn thức, ta phải xét tập hợp tất cả các số có thể nhận được từ các hệ số của phương trình đã cho bởi một số hữu hạn các phép toán cộng trừ nhân chia.

Một tập con $K$ của tập các số phức $\mathbb{C}$ được gọi là một trường nếu $K$ chứa ít nhất một số khác 0 và đóng với các phép toán cộng trừ nhân chia. Có nghĩa là

$$ 
a,b\in K \rightarrow a+b,a-b,ab,a:b \in K 
$$

Chú ý: Mọi trường $K$ đều chứa tập số hữu tỉ $\mathbb{Q}$. Thật vậy do $K$ chứa một số $a\neq 0$ cho nên $a:a=1 \in K$ và $a-a=0\in K$. Như vậy mọi số nguyên $n$ đều thuộc $K$ và ta cũng có $\displaystyle \frac{a}{b} \in K, a\in\mathbb{Z}, b \in \mathbb{Z}$.

Cho $K$ là một trường tùy ý và $T$ là một tập gồm một số các số phức. Ta kí hiệu $K(T)$ là tập các số nhận được từ $K$ và $T$ bởi các phép toán cộng trừ nhân chia. Theo định nghĩa thì $K(T)$ là một trường và là trường nhỏ nhất chứa $K$ và $T$. Ta gọi $K(T)$ là trường mở rộng của $K$ bởi tập $T$.

Ví dụ: $\mathbb{C}$ là mở rộng của trường $\mathbb{R}$ bởi số ảo $i$.

Nếu $T$ chứa ít nhất một số khác 0 thì tập các số nhận được từ $T$ bởi các phép toán cộng trừ, nhân chia tạo thành một trường.

Nếu $T$ là một tập hữu hạn các số $a_1,a_2,..,a_n$ thì ta dùng kí hiệu $K(a_1,a_2,...,a_n)$ thay cho $K(T)$Ta có thể mô tả các phần tử của $K(a_1,a_2,...,a_n)$ thông qua các đa thức nhiều biến.

Một đa thức của các biến $X_1,...,X_n$ với hệ số trong $K$ là một biểu thức $P(X_1,...,X_n)$ có dạng

$$
\sum_{\alpha \in \mathbb{N}^n} c_{\alpha} X_1^{\alpha_1}...X_n^{\alpha_n} 
$$

trong đó $\alpha=(\alpha_1,...,\alpha_n)$ và $c_\alpha \in K$ sao cho chỉ có một số hữu hạn các hệ số $c_\alpha$ khác 0.

Tổng và tích định nghĩa/khai triển tương tự đa thức một biến.

Bổ đề. Cho $K(a_1,a_2,...,a_n)$ là một trường mở rộng của $K$. Ta có

$$ 
K( a_{1} ,...,a_{n}) =\left\{\frac{P( a_{1} ,...,a_{n})}{Q( a_{1} ,...,a_{n})} \ |\ P,Q\in K[ x_{1} ,...,x_{n}] ;\ Q( a_{1} ,...,a_{n}) \neq 0\right\} 
$$

Số $a$ được gọi là phần tử căn trên trường $K$ nếu tồn tại một số $c\in K$ và một số nguyên dương $r$ sao cho $a = \sqrt[r]{c}$. Trường $E$ chứa $K$ được gọi là mở rộng căn của $K$ nếu tồn tại các phần tử $a_1,...,a_n\in E$ sao cho $E=K(a_1,...,a_n)$ và $a_i$ là phần tử căn trên trường $K(a_1,...,a_{i-1})$.

**Bổ đề.** Cho $T$ là một tập các số phức có chứa ít nhất một số khác không. Một số $a$ tính được từ các số của $T$ thông qua các phép toán cộng, trừ, nhân chia và khai căn khi và chỉ khi $a$ nằm trong một mở rộng căn của trường $\mathbb{Q}(T)$.

Bây giờ ta có thể định nghĩa khái niệm phương trình giải được bằng căn thức một cách chính xác về mặt toán học.

Cho $f = c_0X^n+c_1X^{n-1}+...+c_n$ là một đa thức với hệ số phức. Đa thức $f$ được gọi là giải được bằng căn thức, nếu tất cả các nghiệm của $f$ nằm trong một mở rộng căn của trường $\mathbb{Q}(c_0,...,c_n)$

**Ví dụ** phương trình bậc hai $aX^2+bX+c=0$ giải được vì các nghiệm của phương trình này nằm trong trường $\mathbb{Q}(a,b,c,\sqrt{b^2-4ac})$.

Tổng quát hơn, ta có thể xét đa thức $f(X)$ với hệ số trong một trường $K$ tùy ý được gọi là trường cơ sở. Cho $a_1,...,a_n$ là tập tất cả các nghiệm của $f$. Ta gọi trường $K(a_1,...,a_n)$ là trường phân rã của $f$ trên $K$. Đa thức $f$ được gọi là giải được bằng căn thức trên $K$ nếu trường phân rã của $f$ trên $K$ nằm trong một mở rộng căn của $K$.

**Ví dụ.**

Cho $f=aX^2+bX+c$ là một đa thức bậc hai với hệ số nằm trong $K$ và $(x_1,x_2)$ là hai nghiệm của $f$. Ta thấy ngay $x_{1,2}\in K(\sqrt{b^2-4ac})$ và $\sqrt{b^2-4ac}=a(x_1-x_2) \in K(x_1,x_2)$ cho nên nó là trường phân rã của $f$ và ta kết luận được rằng $f$ giải được trên $K$ bằng căn thức.

Sau đây, ta có một số khái niệm mới.

Ta gọi $a$ là phần tử đại số trên $K$ nếu $a$ là nghiệm của một đa thức với hệ số trong $K$. Một trường $E$ chứa $K$ được gọi là mở rộng hữu hạn của $K$ nếu $E=K(a_1,...,a_n)$ và $a_i$ là phần tử đại số trên $K(a_1,..,a_{i-1})$.

Trường phân rã của các đa thức hay các mở rộng căn trên $K$ đều là những mở rộng hữu hạn của $K$. 