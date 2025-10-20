## Nhắc lại một số thứ
### AES-128

Trước tiên ta xem lại cách mà AES hoạt động. Phiên bản AES mà mình phân tích sẽ là AES-128 bit.
Tài liệu chính thức cho tiêu chuẩn mã hóa AES: https://nvlpubs.nist.gov/nistpubs/fips/nist.fips.197.pdf
![[Pasted image 20251003212819.png]]
Vì AES-128 thực hiện mã khóa trên từng khối có độ lớn 16 bytes cho nên ta sẽ biểu diễn plaintext bằng cách ánh xạ các kí tự sang một ma trận có kích thước là $4 \times 4$. Một ma trận như vậy sẽ được gọi là ma trận trạng thái. 

Tiếp theo ta có sơ đồ cho thuật toán như dưới đây:
![[Pasted image 20251003213055.png]]
**Bước 1.** Bước đầu tiên sẽ là add round key.
Ở bước này ta sẽ XOR từng phần tử của ma trận trạng thái với từng phần tử của round key. Round key ở đây là đầu ra của một bước gọi là KeyExpand. Ta sẽ bàn về bước này sau.
![[Pasted image 20251003213322.png]]
Sau khi kết thúc phép XOR thì ta thu được một ma trận kết quả mới làm đầu vào cho bước tiếp theo.

**Bước 2.** SubBytes
Ở bước này ta sẽ thay thế từng phần tử trong ma trận trạng thái bằng một phần tử khác trong một bảng gọi là SBox
![[Pasted image 20251003213932.png]]
![[Pasted image 20251003213938.png]]
Bảng này đảm bảo mỗi byte sẽ được ánh xạ tới 1 byte duy nhất (song ánh). Cho nên ta có thể tạo một bảng tra cứu ngược để khôi phục lại ma trận trạng thái. 

**Bước 3.** ShiftRows
Chức năng ShiftRows thực hiện quay trái từng hàng của ma trận trạng thái, ngõ ra của SubBytes, theo byte với hệ số quay tăng dần từ 0 đến 3. Hàng đầu tiên có hệ số quay là 0 thì các byte được giữ nguyên vị trí. Hàng thứ hai có hệ số quay là 1 thì các byte được quay một byte. Hàng thứ ba quay hai byte và hàng thứ tư quay ba byte.
![[Pasted image 20251003214621.png]]

**Bước 4.** MixColumns
Chức năng MixColumns thực hiện nhân từng cột của ma trận trạng thái, ngõ ra của ShiftRows, với một ma trận chuyển đổi được quy định bởi chuẩn AES. 
![[Pasted image 20251003215003.png]]

Việc biến đổi mỗi cột của ma trận trạng thái được thực hiện bởi hai phép toán là $\times$ và $\oplus$ 
![[Pasted image 20251003215105.png]]



Toàn bộ Implement như sau:

```python
N_ROUNDS = 10

def bytes_to_matrix(text: bytes):
    assert len(text) == 16
    return [[text[4*c + r] for r in range(4)] for c in range(4)]

def matrix_to_bytes(matrix):
    out = []
    for c in range(4):
        for r in range(4):
            out.append(matrix[c][r])
    return bytes(out)

def add_round_key(s,k):
    assert len(s) == len(k)
    for i in range(len(s)):
        for j in range(len(s)):
            s[i][j]^=k[i][j]
    
s_box = (
    0x63, 0x7C, 0x77, 0x7B, 0xF2, 0x6B, 0x6F, 0xC5, 0x30, 0x01, 0x67, 0x2B, 0xFE, 0xD7, 0xAB, 0x76,
    0xCA, 0x82, 0xC9, 0x7D, 0xFA, 0x59, 0x47, 0xF0, 0xAD, 0xD4, 0xA2, 0xAF, 0x9C, 0xA4, 0x72, 0xC0,
    0xB7, 0xFD, 0x93, 0x26, 0x36, 0x3F, 0xF7, 0xCC, 0x34, 0xA5, 0xE5, 0xF1, 0x71, 0xD8, 0x31, 0x15,
    0x04, 0xC7, 0x23, 0xC3, 0x18, 0x96, 0x05, 0x9A, 0x07, 0x12, 0x80, 0xE2, 0xEB, 0x27, 0xB2, 0x75,
    0x09, 0x83, 0x2C, 0x1A, 0x1B, 0x6E, 0x5A, 0xA0, 0x52, 0x3B, 0xD6, 0xB3, 0x29, 0xE3, 0x2F, 0x84,
    0x53, 0xD1, 0x00, 0xED, 0x20, 0xFC, 0xB1, 0x5B, 0x6A, 0xCB, 0xBE, 0x39, 0x4A, 0x4C, 0x58, 0xCF,
    0xD0, 0xEF, 0xAA, 0xFB, 0x43, 0x4D, 0x33, 0x85, 0x45, 0xF9, 0x02, 0x7F, 0x50, 0x3C, 0x9F, 0xA8,
    0x51, 0xA3, 0x40, 0x8F, 0x92, 0x9D, 0x38, 0xF5, 0xBC, 0xB6, 0xDA, 0x21, 0x10, 0xFF, 0xF3, 0xD2,
    0xCD, 0x0C, 0x13, 0xEC, 0x5F, 0x97, 0x44, 0x17, 0xC4, 0xA7, 0x7E, 0x3D, 0x64, 0x5D, 0x19, 0x73,
    0x60, 0x81, 0x4F, 0xDC, 0x22, 0x2A, 0x90, 0x88, 0x46, 0xEE, 0xB8, 0x14, 0xDE, 0x5E, 0x0B, 0xDB,
    0xE0, 0x32, 0x3A, 0x0A, 0x49, 0x06, 0x24, 0x5C, 0xC2, 0xD3, 0xAC, 0x62, 0x91, 0x95, 0xE4, 0x79,
    0xE7, 0xC8, 0x37, 0x6D, 0x8D, 0xD5, 0x4E, 0xA9, 0x6C, 0x56, 0xF4, 0xEA, 0x65, 0x7A, 0xAE, 0x08,
    0xBA, 0x78, 0x25, 0x2E, 0x1C, 0xA6, 0xB4, 0xC6, 0xE8, 0xDD, 0x74, 0x1F, 0x4B, 0xBD, 0x8B, 0x8A,
    0x70, 0x3E, 0xB5, 0x66, 0x48, 0x03, 0xF6, 0x0E, 0x61, 0x35, 0x57, 0xB9, 0x86, 0xC1, 0x1D, 0x9E,
    0xE1, 0xF8, 0x98, 0x11, 0x69, 0xD9, 0x8E, 0x94, 0x9B, 0x1E, 0x87, 0xE9, 0xCE, 0x55, 0x28, 0xDF,
    0x8C, 0xA1, 0x89, 0x0D, 0xBF, 0xE6, 0x42, 0x68, 0x41, 0x99, 0x2D, 0x0F, 0xB0, 0x54, 0xBB, 0x16,
)
inv_sbox = [0] * 256
for idx, val in enumerate(s_box):
    inv_sbox[val] = idx 
def sub_bytes(s):
    for i in range(len(s)):
        for j in range(len(s)):
            s[i][j] = s_box[s[i][j]]

def inv_sub_bytes(s):
    for i in range(4):
        for j in range(4):
            s[i][j] = inv_sbox[s[i][j]]

def shift_rows(s):
    s[0][1], s[1][1], s[2][1], s[3][1] = s[1][1], s[2][1], s[3][1], s[0][1]
    s[0][2], s[1][2], s[2][2], s[3][2] = s[2][2], s[3][2], s[0][2], s[1][2]
    s[0][3], s[1][3], s[2][3], s[3][3] = s[3][3], s[0][3], s[1][3], s[2][3]


def inv_shift_rows(s):
    s[0][1], s[1][1], s[2][1], s[3][1] = s[3][1], s[0][1], s[1][1], s[2][1]
    s[0][2], s[1][2], s[2][2], s[3][2] = s[2][2], s[3][2], s[0][2], s[1][2]
    s[0][3], s[1][3], s[2][3], s[3][3] = s[1][3], s[2][3], s[3][3], s[0][3]


# learned from http://cs.ucsb.edu/~koc/cs178/projects/JT/aes.c
xtime = lambda a: (((a << 1) ^ 0x1B) & 0xFF) if (a & 0x80) else (a << 1)


def mix_single_column(a):
    # see Sec 4.1.2 in The Design of Rijndael
    t = a[0] ^ a[1] ^ a[2] ^ a[3]
    u = a[0]
    a[0] ^= t ^ xtime(a[0] ^ a[1])
    a[1] ^= t ^ xtime(a[1] ^ a[2])
    a[2] ^= t ^ xtime(a[2] ^ a[3])
    a[3] ^= t ^ xtime(a[3] ^ u)


def mix_columns(s):
    for i in range(4):
        mix_single_column(s[i])


def inv_mix_columns(s):
    # see Sec 4.1.3 in The Design of Rijndael
    for i in range(4):
        u = xtime(xtime(s[i][0] ^ s[i][2]))
        v = xtime(xtime(s[i][1] ^ s[i][3]))
        s[i][0] ^= u
        s[i][1] ^= v
        s[i][2] ^= u
        s[i][3] ^= v

    mix_columns(s)
def expand_key(master_key):
    r_con = (
        0x00, 0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40,
        0x80, 0x1B, 0x36, 0x6C, 0xD8, 0xAB, 0x4D, 0x9A,
        0x2F, 0x5E, 0xBC, 0x63, 0xC6, 0x97, 0x35, 0x6A,
        0xD4, 0xB3, 0x7D, 0xFA, 0xEF, 0xC5, 0x91, 0x39,
    )

    key_columns = bytes_to_matrix(master_key)
    iteration_size = len(master_key) // 4
    i = 1
    while len(key_columns) < (N_ROUNDS + 1) * 4:
        # Copy previous word.   
        word = list(key_columns[-1])

        # Perform schedule_core once every "row".
        if len(key_columns) % iteration_size == 0:
            # Circular shift.
            word.append(word.pop(0))
            # Map to S-BOX.
            word = [s_box[b] for b in word]
            # XOR with first byte of R-CON, since the others bytes of R-CON are 0.
            word[0] ^= r_con[i]
            i += 1
        elif len(master_key) == 32 and len(key_columns) % iteration_size == 4:
            # Run word through S-box in the fourth iteration when using a
            # 256-bit key.
            word = [s_box[b] for b in word]

        # XOR with equivalent word from previous iteration.
        word = bytes(i^j for i, j in zip(word, key_columns[-iteration_size]))
        key_columns.append(word)

    # Group key words in 4x4 byte matrices.
    return [key_columns[4*i : 4*(i+1)] for i in range(len(key_columns) // 4)]

def encrypt(key, plaintext):
    round_keys = expand_key(key)
    text = bytes_to_matrix(plaintext)
    add_round_key(text, round_keys[0])
    for i in range(1, N_ROUNDS):
        sub_bytes(text)
        shift_rows(text)
        mix_columns(text)
        add_round_key(text,round_keys[i])
    sub_bytes(text)
    shift_rows(text)
    add_round_key(text,round_keys[10])
    ciphertext = matrix_to_bytes(text)
    return ciphertext 


def decrypt(key, ciphertext):
    round_keys = expand_key(key) # Remember to start from the last round key and work backwards through them when decrypting

    # Convert ciphertext to state matrix
    text = bytes_to_matrix(ciphertext)
    # Initial add round key step
    add_round_key(text, round_keys[10])

    for i in range(N_ROUNDS - 1, 0, -1):
        inv_shift_rows(text)
        inv_sub_bytes(text)
        add_round_key(text, round_keys[i])
        inv_mix_columns(text)
    # Run final round (skips the InvMixColumns step)
    inv_shift_rows(text)
    inv_sub_bytes(text)
    add_round_key(text, round_keys[0])
    # Convert state matrix to plaintext

    plaintext = matrix_to_bytes(text)
    return plaintext
if __name__ == "__main__":
    import os 
    key = os.urandom(16)
    pt  = os.urandom(16)
    ct = encrypt(key, pt)
    pt_ = decrypt(key,ct) 
    assert pt == pt_
    print("Thuat toan chay on, plaintext ban dau la :" ,f"{pt}")
```

Bây giờ mình sẽ phân tích lại bước KeyExpansion:
Mục đích của bước này là tạo một lịch khóa (key schedule) nhằm sinh ra các khóa khác nhau từ khóa vòng. Lí do ta cần bước này là vì AES có tổng cộng 10 rounds, số khóa vòng là 10 tương ứng với 9 lần AddRoundKey ở bước lặp mã hóa và 1 lần AddRoundKey ở bước tạo ngõ ra. Cho nên để tăng tính ngẫu nhiên của thuật toán ta sẽ sử dụng mỗi khóa vòng khác nhau ở mỗi bước lặp. 

![[Pasted image 20251004090025.png]]
Chức năng KeyExpansion được thực hiện thông qua 4 bước chính là RotWord, SubWord, AddRcon và AddW. Nó sẽ nhận đầu vào là một khóa vòng 16 bytes và đầu ra là một danh sách gồm 44 từ (176 bytes). 
Khóa vòng của ta ban đầu được chia làm 4 từ, mỗi từ 4 bytes, sau đó chuyển thành một ma trận $4 \times 4$. 
Pseudo code cho bước này:
![[Pasted image 20251004092315.png]]


RotWord là thực hiện quay trái một byte của từ
![[Pasted image 20251004091027.png]]
Bước SubWord là thay thế mỗi byte của từ thành một byte trong bảng SBox
Rcon là là các hằng số (round constant) cho mỗi vòng của KeyExpansion: Mọi người tham khảo tại đây: https://en.wikipedia.org/wiki/AES_key_schedule

### DES
Lưu đồ thuật toán mã hóa DES như sau:
![[Pasted image 20251009163304.png]]

DES thực hiện tính toán dựa trên Key, thông qua một hàm $f$ , gọi là hàm mã khóa và một hàm được gọi là key schedule. Hàm này tạo ra các khóa vòng cho các lần lặp mã khóa. Có tổng cộng 16 vòng và do đó ta cần 16 khóa vòng.

Đầu tiên là bước hoán vị khởi tạo

**Hoán vị khởi tạo**
![[Pasted image 20251009163348.png]]
Hoán vị là thay đổi vị trí của các bit trong chuỗi giá trị nhưng không làm thay đổi giá trị của các bit này. Đầu vào của ta là một plaintext có độ lớn 64 bit. Sau đó được hoán vị theo bảng IP. Như trong hình thì bit thứ 58 của plaintext sẽ được dời lên đầu, còn bit thứ 7 thì dời về cuối.

Sau hoán vị, giá trị này sẽ được chia ra làm 2 nửa là $L_0$ và $R_0$. Đoạn $L_0$ bao gồm các bit từ vị trí 1 tới bit thứ 32, còn $R_0$ bao gồm các bit từ vị trí 33 tới 64.
Kế tiếp, các đoạn này sẽ được tính toán dựa vào công thức sau đây:
$$ 
\begin{array}{l}
L_{n+1} = R_n \\ R_{n+1} = L_n \oplus f(R_n, K_{n+1}) 
\end{array}
$$
**Hàm $f(R,K)​$:**

![[Pasted image 20251009163449.png]]
Đầu tiên, 32 bit của đoạn R sẽ được chuyển đổi thông qua bảng tra cứu E.
![[Pasted image 20251009163458.png]]


Trong bảng $E$ ta thấy có một số vị trí có giá trị được lặp lại. Ví dụ bit thứ 32 của $R$ sẽ được dời lên đầu, bit thứ nhất thì đặt vào vị trí thứ hai và vị trí cuối cùng của đầu ra.

Sau đó giá trị đầu ra 48 bits sẽ được XOR với key round cũng có độ dài 48 bits.

![[Pasted image 20251009163508.png]]
Kết quả phép XOR sau đó được chia thành 8 block và được đưa vào các hàm chuyển đổi $S_1,S_2,...,S_8$.

Việc chuyển đổi giá trị của các hàm này được thực hiện bằng cách tách block 6 bit thành hai phần. Phần thứ nhất là tổ hợp của bit đầu tiên và bit cuối cùng của block để tạo thành 2 bit chọn hàng của bảng S, bảng S có 4 hàng được đánh số từ 0 đến 3 theo thứ tự từ trên xuống. Phần thứ 2 là 4 bit còn lại dùng để chọn cột của bảng S, bảng S có 16 cột được đánh số từ 0 đến 15 theo thứ tự từ trái qua phải. Như vậy, với mỗi block 8 bit ta chọn được 1 giá trị trong bảng S. Giá trị này nằm trong khoảng từ 0 đến 15 sẽ được quy đổi thành chuỗi nhị phân 4 bit tương ứng. Các chuỗi nhị phân có được sau khi chuyển đổi từ S1 đến S8 sẽ được ghép lại theo thứ tự từ trái qua phải để tạo thành một giá trị 32 bit.

![[Pasted image 20251009163522.png]]
Cuối cùng, đầu ra 32 bits lại được tra cứu trong bảng hoán vị P trước khi được dùng cho bước tiếp theo là XOR với $L$.
![[Pasted image 20251009163532.png]]

**Tính khóa vòng**
Một key có 64 bit nhưng chỉ có 56 bit được sử dụng để thực hiện tính toán giá trị khóa vòng. Key được chia làm 8 byte. Các bit ở vị trí 8, 16, 32, 40, 48, 56 và 64 là các bit parity được sử dụng để kiểm tra độ chính xác của key theo từng byte vì khi key được phân phối trên đường truyền đến bộ mã hóa giải mã thì có thể xảy ra lỗi.

Như vậy trước khi tính khóa vòng, nó sẽ chọn bỏ đi 8 bit rồi mới bắt đầu tính.

Quy trình tính khóa vòng như sau:
![[Pasted image 20251009163555.png]]

![[Pasted image 20251009163603.png]]
Bước đầu tiên, key sẽ được hoán vị dựa trên quy tắc trong bảng trên và lấy đầu ra là $C_0,D_0$.
Kể từ đây, các khóa vòng $K_n$ với $n$ từ 1 tới 16 sẽ được tính dựa vào công thức:
$$ 
K_n = PC_2(C_nD_n) 
$$

Trong đó $C_n,D_n$ thu được từ $C_{n-1}, D_{n-1}$ thông qua phép dịch trái (left shift). Số bit cần dịch được quy định thông qua bảng sau:

![[Pasted image 20251009163618.png]]
Sau khi dịch bit sau thì các bit sẽ được đánh số từ 1 tới 56 theo thứ tự trái sang phải và được lựa chọn lại thông qua bảng Permutation Choice 2
![[Pasted image 20251009163628.png]]
Bước cuối cùng trong giá trị mã hóa là hoán vị đảo $IP^{-1}$. Đầu ra của vòng thứ 16 sẽ một lần nữa được hoán vị và lấy kết quả làm ciphertext.
![[Pasted image 20251009163644.png]]


## Các mode AES
Trên thực tế, các văn bản đầu vào thường có kích thước lớn kích thước của một block trong AES. Cho nên để thực hiện mã hóa và giải mã thì ta cần chia đầu vào thành các block khác nhau rồi xử lí chúng. 

### AES - ECB
![[Pasted image 20251020230546.png]]
![[Pasted image 20251020230549.png]]
Mode ECB là mode đơn giản nhất trong số các mode của AES. Mode này thực hiện chia ciphertext thành các block rồi mã hóa độc lập từng block với nhau. 



### AES - GCM 

