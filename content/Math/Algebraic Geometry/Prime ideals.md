Trước đó ở bài [[Ideal and Gröbner Basis]] mình có nhắc qua khái niệm về Idean. Ở bài viết này mình sẽ đi sâu hơn vào các tính chất của nó
Nhắc lại : $V(f)$ là tập nghiệm của đa thức $f$ còn $V(S)$ là tập nghiệm của hệ đa thức $S$ trong $k[X]$. Tập này còn được gọi là tập đại số
## Idean căn 
Cho $V$ là một tập điểm tùy ý trong $\mathbb{A}^n$. Kí hiệu 
$$
I_V:= \{f \in k[X]| \ f(a) = 0 \ \ , \forall a \in V\}
$$
Về ý nghĩa hình thức: $I_V$ là tập các đa thức nhận các điểm trong tập điểm $V$ làm nghiệm.
Có thể thấy ngay $I_V$ là idean và là idean lớn nhất có tập nghiệm chứa $V$. Ta gọi $I_V$ là idean của tập điểm $V$ trong $k[X]$. Nếu $V$ chỉ gồm một điểm $a$ thì ta dùng kí hiệu $I_a$. 

Ví dụ: $I_a = (x_1-\alpha_1,x_2-\alpha_2,...,x_n-\alpha_n)$ với mọi điểm $a=(\alpha_1,\alpha_2,...,\alpha_n)$. 
Thật vậy, dùng liên tiếp thuật toán Euclid thì ta có thể viết mọi đa thức $f \in k[X]$ dưới dạng:
$$
f = h_1(x_1-\alpha_1)+...+h_n(x_n-\alpha_n) + \alpha
$$
với $\alpha \in k$ thì $f(a)=0$ khi và chỉ khi $\alpha = 0$
Một ví dụ khác: Xét $V \subset \mathbb{A}^2$ là một tập vô hạn các điểm trên đường cong $x^3-y^2=0$ thì $I_V= (x^3-y^2)$. Ta chỉ cần chứng minh $I_V \subseteq (x^3-y^2)$. 
Coi mọi đa thức $f \in k[x,y]$ như là đa thức của biến $y$ với hệ số trong $k[x]$. Dùng thuật toán Euclid ta có thể viết: 
$$
f = h(x^3-y^2)+uy+v
$$
với $u,v \in k[x]$. Do $V \subset V(x^3-y^2)=\{(\alpha^2,\alpha^3) | \ \alpha \in k\}$  nên nếu $f \in I_V$ thì $f(\alpha^2, \alpha^3)=u(\alpha^2)\alpha^3+v(\alpha^2)$ với mọi $\alpha$ thuộc vào một tập vô hạn trong $k$. Từ đây suy ra $u(x^2)x^3+v(x^2) = 0$. Do đa thức $u(x^2)x^3$ chỉ chứa các đơn thức bậc lẻ và đa thức $v(x^2)$ chỉ chứa các đơn thức bậc chẵn, nên ta phải có $u(x^2)x^3=0$ và $v(x^2)=0$. Từ đây suy ra $u=0$ và $v=0$. Do đó có điều phải chứng minh. 

Cho $V$ và $W$ là hai tập điểm tùy ý trong $\mathbb{A}^n$. Dễ thấy rằng $I_V \supseteq I_W$ nếu $V \subseteq W$ và 
$$
I_V \cap I_W = I_{V \cup W}
$$
Ta biết rằng giao của các tập đại số chứa $V$ cũng là tập đại số. Đây là tập đại số nhỏ nhất chứa $V$, kí hiệu là $\overline{V}$. Ta gọi $\overline{V}$ là bao đóng của $V$. 
**Bổ đề.** Cho $W$ là một tập tùy ý trong $\mathbb{A}^n$. Ta có
a/ $\overline{W} = V(I_W)$
b/ $I_{\overline{W}} = I_W$

Nếu $J$ là tập đại số thì $\overline{J}=J$ và do đó $J=V(I_J)$. 
Tóm lại ta có hai mối quan hệ $J\rightarrow V(J)$ và $J \rightarrow I_J$ giữa các idean trong $k[X]$ và tập điểm trong $k^n$. Hai mối quan hệ này cho ta một mối tương ứng 1-1 giữa các tập đại số và các idean dạng $I_J$. 
$$
J \rightarrow I_J \rightarrow V(I_J)=J 
$$
Bây giờ ta sẽ chuyển hướng nghiên cứu sang các idean dạng $I_V$. Đầu tiên ta có định nghĩa về idean căn. 
**Định nghĩa.** Cho $I$ là một idean tùy ý trong vành $A$. Ta gọi tập tất cả các phần tử $f \in A$ có một lũy thừa $f^r \in I$ là căn của $I$, kí hiệu là $\sqrt{I}$ (radical ideal)

Ta sẽ chứng minh $\sqrt{I}$ là một idean.
Để chứng minh nó là idean thì nó cần đảm bảo hai tính chất. Một là với mỗi $f,g \in \sqrt{I}$ thì ta phải có $f+g\in \sqrt{I}$ và $hf \in \sqrt{I}$ với mỗi $h \in A$. 

Đầu tiên, với $f,g\in \sqrt{I}$ thì tồn tại $r,s$ sao cho $f^r,g^s\in I$. Khi đó 
$$
(f+g)^{r+s} = \sum_{i=1}^{r+s}\binom{r+s}{i}f^{r+s-i}g^i
$$
Rõ ràng $r+s-i\geq r$  hoặc $i \geq s$ cho nên $f^{r+s-i}g^i$ chia hết cho $f^r$ hay $g^s$ với mọi $i$. Suy ra $(f+g)^{r+s}\in I$ cho nên $f+g\in \sqrt{I}$ . Còn $hf \in \sqrt{I}$ làm tương tự.

**Bổ đề.** $I_V$ là idean căn.
Chứng minh: Nếu $f^r\in I_V$ thì $f^r(a)=0$ với mọi $a\in V$. Suy ra $f(a)=0$ với mọi $a\in V$ và do đó $f\in I_V$.  (một đa thức bậc hữu hạn thì không thể có vô hạn nghiệm).

**Lưu ý:** Không phải idean căn nào trong $k[X]$ cũng là idean của một tập đại số. Giả sử $k[X]$ chứa một idean $I \neq k[X]$ vô nghiệm. Khi đó $\sqrt{I}$ cũng vô nghiệm. Nếu $\sqrt{I}=I_V$ là idean của một tập đại số $V$ nào đó thì ta phải có $V =\emptyset$ .  Suy ra $I_V=I_\emptyset=k[X]$ tức là  $1\in I$ và suy ra $I = k[X]$ là mâu thuẫn. 

Cho $I$ là idean thực sự của vành $A$. Ta gọi $I$ là một idean cực đại nếu $I$ không nằm trong một idean thực sự nào khác của $A$. 
Với mọi chuỗi tăng các idean thực sự $I_1 \subseteq I_2 \subseteq I_2 \subseteq... \subseteq I_j \subseteq ...$ ta thấy $\bigcup I_j$ cũng là một idean thực sự. Vì vậy ta có thể áp dụng bổ đề Zorn để thấy mọi idean thực sự đều nằm trong ít nhất một idean cực đại.

Ví dụ: $I_a = (x_1-\alpha_1,...,x_n-\alpha_n)$ là idean cực đại trong $k[X]$. 
Từ nhận xét ở trên thì ta biết được rằng $f = \sum_{i=1}^{n} h_i(x_i-\alpha_i)+\alpha$ với $\alpha \in k$ cho nên $\alpha \in (I_a,f)$ và nếu $f \notin I_a$ thì $\alpha \neq 0$ và do đó $(I_a,f) = k[X]$


Note: 
$(I,f)$ là idean sinh bởi $I$ và $f$ tức là tập các đa thức dạng $g+hf$ với $g \in I$ và $h\in R$ ). 

## Idean nguyên tố
Cho $I$ là idean thực sự của vành $A$ tức là $I \neq A$. Ta gọi $I$ là idean nguyên tố nếu từ $fg \in I$ suy ra được $f \in I$ hay $g\in I$ .



