---
title: Diffie Hellman Key Exchange
---
# Security Analysis
## Bit - guessing game
Ta nhắc lại một cách để tổng quát hóa các security game. Thay vì xác định hai thí nghiệm $b=0,1$ riêng biệt thì challenger sẽ chọn ngẫu nhiên một trong hai giá trị $b\in \lbrace0,1 \rbrace$ và chạy thí nghiệm $b$ tương ứng. Mục tiêu Adversary là phải đoán chính xác giá trị bit này với xác suất tốt hơn xác suất đoán ngẫu nhiên tức là $1/2$.
**Attack Game - Bit-gues**s**ing version of semantic security:** Với mỗi cipher $\mathcal{E} = (E,D)$ được xác định trên $(\mathcal{K},\mathcal{M}, \mathcal{C})$ và một adversary $\mathcal{A}$, attack games diễn ra như sau:
- $\mathcal{A}$ tính hai giá trị $m_0,m_1\in \mathcal{M}$ với độ dài bằng nhau và gửi tới challenger.
- Challenger tính: $b \xleftarrow{R} \{0,1\}, k\xleftarrow{R} \mathcal{K}, c\xleftarrow{R} E(k,m_b)$ và gửi $c$ tới cho Adversary.
- Adversary output một bit $b'\in \lbrace0,1\rbrace$.
$\mathcal{A}$ thắng nếu đoán đúng $b=b'$.
![[Pasted image 20250919205304.png]]
Advantage của adversary đối với modified game này sẽ là
$$ 
\text{SSadv}[\mathcal{A},\mathcal{E}] = | 2 \cdot Pr[W] - 1| 
$$

## CPA Security and CCA Security

Nhắc lại CPA Security: Adversary có quyền encrypt bất kì messages nào và sẽ cố gắng phân biệt giữa hai ciphertext. Cụ thể như sau

1. Attack Game - CPA Security: Với mỗi cipher $\mathcal{E} = (E,D)$ được xác định trên $(\mathcal{K},\mathcal{M}, \mathcal{C})$ và một adversary $\mathcal{A}$, ta định nghĩa hai thí nghiệm, thí nghiệm 0 và thí nghiệm 1. Tương ứng với mỗi $b = 0,1$ ta xác định
- Thí nghiệm $b$:
    - Challenger chọn một giá trị $k\xleftarrow{R}\mathcal{K}$
    - Adversary gửi các truy vấn tới challenger
    - Với mỗi truy vấn thứ $i$, adversary sẽ gửi cặp messages $m_{i0}, m_{i1}\in\mathcal{M}$ có độ dài bằng nhau
    - Challenger sẽ tính $c_{i} \xleftarrow{R} E(k,m_{ib})$ và gửi lại $c_i$ cho adversary
    - Adversary sẽ output một bit $b'\in \lbrace 0,1 \rbrace$

Với mỗi $b = 0,1$ ta kí hiệu $W_b$ là biến cố để $\mathcal{A}$ output $1$ trong thí nghiệm $b$. Ta định nghĩa lợi thế của adversay $\mathcal{A}$ trước $\mathcal{E} = (E,D)$ sẽ là

$$ \text{CPA}adv[\mathcal{A},\mathcal{E}] := \displaystyle | Pr[W_0]-Pr[W_1] \displaystyle | $$

Lưu ý rằng trong CPA attack games thì một key sẽ được dùng cố định trong suốt quá trình truy vấn và mã hóa. Như vậy, một hệ mật được định nghĩa là **CPA-Secure** nếu như với mọi Adversary $\mathcal{A}$ truy vấn hiệu quả thì giá trị $\text{CPA}adv[\mathcal{A},\mathcal{E}]$ là không đáng kể.

Một hệ mật là **CPA-Secure** thì nó cũng là một hệ mật không tất định (non-deterministic). Thật vậy, nếu như một hệ mật là tất định (deterministic), ta kí hiệu là $\mathcal{E} = (E,D)$.

Ta sẽ cài đặt một CPA - Adversary như sau. Với $m,m'$ là hai messages bất kì được chọn và chúng phân biệt nhau, $\mathcal{A}$ sẽ thực hiện 2 lần truy vấn tới challenger.

Lần truy vấn đầu tiên nó sẽ gửi tới server cặp giá trị $(m,m')$ và lần tiếp theo sẽ là $(m,m)$. Vì thuật toán là tất định nên ở hai lần trả về $c_1,c_2$ thì $\mathcal{A}$ sẽ lựa chọn output $1 \ \text{if} \ c_1=c_2$ và $0$ trong trường hợp ngược lại.

Ở đây mỗi experiment sẽ được định nghĩa khác nhau với mỗi bit $0$ và $1$. Thông thường challenger sẽ chọn ngẫu nhiên một trong hai thí nghiệm và mục tiêu của Adversary là đoán được challenger đang chạy thí nghiệm nào.

![[Pasted image 20250919205419.png]]

Tương tự ta cũng có **CCA-Secure** như dưới đây

1. Attack Game - CCA Security: Với mỗi cipher $\mathcal{E}=(E,D)$ được xác định trên $(\mathcal{K},\mathcal{M},\mathcal{C})$ và adversary $\mathcal{A}$ ta cũng xét hai thí nghiệm $b=0,1$ như sau:
- Thí nghiệm $b$:
    - Challenger chọn khóa $k \xleftarrow{R}\mathcal{K}$
    - $\mathcal{A}$ tạo các chuỗi truy vấn tới challenger. Mỗi truy vấn có thể rơi vào một trong hai loại:
        - Encryption Query: với mỗi $i = 1,2,...$ , truy vấn thứ $i$ gồm cặp tin nhắn $(m_{i0},m_{i1})\in\mathcal{M}^2$. Challenger sau đó sẽ tính $c_i \xleftarrow{R}E(k,m_{ib})$ và gửi $c_i$ về lại cho Adversary
        - Decryption Query: với mỗi $j=1,2,...$, truy vấn thứ $j$ gồm một ciphertext $c'_j\in\mathcal{C}$ mà không trùng với các ciphertext đã được trả về ở truy vấn encrypt.
        $$
        c_j'\notin \{c_1,c_2,...\} 
        $$
        - Challenger sau đó sẽ tính $m_j'\leftarrow D(k,c_j')$ và trả lại $m_j'$ cho $\mathcal{A}$.
    - $\mathcal{A}$ output một bit $b'\in \{0,1\}$

Tương tự ta cũng có $\text{CCA}adv[\mathcal{A},\mathcal{E}] := \displaystyle | Pr[W_0] - Pr[W_1] \displaystyle |$ và một hệ mật được gọi là **CCA-Secure** nếu như giá trị trên là không đáng kể.
![[Pasted image 20250919205528.png]]

# Semantic Security of ElGamal

**Định nghĩa 1 - CDH Assumption**: Xét nhóm hữu hạn sinh $\mathbb{G}$ với phần tử sinh $g$. Bài toán đặt ra là làm thế nào để tính được giá trị của $g^{ab}$ nếu như biết cặp giá trị $g^a,g^b$.
**Định nghĩa 2 - DDH Assumption**: Xét nhóm hữu hạn sinh $\mathbb{G}$ với phần tử sinh $g$. Bài toán đặt ra là làm thế nào để phân biệt được giữa $g^{ab}$ và một phần tử $g^{c}$ của nhóm. Giả định ta biết cặp giá trị $(g^a,g^b)$.
Elgamal Encryption là một lược đồ mã hóa dựa trên quá trình trao đổi khóa Diffie - Hellman. Bao gồm các thành phần như sau:
- một nhóm cyclic $\displaystyle \mathbf{G}$ với cấp là số nguyên tố $\displaystyle q$ và điểm sinh $\displaystyle g\in \mathbf{G}$.
- một symmetric cipher $\displaystyle \mathcal{E}{s} =( E{s} ,D_{s})$ được xác định trên $\displaystyle (\mathcal{K} ,\mathcal{M} ,\mathcal{C})$.
- một hàm băm mật mã $\displaystyle H:\mathbf{G}^{2}\rightarrow \mathcal{K}$

Ta kí hiệu hệ mật là $\displaystyle \mathcal{E}_{EG}$*. Message space cho $\displaystyle \mathcal{E}_{EG}$* là $\displaystyle \mathcal{M}$ và ciphertext space là $\displaystyle \mathbf{G} \times \mathcal{C}$. Tiếp theo ta xác định các hàm sinh khóa, mã hóa và giải mã cho lược đồ.

- Key generation algorithm:
    - $G():= \alpha \displaystyle \xleftarrow{R}\mathbb{Z}_{q}, u \displaystyle \leftarrow g^{\alpha}, \newline pk \leftarrow u, sk \leftarrow \alpha \newline \text{output} (pk,sk);$
- với mỗi public key $pk = u \in \mathbf{G}$ và mesage $m\in \mathcal{M}$, thuật toán mã hóa hoạt động như sau:
    - $E(pk,m) := \beta \xleftarrow{R} \mathbb{Z}_{q}, v \leftarrow g^{\beta}, w \leftarrow u^{\beta}, k\leftarrow H(v,w), c\leftarrow E_{s}(k,m)\newline \text{output(v,c)}$
- với mỗi secret key $sk = \alpha\in \mathbb{Z}_{q}$ và ciphertext $(v,c)\in \mathrm{G} \times \mathcal{C}$, thuật toán giải mã hoạt động như sau:
    - $D(sk,(v,c)):=w\leftarrow v^{\alpha}, k\leftarrow H(v,w), m \leftarrow D_s(k,c) \newline \text{output m }$
Phân tích: Lược đồ bắt đầu bằng việc khởi tạo các cặp $(pk,sk)$. Ở đây $pk = u = g^{\alpha}$ và $sk = \alpha$. Ta lựa chọn các cặp $(pk,sk)$ như trên dựa vào việc giải bài toán DLP trên các nhóm cyclic cấp nguyên tố là bài toán khó.
Để mã hóa một tin nhắn $m$ bằng public key $pk$ thì ta làm như sau: Đầu tiên ta chọn một số mũ $\beta$ bất kì. Tiếp theo ta tính $v=g^{\beta}, w=u^{\beta}$. Cặp giá trị này sẽ được đưa vào hàm hash để lấy đầu ra là khóa $k$. Khóa này sẽ đóng vai trò là khóa mã hóa/giải mã trong symmetric cipher, ví dụ là các mode của AES. Ciphertext sẽ được tính bởi
$$ 
c = E_s(k,m) 
$$

Để giải mã ta cần khôi phục lại khóa $k$. Người giữ $sk$ hoàn toàn làm được điều này bằng cách tính

$$
w = v^{\alpha} = (g^{\beta})^{\alpha} = g^{\alpha \times \beta} = u ^ {\beta} 
$$

Và từ giá trị của $v$ ở bước giải mã ta sẽ tính lại giá trị hash $H(v,w)$.
Phiên bản trên là phiên bản Hybrid Encryption cho Elgamal Scheme. Điểm khác biệt giữa nó và Textbook Elgamal đó chính là thay quá trình mã hóa message. bằng lược đồ thành quá trình trao đổi khóa và sẽ mã hóa tin nhắn bằng một Symmetric Scheme. Điều này giúp hạn chế một số vấn đề mà textbook Elgamal đang có. Cụ thể như sau:
**Lược đồ textbook Elgamal:**
Một nhóm đại số $\mathbb{G}$ với cấp là số nguyên tố $q$ và điểm sinh $g\in \mathbb{G}$
- Key generation algorithm:
    - $G:()= \alpha \xleftarrow{R} \mathbb{Z}_q, h = g^\alpha \newline pk \leftarrow h, sk \leftarrow \alpha \newline \text{output}(h,g)$ là public parameters
- với mỗi public key $pk$ và tin nhắn $m \in \mathbb{G}$ thuật mã hóa hoạt động như sau
    - $k \xleftarrow{R} \mathbb{Z}_{q}$, tính $c_1 = g^k, c_2 = m\cdot h^k = m \cdot g^{\alpha k} \newline \text{output}(c_1,c_2)$
- Để giải mã đầu tiên ta sẽ kiểm tra $c_1,c_2\in \mathbb{G}$ và sau đó sẽ tính $m=c_2\times c_1^{-\alpha} = m \times g^{\alpha k} \times g^{-k \alpha} = m$.

Một biến thể khác của scheme thay đổi bước mã hóa bằng cách lấy $c_2 = m \ \oplus \ H(h^k)$ trong đó $H : \mathbb{G} \rightarrow \{0,1\}^l$ là một hàm băm mật mã. Để tính chính xác lại ciphertext thì ta cần tính lại $c_1^\alpha$ và truy vấn vào hàm băm.
Tiếp theo ta có định lí sau đây:
**Định lí 1.** Bài toán **OWE - Security** đối với textbook ElGamal tương đương với bài toán **CDH** trong nhóm cyclic $\langle g \rangle$.
OWE là viết tắt của One Way Encryption tức là nếu biết ciphertext $c$ thì cũng “không thể” tính toán lại tin nhắn ban đầu là $m$ được.
_Proof._
Ta sẽ chứng minh kết quả cho các perfect oracle. Đầu tiên ta sẽ chỉ ra $\text {OWE-CPA} \leqslant _{R} \text{CDH}$. Xét $\mathcal{A}$ là một perfect oracle có thể giải quyết bài toán CDH với nhóm cyclic cấp nguyên tố như trên. Ta sẽ truy vấn $\mathcal{A}(g,h_A,c_2)$ để lấy về $u$ và giải $m=c_2 u^{-1}$.
Tương tự ta sẽ có $\text{CDH} \leqslant \text {OWE-CPA}$ với $\mathcal{A}$ là một perfect oracle nhận vào cặp public key $(g,h_A)$ và ciphertext $(c_1,c_2)$ và trả về message $m$. Ta sẽ dùng oracle này để giải bài **CDH**. ****
Xét một CDH Instance như sau $(g,g_1,g_2)$. Chọn một giá trị $c_2 \in \langle g \rangle$ ngẫu nhiên và truy vấn $\mathcal{A}(g,g_1,g_2,c_2)$ để lấy giá trị $m$. Trả về $c_2m^{-1}$ là kết quả của **CDH** **Instance**.
Tiếp theo ta sẽ chứng minh rằng textbook ElGamal không đảm bảo **OWE - Security** dưới adaptive **CCA Attacker** và cũng không thỏa mãn **IND - CCA Security**.
**Bổ đề.** Với $(c_1,c_2)$ là hai ciphertext ứng với textbook ElGamal và public key $(\mathbb{G},g,h)$. Giả sử $\mathcal{A}$ là một decryption oracle thì khi đó attacker bằng cách truy vấn $\mathcal{A}$ có thể tính được kết quả của cặp $(c_1,c_2)$.
_Proof._
Giả sử $\mathcal{A}$ là một perfect oracle thì khi truy vấn cặp giá trị $(c_1,c_2g = mgh^{k})$ ta sẽ thu lại được giá trị $m'=mg$. Lúc này ta có được $m=m'g^{-1}$.
Một cách để ngăn chặn attacks kiểu như trên đó là thêm vào MAC - Message Authentication Code
Tiếp theo ta sẽ phân tích lược đồ Hybrid Encryption của ElGamal và xem xét khi nào nó thỏa IND — CCA Security.

## KEM/DEM Paradigm

Mô hình KEM/DEM nhằm mục đích chia quá trình mã hóa thành hai phần

- KEM (key encapsulation mechanism) là cơ chế dùng khóa công khai để tạo ra và gửi đi một khóa đối xứng tạm thời (trao đổi khóa tĩnh) một cách an toàn.
- DEM (data encapsulation mechanism) là cơ chế mã hóa dữ liệu thực tế bằng cách sử dụng khóa đối xứng từ KEM. Thông thường, DEM sẽ sử dụng một scheme mã hóa đối xứng có xác thực như AEAD (Authenticated Encryption with Associated Data) để đảm bảo tính toàn vẹn và bảo mật.

Cơ chế đóng gói khóa KEM bao gồm các thuật toán sau:

- Một thuật toán xác suất, chạy trong thời gian đa thức $\text{KEM.KeyGen}$ với đầu vào là security parameter $1^\lambda$, trong đó $\lambda \in \mathbb{Z}_{\geq 0}$, output một cặp $(\text{pk,sk})$. Cấu trúc của public key và secret key tùy thuộc vào scheme mà ta đang sử dụng.
    Với $\lambda_{\geq 0}$ ta định nghĩa các không gian mẫu như sau
    $$ 
    \text{KEM.PKSpace}_\lambda := \{PK : (PK,SK) \xleftarrow{R} \text{KEM.KeyGen}(1^\lambda)\} \newline \text{KEM.SKSpace}_\lambda:=\{SK:(PK,SK) \xleftarrow{R} \text{KEM.KeyGen}(1^\lambda)\} 
    $$
    
    Kể từ bây giờ ta sẽ mặc định security parameters là $1^\lambda$
    
- Một thuật toán xác suất, chạy trong thời gian đa thức $\text{KEM.Encrypt}$ với đầu vào là $\text{PK}$ trong không gian khóa như trên cùng với security parameters và output một cặp giá trị $(K,\psi)$ trong đó $K$ là một khóa và $\psi$ là ciphertext
    Biết rằng:
    - $K$ có độ dài là $\text{KEM.KeyLen}(\lambda)$
    - Ciphertext là một bitstring
- Tương tự, hàm mã hóa $\text{KEM.Decrypt}$ với đầu vào là $\text{SK}$ từ không gian khóa, security parameters và ciphertext $\psi$. Output sẽ là khóa $K$ hoặc $\text{reject}$, kí hiệu $\perp$.
    

![[Pasted image 20250919205654.png]]
**Độ tin cậy**
Tương tự như **PKE**, **KEM** cũng cần phải được đảm bảo tính hợp lệ, tức là mỗi ciphertext hợp lệ phải được giải mã đúng về khóa gốc mà nó đã đóng gói.
Ta gọi một cặp pubkey/seckey $(\text{PK,SK}) \in [\text{KEM.KeyGen}(1^\lambda)]$ là không tốt nếu như có một cặp $(K,\psi) \in [\text{KEM.Encrypt}(1^\lambda,PK)]$, ta có $\text{KEM.Decrypt}(1^\lambda,\text{SK},\psi) \neq K$.
Nếu ta gọi $\text{BadKeyPair}_\text{KEM}(\lambda)$ là xác suất để hàm sinh khóa sinh ra một cặp khóa không tốt, thì lúc này yêu cầu của ta là làm sao để giá trị trên tăng không đáng kể theo $\lambda$.
**Security against Adaptive CCA**
Ta định nghĩa một security game cho **KEM - CCA**. Tương tự với các security game khác ta cũng sẽ có $\mathcal{A}$ là một adversary với đầu vào là security parameter $\lambda$.
- Stage 1: $\mathcal{A}$ truy vấn đến oracle sinh khóa. Key generation oracle sẽ tính $(\text{PK,SK}) \xleftarrow{R} \text{KEM.KeyGen}(1^\lambda)$ và trả về $\text{PK}$.
- Stage 2: Adversary tiếp tục thực hiện chuỗi truy vấn tới decryption oracle.
    Với mỗi truy vấn, adversary submits một ciphertext $\psi$ và oracle sẽ trả về giá trị của $\text{KEM.Decrypt}(1^\lambda,\text{SK},\psi)$
- Stage 3: Adversary truy vấn tới encryption oracle
    Oracle sẽ tính:
    $$
    (K^*,\psi ^*) \xleftarrow{R} \text{KEM.Encrypt}(1^\lambda,\text{PK}); K^+ \xleftarrow{R} \{0,1\}^l; \tau \xleftarrow{R} \{0,1\}; \newline \text{if} \ \tau = 0 \ \text{then} \ K^{\dagger} \leftarrow K^* \ \text{else} \ K^{\dagger} \leftarrow K^+
    $$
    trong đó $l$ là độ dài của khóa được quy định trong $\text{KEM}$ và phụ thuộc vào security parameter. Oracle trả về kết quả $(K^{\dagger}, \psi^*)$.
- Stage 4: Adversary truy vấn tới decryption oracle, submit một ciphertext $\psi$ với điều kiện $\psi \neq \psi ^*$
- Stage 5: $\mathcal{A}$ output một bit $\tau' \in \{0,1\}$
Ta định nghĩa

$$ 
\text{AdvCCA}_{\text{KEM},A}(\lambda)=|Pr[\tau' = \tau] - 1/2| 
$$
**KEM** an toàn trước Adaptive CCA nếu như giá trị trên tăng không đáng kể theo $\lambda$.
**KEM - DEM Framework**
Framework bao gồm 3 thành phần chính. Một lược đồ mã hóa đối xứng, một hàm sinh **MAC**, và một key derivation function $\text{kdf} : G\rightarrow \{0,1\}^l$. Vai trò của hàm $\text{kdf}$ đó là chuyển đổi một khóa bí mật chung thành một khóa giả ngẫu nhiên và được dùng cho hàm mã hóa đối xứng.
Một version kết hợp với Diffie - Hellman như sau với nhóm $\mathbb{F}_p^*$:
**Encapsulation**
- Chọn ngẫu nhiên một giá trị $0<r<|\mathbb{G}|$.
- Tính $h=g^r$.
- Tính $K=\text{kdf}(h_A^r)$
- Output $(h,K)$.
**Decapsulation**
- Tính $K'=\text{kdf}(h^a)$
- Output $K'$, trong đó $K'=\text{kdf}(h^a)=\text{kdf}((g^r)^a)=\text {kdf}(h_A^r) =K$
Hàm phân phối khóa $\text{kdf}$ thông thường sẽ được mô hình hóa như một random oracle.
### ElGamal in the random oracle model
Trường hợp đầu tiên: Ta có các thiết lập lí tưởng hóa như sau:
- $H:\mathbb{G}^2 \rightarrow\mathcal{K}$ là một random oracle
- $\mathbb{G}$ với giả định **CDH** là hard
- $\mathcal{E}_s$ là semantically secure
Với các thiết lập như trên ta có thể kết luận rằng $\mathcal{E}_{EG}$ là semantically secure.
_Proof._
Giả sử Adversary $\mathcal{A}$ biết được thông tin về cặp ciphertext $(v,c)$ trong đó $v=g^{\beta}$. Nếu như $H$ được cấu hình là một random oracle, thì cách duy nhất để Adversary có thể thu thập thông tin về khóa $k$ đó là làm sao truy vấn chính xác vào oracle $H$ với cặp giá trị $(v,w)$. Vì $H$ là random oracle nên ta không thể biết thêm thông tin gì về $H$ ngoại trừ việc trực tiếp truy vấn nó và quan sát đầu ra.

Để làm được điều đó, Adversary $\mathcal{A}$ phải tính đúng giá trị của cặp $(g^{\alpha},g^{\alpha \beta})$. Tuy nhiên, nếu $\mathcal{A}$ có thể làm được điều này thì đồng nghĩa nó có thể giải được bài toán **CDH** trên nhóm $\mathbb{G}$. Như vậy trừ khi adversary có thể giải được bài toán **CDH** hoặc nếu không, $k$ sẽ gần như random và semactic security của $\mathcal{E}_{EG}$ sẽ được suy ra trực tiếp từ security của $\mathcal{E}_s$.

Cụ thể, với mỗi semantic security $\mathcal{A}$ thực hiện truy vấn cho random oracle $H$ tương ứng với $\mathcal{E}_{EG}$ và truy vấn tối đa $Q$ lần, tồn tại một **CDH** Adversary $\mathcal{B}_{\text{cdh}}$ cho **Attack Game** - **CDH** và một SS (semantic security) $\mathcal{B}_s$ tương ứng cho cho **Attack Game - Semantic Security** với $\mathcal{E}_s$ trong đó $\beta_{\text{cdh}}$ và $\beta_s$ là các elementary wrappers của $\mathcal{A}$, chúng sẽ mô phỏng biến $\mathcal{A}$ thành adversary giải bài CDH hoặc $\mathcal{E}_s$. Lúc này ta có bất đẳng thức

$$ \text{SS}^\text{ro} \text{adv}[\mathcal{A},\mathcal{E}_{EG}] \leq 2Q \cdot \text{CDHadv}[\beta_{\text{cdh}}, \mathbb{G}]+ \text{SSadv}[\beta_s, \mathcal{E}_s] $$

Ở mỗi game ta sẽ xét $b$ là bit được output bởi challenger và $b'$ là bit được output bởi adversary.

Ta sẽ chứng minh bất đẳng thức trong phiên bản bit-guessing của mỗi security game tức là

$$ 
\text{SS}^\text{ro} \text{adv}^*[\mathcal{A},\mathcal{E}_{EG}] \leq Q \cdot \text{CDHadv}[\beta_{\text{cdh}}, \mathbb{G}]+ \text{SSadv}^*[\beta_s, \mathcal{E}_s]
$$

Bit - guessing version:
$$ 
\text{SS}^\text{ro} \text{adv}^*[\mathcal{A},\mathcal{E}_{EG}]= \ | Pr[b=b']- \displaystyle \frac{1}{2}| 
$$

**Bước khởi tạo:**

1. $\alpha, \beta \xleftarrow{R} \mathbb{Z}_{q}, u \leftarrow g^{\alpha}, v \leftarrow g^{\beta}, w \leftarrow g^{\alpha \beta}$
    Lập một bảng trống $M:\mathbb{G}^2 \rightarrow \mathcal{K}$
2. Tính $k\xleftarrow {R} \mathcal{K}, b\xleftarrow {R} \{0,1\}$  
3. Ánh xạ $M[v,w]\leftarrow k$
    Gửi public key $u$ tới cho Adversary $\mathcal{A}$.
Gửi truy vấn mã hóa cặp giá trị $(m_0,m_1)\in \mathcal{M}$:
4. $c \xleftarrow {R} E_s(k,m_b)$  
    Gửi $(v,c)$ lại cho $\mathcal{A}$.
Truy vấn vào random oracle $(v',w')\in \mathbb{G}^2:$
Nếu $(v',w')\notin Domain(M)$ thì gán $M[v',w'] \leftarrow \mathcal{K}$
Ngược lại thì trả về giá trị $M[v',w']$.
**Game 0:** $\mathcal{A}$ có thể truy vấn random oracle tùy ý nhưng chỉ được truy vấn đúng 1 lần vào Encryption Oracle, nếu không thì $\mathcal{A}$ có thể thử cả hai messages. Ở game trên thì $k$ được tạo ngẫu nhiên và $\mathcal{A}$ cần tính đúng $w'=v^\alpha$ và tủy vấn đến oracle để trả về $k$. Nếu $\mathcal{A}$ có thể làm được điều này thì đồng nghĩa với việc nó tính được $g^{\alpha \beta}$ và giải được bài CDH.

**Game 1:** Tương tự như game 0 nhưng lúc này ta không lưu lại $M[v,w]\leftarrow k$.
Lúc này ta gọi $Z$ là biến cố mà Adversary truy vấn đúng cặp $[v,w]$ trong Game 1. Game 0 và game 1 diễn ra giống hệt nhau trừ khi biến cố $Z$ xảy ra cho nên ta có:

$$ 
|Pr[W_0]-Pr[W_1]| \leq Pr[Z] 
$$

Nếu như $\mathcal{A}$ có thể tính được $w$ thì đồng nghĩa với việc nó tính được $g^{\alpha \beta}$ từ $(g^\alpha, g^\beta)$ như đã đề cập ở trên. Như vậy ta có thể xem $\mathcal{A}$ như một black box dùng để giải bài CDH. Cụ thể ta sẽ xây dựng một adversary $\mathcal{B}_{cdh}$ đóng vai trò là challenger của $\mathcal{A}$ và dựa vào $\mathcal{A}$ attack CDH games.
Xác suất để chọn trúng 1 truy vấn có chứa solution cho CDH là $Pr[Z]/Q$ trong đó $Q$ là số lần truy vấn.
## Tài liệu tham khảo

1 [A Graduate Course in Cryptography](https://crypto.stanford.edu/~dabo/cryptobook/BonehShoup_0_6.pdf)

[2] [Mathematics of Public Key Cryptography](https://www.math.auckland.ac.nz/~sgal018/crypto-book/main.pdf)

3 [Design and Analysis of Practical Public-Key Encryption Schemes Secure against Adaptive Chosen Ciphertext Attack](https://eprint.iacr.org/2001/108.pdf)

4 [A graduate course in cryptography](https://crypto.stanford.edu/~dabo/cryptobook/BonehShoup_0_6.pdf)
