---
title: Độc lập tuyến tính
---
Cho $E$ là một không gian vector và $S$ là một tập hợp con của $E$. Ta xét các vector có thể nhận được từ $S$ qua các phép cộng và nhân vô hướng
**Định nghĩa.** Một vector $x \in E$ được gọi là một tổ hợp tuyến tính của $S$ nếu $x$ có thể viết dưới dạng 
$$ 
x = a_1x_1+...+a_nx_n
$$
với $a_i \in K$ và $x_i \in S(i =1,...,n)$. Đặc biệt, vector 0 cũng được coi là một tổ hợp tuyến tính của tập rỗng $\emptyset$
Kể từ giờ ta sẽ dùng biểu thức $x = \sum_{i} a_ix_i \ (x_i \in S)$ để biểu thị một tổ hợp tuyến tính $x$ của $S$. 
Khái niệm tổ hợp tuyến tính có tính chất bắc cầu. Cụ thể ta có bổ đề sau đây.
**Bổ đề 1.** Cho $T$ là một hệ các vector của $E$. Nếu $x$ là một tổ hợp tuyến tính của $T$ và mọi vector của $T$ là một tổ hợp tuyến tính của $S$ ,thì $x$ cũng là một tổ hợp tuyến tính của $S$. 
*Chứng minh.*
Giả sử 
$$
\begin{array}{l}
x = \sum_{i}a_ix_i \ (x_i \in T) \\
x_i = \sum_{j}b_{ij}y_j \ (y_j \in S)
\end{array}
$$
Đặt $c_j = \sum_{i}a_ib_{ij}$ thì ta có $x = \sum_{j}c_jy_i$
Do chỉ có một số hữu hạn các phần tử $a_i$ và $b_{ij}$ khác không nên chỉ có một số hữu hạn $c_j$ khác không. 
**Định nghĩa.** Tập hợp tất cả các tổ hợp tuyến tính của $S$ được gọi là bao đóng tuyến tính của $S$, kí hiệu là $E_S$. 

**Bổ đề 2.** $E_S$ là không gian con nhỏ nhất của $E$ chứa $S$. 
*Chứng minh.*
Nếu $x$ và $y$ là hai tổ hợp tuyến tính của $S$ thì $x+y,ax$ với mọi $a \in K$ cũng là những tổ hợp tuyến tính của $S$. Vì vậy $E_S$ đóng đối với phép cộng và nhân vô hướng. 
Mà ta đã biết một tập $E_S$ thỏa mãn như vậy thì cũng là một không gian con của $E$. Do mọi phần tử của $E_S$ đều nhận được từ $S$ qua các phép nhân vô khương và phép cộng nên mọi không gian con chứa $S$ đều phải chứa $E_S$. Điều này cho thấy $E_S$ là không gian con nhỏ nhất chứa $S$. 
Từ khái niệm bao đóng tuyến tính ta có thể đưa ra khái niệm sau:
**Định nghĩa.** Tập $S$ được gọi là một hệ sinh của $E$ nếu mọi vector của $E$ đều là một tổ hợp tuyến tính của $S$ tức là $E = E_S$. 
Chẳng hạn, tập các vector $e_1,...,e_n$ là một hệ sinh của $K^n$. 
Để xác định một không gian vector, ta chỉ cần biết một hệ sinh. Từ đây nảy sinh ra vấn đề khi nào thì một hệ sinh là cực tiểu, có nghĩa là hệ đó không chứa một hệ sinh khác của không gian vector. 
Trước đó ta hãy xem xét mối quan hệ giữa các vector
**Định nghĩa.** Một ràng buộc $a_1x_1+...+a_nx_n = 0$ với $a_i\in K$ và $x_i \in S$ được gọi là một quan hệ tuyến tính của $S$. Quan hệ đó được gọi là không tầm thường nếu có ít nhất một hệ số $a_i \neq 0$. 
Tập $S$ được gọi là phụ thuộc tuyến tính nếu $S$ có một quan hệ tuyến tính không tầm thường.
Ta có thể thử sự phụ thuộc tuyến tính bằng tiêu chuẩn sau:

**Bổ đề 3.** Tập $S$ là phụ thuộc tuyến tính khi và chỉ khi $S$ có một vector là một tổ hợp tuyến tính của các vector khác. 
*Chứng minh.* 
Nếu $S$ là phụ thuộc tuyến tính thì $S$ có một quan hệ tuyến tính không tầm thường.
Ngược lại nếu có $x$ là một tổ hợp tuyến tính của các vector khác thì ta có thể suy ra $x-\sum_{i}a_ix_i =0$ là một quan hệ tuyến tính không tầm thường của $S$. Vì vậy $S$ là phụ thuộc tuyến tính.

**Định nghĩa.** Tập $S$ đuộc gọi là độc lập tuyến tính nếu nó không phụ thuộc tuyến tính, có nghĩa là từ mọi quan hệ tuyến tính dạng 
$$
a_ix_1+...+a_nx_n = 0
$$
với $x_i \in S$ ta suy ra được $a_i = 0, \forall i = 1,...,n$. 
Theo định nghĩa thì mội tập hợp con của một hệ độc lập tuyến tính cũng là độc lập tuyến tính. Dựa vào tính chất này ta có bổ đề sau để kiểm tra tính độc lập tuyến tính

**Bổ đề 4.** Giả sử $R$ và $T = R \cup \{x\}$ là hai tập hợp con trong $E, x\notin R$. Tập $T$ là tập độc lập tuyến tính khi và chỉ khi $R$ là tập độc lập tuyến tính và $x \notin E_R$. 

Tiếp theo ta giải quyết vấn đề xác định hệ sinh cực tiểu.
**Định lí 5.** Tập $S$ là một hệ sinh cực tiểu của $E_S$ khi và chỉ khi $S$ là độc lập tuyến tính.
*Chứng minh.*
Dựa vào định nghĩa thì $S$ là một hệ sinh cực tiểu của $E_S$ khi và chỉ khi $E_R \neq E_S$ với mọi tập con thực sự $R$ của $S$. Không làm mất tính tổng quát, ta chỉ xét các tập $R$ có dạng $\displaystyle R=S\backslash \{x\}$ với $x$ là một vector tùy ý của $S$. Khi đó $E_R \neq E_S$ khi và chỉ khi $x \notin E_R$, có nghĩa $x$ không là một tổ hợp tuyến tính của các phần tử khác của $S$. Theo bổ đề 3 thì $S$ là một hệ độc lập tuyến tính.


Tiếp theo: [[Tổng trực tiếp]]

