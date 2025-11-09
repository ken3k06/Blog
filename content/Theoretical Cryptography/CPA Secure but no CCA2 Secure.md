Trong bài viết này mình sẽ trình bày lại các định nghĩa về CPA/CCA và một scheme thỏa CPA Secure nhưng không thỏa CCA2 Secure



## IND-CPA Secure

![[Pasted image 20251108172842.png]]

Nhìn vào lược đồ trên ta có thể hình dung IND-CPA Security game sẽ diễn ra như sau:
1. Đầu tiên Challenger $\mathcal{C}$ sẽ sinh ra khóa $k$ . Nếu scheme là mã hóa đối xứng thì Adversary $\mathcal{A}$ sẽ không biết thông tin về khóa $k$. Ngược lại nếu scheme là mã hóa bất đối xứng thì Adversary sẽ được biết thông tin về khóa công khai $pk$ trong cặp $k=(pk,sk)$. $k \leftarrow Gen(1^\lambda)$ trong đó $\lambda$ là security parameter.  
2. $\mathcal{A}$ được quyền truy vấn vào encryption oracle với đầu vào là các plaintext tự sinh $m_i$, trong đó $i \in poly(n)$ có nghĩa là $\mathcal{A}$ có khả năng truy vấn oracle trong thời gian đa thức. 
3. $\mathcal{C}$ sẽ mã hóa plaintext bằng $c_i \leftarrow Enc(k,m_i)$ và gửi về cho $\mathcal{A}$ 
4. Sau khi kết thúc query phase thì $\mathcal{A}$ sẽ gửi một cặp plaintext $m_0^{*},m_1^{*}$ tới $\mathcal{C}$ . 
5. $\mathcal{C}$ chọn ngẫu nhiên $\displaystyle b\xleftarrow{\$}\{0,1\}$ và mã hóa $c^{*} \leftarrow Enc(k,m_b^{*})$ rồi gửi lại cho $\mathcal{A}$. 
6. $\mathcal{A}$ sau đó tiếp tục được truy vấn vào oracle và gửi thêm các messages $m_i'$ khác. 
7. Cuối cùng $\mathcal{A}$ sẽ output ra một bit $b'$ và $\mathcal{A}$ thắng nếu như $b'=b$. 
Ở bước truy vấn sau này $\mathcal{A}$ không được gọi lại $m_0^{*},m_1^{*}$

Như vậy một scheme được gọi là CPA-Secure nếu như xác suất thắng cuộc của $\mathcal{A}$ đối với game trên là không quá đáng kể so với xác suất đoán ngẫu nhiên $1/2$ tức là 
$$
\Pr[A \ \text{wins}] \leq \frac{1}{2} + negl(\lambda)
$$
Với $\lambda$ là security parameter. 


## IND-CCA1/2 Secure

![[Pasted image 20251108175741.png]]


Tiếp theo ta có IND-CCA1 Security game
1. $\mathcal{C}$ sinh khóa $k \leftarrow Gen(1^\lambda)$  
2. Khác với IND-CPA thì ở IND-CCA1 game, Adversary $\mathcal{C}$ được quyền truy vấn tới cả 2 oracle là decryption oracle và encryption oracle. Cả hai đều được truy vấn giới hạn trong thời gian đa thức. 
	- Gửi $c_i,m_j$ và trả về $c_j, m_i$ 
	- $c_j \leftarrow Enc(k,m_j)$ 
	- $m_i \leftarrow Dec(k,c_i)$ 
3. Tiếp đó $\mathcal{A}$ gửi $m_0^{*},m_1^{*}$ và $\mathcal{C}$ chọn ngẫu nhiên $\displaystyle b\xleftarrow{\$}\{0,1\}$ và mã hóa $c^* \leftarrow Enc(k,m_b^{*})$ rồi trả về cho $\mathcal{A}$ 
4. Sau khi nhận $c^*$ thì $\mathcal{A}$ vẫn còn quyền truy vấn đến encryption oracle
5. Cuối cùng $\mathcal{A}$ sẽ output ra một bit $b'$ và thắng nếu như $b'=b$. 

Còn đối với IND-CCA2 thì ta sẽ có thêm quyền truy vấn vào decryption oracle nhưng không được truy vấn với ciphertext $c^{*}$ nhận được ở challenge phase. Nếu không thì $\mathcal{A}$ sẽ biết được đó là ciphertext của plaintext nào và security game trở nên vô nghĩa. 

![[Pasted image 20251108182441.png]]

 
## Textbook Elgamal 

Cho một nhóm cyclic hữu hạn $G$ và một phần tử sinh $g$. Quy trình trao đổi khóa Diffie-Hellman bắt đầu bằng việc hai người $A$ và $B$  sinh các giá trị bí mật $a,b$ và trao đổi các khóa $g^a,g^b$ cho nhau. Bằng cách này cả hai sẽ tính được khóa chung là $g^{ab}$. 
![[Pasted image 20251108215946.png]]

Để bẻ khóa giao thức truyền khóa như trên thì ta phải tìm được một thuật toán hiệu quả nhằm tính được giá trị $g^{ab}$ từ cặp khóa $(g^a,g^b)$.
Có hai giả định được đặt ra. 
Đầu tiên là CDH - Computational Diffie-Hellman Assumption
Giả định này phát biểu rằng không tồn tại một thuật toán hiệu quả nào để tính $g^{ab}$ từ $g^a$ và $g^b$. Tức là với mọi PPT (probabilistic polynomial time) Adversary $\mathcal{A}$ thì 
$$
\Pr[A(g^x,g^y)=g^{xy}:x,y \leftarrow \mathbb{Z}_q] = negl(n)
$$
Tiếp theo ta có DDH - Decisional Diffie-Hellman Assumption
Giả định này phát biểu rằng không tồn tại một thuật toán hiệu quả có thể phân biệt được giữa 2 bộ $(g^x,g^y,g^{xy})$ và $(g^x,g^y,g^z)$ với $z \leftarrow \mathbb{Z}_q$ được sinh ngẫu nhiên. 

Bây giờ ta sẽ xem xét lược đồ của thuật toán Elgamal Textbook, được xây dựng dựa trên độ khó của bài toán loga rời rạc.

**Textbook Elgamal**
**KeyGen**: Đầu vào là security parameter $1^\lambda$ và output $(\mathbb{G},q,g)$ với $\mathbb{G}$ là một nhóm cyclic, có cấp là $q$ và phần tử sinh là $g$. Sau đó chọn một $x \leftarrow \mathbb{Z}_q$ ngẫu nhiên và tính $h=g^x$. Output public key sẽ là  $(\mathbb{G},q,g,h)$ và private key là $(\mathbb{G},q,g,x)$. Mesage space sẽ là $\mathbb{G}$. 
**Enc**: Với message $m \in \mathbb{G}$, và public key $(\mathbb{G},q,g,h)$: 
--> Chọn một giá trị $y \in \mathbb{Z}_q$ ngẫu nhiên và tính cặp ciphertext là $(g^y,h^y \times m)$ 
**Dec**: Với ciphertext $(\mathbb{G},q,g,x)$ và cặp ciphertext $(g^y,h^y \times m)=(c_1,c_2)$: 
--> Tính $c_1^{-x}$ và tính $m=c_2 \times c_1^{-x} = g^y \times h^{-(xy)} \times m = g^{y} \times g^{x-x-y} \times m = m$


Tiếp theo ta sẽ chứng minh lược đồ trên là CPA-Secure nếu như $\mathbb{G}$ thỏa mãn DDH Assumption.

Trước tiên ta có một bổ đề như sau: 
**Bổ đề:** Cho $\mathbb{G}$ là một nhóm hữu hạn và $m \in \mathbb{G}$ ngẫu nhiên. Chọn $k$ đều trên $\mathbb{G}$, tức là mỗi phần tử đều có xác suất được chọn là như nhau và đặt $k' := k \times m$. Khi đó với mỗi $g' \in \mathbb{G}$ thì ta có 
$$
\Pr[k \times m = g'] = 1/|\mathbb{G}|
$$
Chứng minh đơn giản như sau: 
Chọn $g'\in \mathbb{G}$ là một phần tử ngẫu nhiên. Khi đó tồn tại duy nhất một giá trị $k$ sao cho $k = g' \times m^{-1}$ 
$$
\Pr[k \times m =g'] = \Pr[k = g'\times m^{-1}]
$$
Do $k$ được chọn đều trên $\mathbb{G}$ cho nên xác suất để nó bằng với một phần tử bất kì trong $\mathbb{G}$ cũng đúng bằng $1/|\mathbb{G}|$.

Bây giờ ta sẽ chứng minh CPA-Secure của Textbook Elgamal

Ta gọi $\Pi$ là Elgamal scheme gốc và $\displaystyle \overset{\sim }{\Pi }$ là biến thể của nó trong đó cặp ciphertext output sẽ là 
$$ 
(g^y, g^z\times m)
$$
trong đó $y,z$ là các giá trị ngẫu nhiên. 
Ta cần chứng minh rằng kết quả sau đối với $\Pi$ 
$$
\displaystyle \Pr\left[ Pub_{\mathcal{A} ,\Pi }^{IND-CPA}( n) =1\right] \leqslant \frac{1}{2} +negl( n)
$$
![[Pasted image 20251108225904.png]]


Bây giờ từ bổ đề ở trên thì ta có được 
$$
\displaystyle \Pr\left[ Pub_{\mathcal{A} ,\overset{\sim }{\Pi } }^{IND-CPA}( n) =1\right] = \frac{1}{2}
$$
Vì phân bố của $g^y$ và $g^z\times m$ là phân bố đều trên $\mathbb{G}$ và không phụ thuộc vào $m$ cho nên xác suất để Adversary có thể phân biệt được giữa hai ciphertext của $m_0$ và $m_1$ chính là xác suất khi ta đoán ngẫu nhiên $1/2$. 

Từ đây ta sẽ xây dựng một DDH Challenger, có subroutine là adversary $\mathcal{A}$ đối với CPA Challenger. 

![[Pasted image 20251108231020.png]]



DDH Challenger: 
- Sinh ra các giá trị $(\mathbb{G},q,g,g^x,g^y,h)$ trong đó $h$ sẽ rơi vào 1 trong 2 trường hợp ngẫu nhiên như sau: Chọn $c \leftarrow \{0,1\}$ 
	- Nếu $c=0$ thì $h=g^{xy}$ 
	- Nếu $c=1$ thì $h=g^{z}$ với $z \leftarrow \mathbb{Z}_q$ ngẫu nhiên
Tiếp đó các phase diễn ra như sau: 

- DDH Challenger, ta kí hiệu là $\mathcal{D}$ gửi các giá trị $(\mathbb{G},q,g,g^x,g^y,h)$ đến cho $B$. Trong đó $B$ là CPA-Challenger đối với Adversary $\mathcal{A}$.
- $B$ gửi "public key" của mình là $(\mathbb{G},q,g,g^x)$ đến $\mathcal{A}$. 
- $\mathcal{A}$ gửi cặp plaintext $m_0,m_1$ đến $B$. 
- $B$ tạo cặp ciphertext $c_1 = g^y, c_2 = m_b \times h$ với $b \leftarrow \{0,1\}$ được chọn ngẫu nhiên, sau đó gửi tới cho $\mathcal{A}$. 
- $\mathcal{A}$ sau đó output ra $b'$ và trả về cho $B$. 
- Nếu $b'=b$ thì $c'=0$ , ngược lại $c'=1$. Sau đó $B$ gửi lại $c'$ cho $\mathcal{D}$ 
Ta có:
$$
\begin{array}{l}
\Pr[B \ \text{win DDH}] = \Pr[B \ \text{win DDH} \ | \ c=0]\Pr[c=0] + \Pr[B \ \text{win DDH}\ | \ c =1]\Pr[c=1]\\ 
= 1/2\Pr[c'=0 \ | \ c=0 ] + 1/2\Pr[c'=1 \ | \ c=1]
\\
=1/2\Pr[\mathcal{A} \ \text{win CPA}\ | \ c= 0] + 1/2\Pr[\mathcal{A} \ \text{win CPA}\ | \ c = 1 ] \\ 
= (1/2)(1/2+Adv(\mathcal{A} )) + (1/2)(1/2)\\
= 1/2 + 1/2 \times Adv(\mathcal{A})
\end{array}
$$
Trong đó 

$$
Adv(\mathcal{A}) =  |\Pr[A \ \text{wins}] -\frac{1}{2}| \leq negl(\lambda)
$$
đối với IND-CPA Game. 
Nếu như $\mathcal{A}$ có thể thắng IND-CPA Game với xác suất đáng kể (non-negl) thì $Adv(B)$ đối với DDH Game cũng là đáng kể. Điều này mâu thuẫn với giả định DDH của $\mathbb{G}$.
Vì ta có 
$$
Adv(B)=|\Pr[B \ \text{win DDH}] - 1/2| = 1/2 \times Adv(\mathcal{A}) 
$$

Ngoài ra, bằng việc dùng bổ đề ở trên thì ta có thể kết luận rằng: 
$$
\Pr[\mathcal{A} \ \text{win CPA}\ | \ c = 1 ] = 1/2
$$
Tức là trong trường hợp $h=g^z$ với $z$ là ngẫu nhiên thì $\mathcal{A}$ không thể phân biệt được 2 ciphertext tốt hơn so với đoán ngẫu nhiên. 


## Tài liệu tham khảo
- https://inst.eecs.berkeley.edu/~cs161/su19/lectures/lec05_symmetric.pdf
- https://www.isec.tugraz.at/wp-content/uploads/teaching/mpkc/2022/L2-pke.pdf
- https://people.csail.mit.edu/alinush/cse508-spring-2011/03-03-cpa-and-cca.pdf
