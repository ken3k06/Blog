---
title: Các khái niệm cơ bản
---
Vào một ngày đẹp trời mình quyết định học lại đại số tuyến tính <3, sau khi nhận ra môn này cực kì quan trọng nếu muốn học sâu hơn sau này.
Thật ra nếu mọi người để ý kĩ thì trong đại số trừu tượng có một số tính chất mà ta có thể liên hệ qua đại số tuyến tính.
## Không gian vector
Các vector trong hình học là những đoạn thẳng định hướng trong không gian. Hai đoạn thẳng định hướng xác định cùng một vector nếu chúng có cùng độ dài và hướng. Các vector thường được kí hiệu là các mũi tên. Đuôi của mũi tên được gọi là điểm gốc, còn đầu của mũi tên là điểm ngọn. Phép cộng các vector trong hình học có các tính chất sau:
	A1. $(x+y)+z=x+(y+z)$ (luật kết hợp)
	A2. $x+y=y+x$ (luật giao hoán)
	A3. Tồn tại một vector gọi là vector $0$ thỏa mãn $x+0=0+x=x$ với mọi vector $x$
	A4. Mọi vector $x$ có vector đối $-x$ thỏa mãn $x+(-x)=0$. 
Ngoài ra ta còn có phép nhân một số thực $c$ với một vector $x$.
Tích này có các tính chất sau với mọi số thực $a,b$ và vector $x$:
	B1. $(ab)x = a(bx)$ (luật kết hợp)
	B2. $(a+b)x = ax+bx$ (luật phân phối trái)
	B3. $a(x+y) = ax+ay$ (luật phân phối phải)
	B4. $1x = x$
Khái niệm niệm vector còn có rất nhiều ứng dụng khác và bây giờ nhiệm vụ của ta là khái quát hóa khái niệm vector.
Cho $K$ là một trường. Bây giờ ta sẽ định nghĩa một không gian vector $E$ trên $K$ là một tập hợp có hai phép toán:
- Phép cộng vector xác định cho mỗi cặp phần tử $x,y \in E$ một phần tử thuộc $E$ kí hiệu là $x+y$. Phép cộng này thỏa mãn các điều kiện A1-A4 
- Phép nhân vô hướng xác định cho mỗi cặp phần tử $a\in K$ và $x \in E$ một phần tử thuộc $E$ được kí hiệu là $ax$. Phép nhân này thỏa mãn các điều kiện của B1-B4, trong đó $a,b$ là những phần tử tùy ý và 1 là phần tử đơn vị của $K$.
Các điều kiện A1-A4 và B1-B4 được gọi là hệ tiên đề của không gian vector. 
Các phần tử của không gian vector $E$ được gọi là một vector. Còn các phần tử của $K$ được gọi là phần tử vô hướng. Phép cộng một vector với phần tử đối của một vector khác được gọi là phép trừ. 

**Bổ đề 1.** 
i/ Vector $0$ được xác định một cách duy nhất
ii/ Vector đối $-x$ được xác định một cách duy nhất
iii/ $x+y =z$ thì $x=z-y$  (luật chuyển vế)
iv/ Nếu $x+y = x+z$ thì $y=z$ (luật giản ước)
**Bổ đề 2.** 
i/ $cx=0$ khi và chỉ khi $c=0$ hoặc $x=0$
ii/ $ax=bx$ suy ra $a=b$ nếu $x \neq 0$
iii/ $cx = cy$ suy ra $x=y$ nếu $c\neq 0$
iv/ $(-c)x = c(-x) = -cx$

**Định nghĩa.** Một tập con không rỗng $E'$ của $E$ được gọi là một không gian con của $E$ nếu $E'$ cũng là một không gian vector với các phép cộng và phép nhân vô hướng của $E$. 

Tập $\{0\}$ chỉ gồm vector không bao giờ cũng là một không gian con và được kí hiệu là $0$. 
Không gian con lớn nhất của $E$ là $E$. 
Không gian con đòi hỏi phép cộng vector và phép nhân vô hướng phải được xác định trong $E'$, có nghĩa là:
$$ 
\begin{array}{l}
x+y \in E', \forall x,y \in E' \\
ax \in E', \forall a \in K,x \in E'
\end{array}
$$
Nếu $E'$ thỏa mãn các điều kiện trên thì ta nói $E'$ đóng với các phép cộng và phép nhân vô hướng của $E$. 

**Bổ đề 3.** Một tập con không rỗng $E' \subseteq E$  là một không gian con của $E$ khi và chỉ khhi $E'$ đóng với các phép cộng và phép nhân vô hướng của $E$. 
**Bổ đề 4.** Nếu $\{E_i\}$ là một họ các không gian con của $E$ thì giao $\cap E_i$ cũng là một không gian con của $E$. 
Tiếp theo ta có khái niệm [[Độc lập tuyến tính]]
 
