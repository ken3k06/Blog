## Pseudo-random functions and Permutations
Đối với các hệ mã đối xứng thì ta cần chú ý tới các thuật toán mã hóa cấp thấp, trong đó bao gồm PRF hay Pseudo-random functions. 
http://en.wikipedia.org/wiki/Cryptographic_primitive

Một PRF là một hàm mà trông có vẻ ngẫu nhiên đối với Adversary, hay nói cách khác thì Adversary không thể dự đoán được đầu ra của nó. 

Ta xem xét một security game như sau:
![[Pasted image 20250924213048.png]]
Đối với security game này, ta được cho một hàm $F:D \rightarrow C$ và Adversary cũng được biết thông tin về hàm này, tức là nó có thể truy vấn đầu vào và biết được đầu ra của hàm.
Nhiệm vụ của Challenger là chọn một cặp $(x,y)$ ngẫu nhiên trong trường hợp $b=0$ hoặc là $(x,F(x))$ trong trường hợp ngược lại để gửi cho Adversary. 
Nhiệm vụ của Adversary lúc này là đoán xem cặp giá trị được Challenger gửi tới là cặp giá trị ngẫu nhiên hay là cặp giá trị được tính bởi hàm $F$ trên. Bởi vì Adversary có được hàm $F$ cho nên nó có thể tính $x=F(x)$ để kiểm tra và xác nhận. 
Như vậy, Adversary trong security game trên khá "mạnh" vì nó có thể thắng gần như mọi game nếu biết được hàm $F$. 
Ngược lại, nếu như ta không cho Adversary biết thông tin về hàm $F$ thì security game sẽ trở nên vô nghĩa, vì mục đích của việc thiết kế security game nhằm kiểm tra mức độ an toàn của một scheme. Nếu như Adversary không biết bất cứ thông tin gì về scheme thì việc đánh giá cũng sẽ trở nên không có giá trị. 
Như vậy nếu ta vẫn muốn cho $\mathcal{A}$ biết thông tin về hàm $F$ thì cần thiết kế lại security game theo cách khác. 


Thay vì tập trung vào scheme mã hóa thì ta sẽ tìm cách phân phối các khóa $k$ cho scheme. Chẳng hạn thay vì chỉ có một hàm PRF là $F$ thì ta sẽ định nghĩa một họ các PRF là $\{F_k\}_K$.
Lúc này Adversary chỉ biết thông tin về họ các hàm này thay vì các key. 

![[Pasted image 20250924215019.png]]

Nhưng với cách định nghĩa này thì ta lại trao quá nhiều lợi thế cho Challenger. Chẳng hạn với họ các hàm có dạng $K = D = C = \{0,1\}^n$ và $F_k(x) = k\oplus x$ thì gần như bất khả thi cho Adversary để có thể thắng được game. 

Ta cần thiết kế lại game thêm một lần nữa. 
![[Pasted image 20250924215045.png]]
Ở phiên bản này, ta cho $\mathcal{A}$ thêm quyền được truy vấn.
Ta tạo một danh sách $\mathcal{L}$ để lưu các output được sinh ra bởi $F_k$. Điều này nhằm tránh xảy ra trường hợp $\mathcal{A}$ gọi truy vấn cùng một giá trị $x$ nhưng được trả về 2 đầu ra khác nhau. Nếu như điều trên xảy ra trong trường hợp $b=0$ thì $\mathcal{A}$ có thể xác định ngay được. 
Quan sát hình trên ta có thể thấy rằng: $\mathcal{A}$ có quyền truy vấn tới một Oracle $\mathcal{O}_{F_k}$. Oracle sau đó sẽ kiểm tra xem có tồn tại cặp giá trị $(x,y')$ trong $\mathcal{L}$ hay chưa. Nếu rồi thì nó sẽ trả về. 
Ngược lại nó sẽ sinh ra giá trị $y$ mới dựa vào một trong hai trường hợp.
- Nếu $b=0$ thì lấy $y \leftarrow C$
- Ngược lại lấy $y \leftarrow F_k(x)$
Cuối cùng cập nhật lại $\mathcal{L} \leftarrow \mathcal{L} \cup (x,y)$
Lúc này Advantage của $\mathcal{A}$ sẽ là:
$$
\text{Adv}^{PRF}_{\{F_k\}_K}(A) = 2 \cdot \left| \Pr[A^{\mathcal{O}_{F_k}}  \ \text{Wins}] - \frac{1}{2} \right|
$$
Hoặc ta có thể viết
$$
\text{Adv}^{PRF}_{\{F_k\}_K}(A) =\left|    \Pr[b'=1 \mid b=1] - \Pr[b'=1 \mid b = 0]   \right|
$$
Hai biểu thức trên là tương đương nhau về mặt ý nghĩa.
Tiếp theo ta có PRP - Pseudo-random permutation. 
Lúc này hàm $F$ của ta có dạng $F:D\rightarrow D$ và là một hàm song ánh. Như vậy để tranh việc Adversary phân biệt được giữa PRF và PRP thì ta có security game như sau:
![[Pasted image 20250924220811.png]]

## OWF and Trapdoor OWF
