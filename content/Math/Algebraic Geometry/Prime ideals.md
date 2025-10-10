Trước đó ở bài [[Ideal and Gröbner Basis]] mình có nhắc qua khái niệm về Idean. Ở bài viết này mình sẽ đi sâu hơn vào các tính chất của nó

## Idean căn 
Cho $V$ là một tập điểm tùy ý trong $\mathbb{A}^n$. Kí hiệu 
$$
I_V:= \{f \in k[X]| \ f(a) = 0 \ \ , \forall a \in V\}
$$
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


