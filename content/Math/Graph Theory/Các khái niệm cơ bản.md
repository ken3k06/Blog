## Đồ thị

**Định nghĩa 1.** Đồ thị $G=(V,E)$ gồm hai tập hữu hạn, tập đỉnh $V$ gồm các phần tử được gọi là đỉnh của đồ thị và tập cạnh $E$ gồm các cặp không sắp thứ tự $(u,v)$ trong đó $u,v$ là hai đỉnh của $G$. Cặp $(u,v)$ được gọi là cạnh của $G$ với hai đầu mút $u,v$.
Tiếp theo ta gọi $|V|=n$ là bậc của đồ thị và $|E|=m$ là kích thước của đồ thị.
Thông thường, ta biểu diễn các đỉnh của đồ thị bằng tập các điểm trên mặt phẳng còn các cạnh được biểu diễn bởi đường thẳng nối hai đầu mút. Có một số trường hợp đặc biệt:

- Hai cạnh có chung đầu mút được gọi là hai cạnh song song
- Cạnh có hai đầu mút trùng nhau được gọi là khuyên

Đồ thị đơn là đồ thị không chứa khuyên và cạnh song song nào. Đồ thị không phải đồ thị đơn thì được gọi là đa đồ thị.

**Định nghĩa 2.** Cho đồ thị $G$ với các định $v_1,v_2,...,v_n$ và dãy bậc $d(v_1),d(v_2),...,d(v_n)$ được sắp xếp theo thứ tự giảm dần. Ta kí hiệu bậc nhỏ nhất và bậc lớn nhất của $G$ bởi $\delta(G)$ và $\Delta(G)$

Khi tất cả các đỉnh có bậc là $d$ tức là $\delta(G)=\Delta(G)$ thì ta gọi $G$ là đồ thị đều bậc $d$ và kí hiệu là $K_d$.
![[Pasted image 20251009155318.png]]
Ví dụ ta có một đồ thị đều bậc 2 như trên.

**Định lý 3.** Cho đồ thị $G=(V,E)$ với $n$ đỉnh $v_1,v_2,...,v_n$ và $m$ cạnh. Khi đó

$$ \sum_{i=1}^n d(v_{i})=2m $$

Kết quả trên còn được gọi là **bổ đề bắt tay.**

**Định nghĩa 4.** Đồ thị có hướng $G=(V,E)$ gồm hai tập hữu hạn, tập đỉnh $V$ gồm các phần tử được gọi là đỉnh của đồ thị và tập cạnh có hướng $E$ gồm các cặp có thứ tự $(u,v)$ trong đó $u,v$ là hai đỉnh của $G$. Cặp $(u,v)$ được gọi là cạnh có hướng đi từ $u$ tới $v$.

Để tính bậc của một đỉnh $v$ của đồ thị có hướng thì ta sẽ lấy tổng của bậc ra và bậc vào. Bậc ra là số lượng các đỉnh mà có đường đi trực tiếp từ $v$ tới (tức là đường đi không đi qua đỉnh nào khác). Tương tự với bậc vào. Như vậy

$$ d(v)=d^{+}(v)+d^{-}(v) $$

Tương tự ta cũng có bổ đề bắt tay cho đồ thị có hướng

**Định lí 5.** Cho đồ thị có hướng $G=(V,E)$. Ta có

$$ \sum_{v\in G}d^{+}(v)=\sum_{v\in G}d^{-}(v)=|E| $$

**Định lí 6.** Đồ thị $G_1=(V_1,E_1)$ được gọi là đẳng cấu với đồ thị $G_2=(V_2,E_2)$ nếu có một song ánh $f$ từ tập đỉnh $V_1$ vào tập đỉnh $V_2$ sao cho $(u,v)$ là cạnh của $G_1$ khi và chỉ khi $(f(u),f(v))$ là cạnh của $G_2$.
![[Pasted image 20251009155339.png]]
Quan hệ đẳng cấu là quan hệ tương đương. Nó thỏa mãn ba tính chất phản xạ, đối xứng và bắc cầu.

**Định nghĩa 7.** Cho hai đồ thị $G=(V,E)$ và $G_1=(V_1,E_1)$. Ta nói $G_1$ là đồ thị con của $G$ nếu $V_1 \subseteq V$ và $E_1\subseteq E$. Khi hai tập cạnh và đỉnh trùng nhau thì ta nói $G_1$ bao trùm $G$.

**Định nghĩa 8.** Giả sử $G_1=(V_1,E_1)$ là đồ thị con của $G=(V,E)$ sao cho với mọi $u,v\in V_1, (u,v)\in E_1$ khi và chỉ khi $(u,v)\in E$. Khi đó, $G_1$ được gọi là đồ thị con cảm sinh (induced graph) của $G$ trên tập đỉnh $V_1$ và kí hiệu $G[V_1]$.

Như vậy đồ thị cảm sinh có thể coi là trường hợp đặc biệt của đồ thị con.

**Định nghĩa 9.** Đồ thị đầy đủ bậc $n$, kí hiệu là $K_n$, là đồ thị gồm $n$ đỉnh đôi một kề nhau.

![[Pasted image 20251009155351.png]]
**Định nghĩa 10.** Cho đồ thị $G=(V,E)$. Nếu tập đỉnh $V$ của $G$ có thể được phân hoạch thành hai phần $V_1$ và $V_2$ khác rỗng, tức là $V=V_{1} \cup V_{2} ,V_{1} \cap V_{2} =\emptyset$ , sao cho mỗi cạnh của $G$ có một đầu mút thuộc $V_1$ và đầu mút còn lại thuộc $V_2$ thì $G$ được gọi là đồ thị hai phần hay đồ thị lưỡng phân (định nghĩa tương tự cho đồ thị $k$ - phân). Kí hiệu $G=(V_1,V_2,E)$.
![[Pasted image 20251009155427.png]]

Tương tự với đồ thị đầy đủ thì ta cũng có đồ thị lưỡng phân đầy đủ.

**Định nghĩa 11.** Đồ thị lưỡng phân đầy đủ là một đồ thị lưỡng phân thỏa mãn tính chất

$$ E=\{(v_1,v_2) \mid v_1 \in V_1, v_2 \in V_2\} $$

Kí hiệu $K_{m,n}$ trong đó $| V_1| = m, |V_2|=n$.

**Định nghĩa 12.** Một hành trình từ $v_0$ đến $v_k$ trong $G$ là một dãy hữu hạn

$$ W=(v_0,e_1,v_1,e_2,...,v_{k-1},e_k,v_k) $$

trong đó $v_i\in V, e_i\in E$ với hai đầu mút của $e_i$ là $v_{i-1}$ và $v_i$.

- Nếu các đỉnh trong hành trình là phân biệt thì $W$ được gọi là một đường đi.
- Đường đi khép kín với đỉnh đầu và đỉnh cuối trùng nhau được gọi là chu trình.
- Ta kí hiệu đường đi $n$ đỉnh bởi $P_n$ và chu trình là $C_n$.

**Định nghĩa 13.** Hai đỉnh $u,v$ của đồ thị $G$ được gọi là liên thông nếu như có một đường đi từ $u$ đến $v$ trong $G$. Đồ thị $G$ được gọi là liên thông nếu như hai đỉnh bất kì của $G$ là liên thông.

Dễ dàng kiểm tra được quan hệ liên thông giữa các đỉnh của một đồ thị $G$ là quan hệ tương đương. Do đó tập đỉnh của $G$ sẽ được phân thành các lớp tương đương theo quan hệ liên thông. Các lớp tương đương này được gọi là các thành phần liên thông của $G$. Rõ ràng, đồ thị $G$ được gọi là đồ thị liên thông nếu như chỉ có một thành phần liên thông.

Tiếp theo ta sẽ nhắc lại không chứng minh một tính chất quan trọng của đồ thị hai phần

**Định lí 14.** Đồ thị $G$ là đồ thị hai phần khi và chỉ khi mọi chu trình có độ dài chẵn, tức nó không chứa chu trình độ dài lẻ.

Một số định lí và khái niệm về đường đi/chu trình

**Định lí 15.** Đồ thị liên thông $G$ có một hành trình khép kín $W$ đi qua tất cả các cạnh, mỗi cạnh đúng một lần, khi và chỉ khi tất cả các đỉnh của $G$ có bậc chẵn. Hành trình $W$ như vậy được gọi là hành trình Euler của $G$. Trường hợp này ta gọi $G$ là đồ thị Euler.

**Định nghĩa 16.** Chu trình Hamilton của đồ thị $G$ là một chu trình đi qua tất cả các đỉnh của $G$. Còn đường đi Hamilton của $G$ cũng là đường đi qua tất cả các đỉnh của $G$.

Trong khuôn khổ bài viết, mình sẽ không nhắc lại các định lí và điều kiện tồn tại đường đi Hamilton ở đây (vì cũng không cần thiết lắm).

## Tài liệu tham khảo

[1] Lí thuyết đồ thị - Lê Anh Vinh