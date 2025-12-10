## crypto/Catch

Source code của bài:

```python
from Crypto.Random.random import randint, choice
import os

# In a realm where curiosity roams free, our fearless cat sets out on an epic journey.
# Even the cleverest feline must respect the boundaries of its world—this magical limit holds all wonders within.
limit = 0xe5db6a6d765b1ba6e727aa7a87a792c49bb9ddeb2bad999f5ea04f047255d5a72e193a7d58aa8ef619b0262de6d25651085842fd9c385fa4f1032c305f44b8a4f92b16c8115d0595cebfccc1c655ca20db597ff1f01e0db70b9073fbaa1ae5e489484c7a45c215ea02db3c77f1865e1e8597cb0b0af3241cd8214bd5b5c1491f

# Through cryptic patterns, our cat deciphers its next move.
def walking(x, y, part):
    # Each step is guided by a fragment of the cat's own secret mind.
    epart = [int.from_bytes(part[i:i+2], "big") for i in range(0, len(part), 2)]
    xx = epart[0] * x + epart[1] * y
    yy = epart[2] * x + epart[3] * y
    return xx, yy

# Enter the Cat: curious wanderer and keeper of hidden paths.
class Cat:
    def __init__(self):
        # The cat's starting position is born of pure randomness.
        self.x = randint(0, 2**256)
        self.y = randint(0, 2**256)
        # Deep within, its mind holds a thousand mysterious fragments.
        while True:
            self.mind = os.urandom(1000)
            self.step = [self.mind[i:i+8] for i in range(0, 1000, 8)]
            if len(set(self.step)) == len(self.step):
                break

    # The epic chase begins: the cat ponders and strides toward the horizon.
    def moving(self):
        for _ in range(30):
            # A moment of reflection: choose a thought from the cat's endless mind.
            part = choice(self.step)
            self.step.remove(part)
            # With each heartbeat, the cat takes a cryptic step.
            xx, yy = walking(self.x, self.y, part)
            self.x, self.y = xx, yy
            # When the wild spirit reaches the edge, it respects the boundary and pauses.
            if self.x > limit or self.y > limit:
                assert False

    # When the cosmos beckons, the cat reveals its secret coordinates.
    def position(self):
        return (self.x, self.y)

# Adventurer, your quest: find and connect with 20 elusive cats.
for round in range(20):
    try:
        print(f"👉 Hunt {round+1}/20 begins!")
        cat = Cat()

        # At the start, you and the cat share the same starlit square.
        human_pos = cat.position()
        print(f"🐱✨ Co-location: {human_pos}")
        print(f"🔮 Cat's hidden mind: {cat.mind.hex()}")

        # But the cat, ever playful, dashes into the unknown...
        cat.moving()
        print("😸 The chase is on!")

        print(f"🗺️ Cat now at: {cat.position()}")

        # Your turn: recall the cat's secret path fragments to catch up.
        mind = bytes.fromhex(input("🤔 Path to recall (hex): "))

        # Step by step, follow the trail the cat has laid.
        for i in range(0, len(mind), 8):
            part = mind[i:i+8]
            if part not in cat.mind:
                print("❌ Lost in the labyrinth of thoughts.")
                exit()
            human_pos = walking(human_pos[0], human_pos[1], part)

        # At last, if destiny aligns...
        if human_pos == cat.position():
            print("🎉 Reunion! You have found your feline friend! 🐾")
        else:
            print("😿 The path eludes you... Your heart aches.")
            exit()
    except Exception:
        print("🙀 A puzzle too tangled for tonight. Rest well.")
        exit()

# Triumph at last: the final cat yields the secret prize.
print(f"🏆 Victory! The treasure lies within: {open('flag.txt').read()}")
```
Phân tích:

Đầu tiên là hàm walking: Nó lấy 2 bytes tạo thành 1 số sau đó kết hợp lại tạo thành một mảng 4 phần tử. Kế đến ta có $\displaystyle xx=e[ 0] x+e[ 1] y$ và $\displaystyle yy=e[ 2] x+e[ 3] y$ tức là từ 

$$
\displaystyle \begin{bmatrix}
x\\
y
\end{bmatrix}\rightarrow \begin{bmatrix}
xx\\
yy
\end{bmatrix} =\begin{bmatrix}
e_{0} x+e_{1} y\\
e_{2} x+e_{3} y
\end{bmatrix} =\begin{bmatrix}
e_{0} & e_{1}\\
e_{2} & e_{3}
\end{bmatrix}\begin{bmatrix}
x\\
y
\end{bmatrix}
$$
. 


Như vậy 
$$
\begin{equation*}
\begin{bmatrix}
xx\\
yy
\end{bmatrix} =\begin{bmatrix}
e_{0} & e_{1}\\
e_{2} & e_{3}
\end{bmatrix}\begin{bmatrix}
x\\
y
\end{bmatrix}
\end{equation*}
$$

Logic chính của bài nằm ở lớp `Cat()`

Tọa độ ban đầu của con mèo là $\displaystyle ( x,y)$ là hai số random. Tạo 1000 byte ngẫu nhiên. Lấy ra $\displaystyle 1000/8=125$ bộ 8 bytes để tạo các bước đi. 

Hàm moving diễn ra như sau:
Nó chọn một bước đi ngẫu nhiên sau đó xóa bước đi này đi. Cập nhật lại $\displaystyle xx,yy$ như trên 30 lần
Sẽ có 20 rounds và cần qua hết cả 20 rounds để lấy flag. 

Ý tưởng của mình là đi ngược lại. 



Bây giờ giả sử ta có 
$$
\begin{equation*}
\begin{bmatrix}
x_{n}\\
y_{n}
\end{bmatrix}
\end{equation*}
$$

là vị trí của con chuột sau khi đi 30 bước. Ta không thể biết được đường đi đầy đủ của con chuột là bao nhiêu. Có tận 30 bước và brute rất lâu. Vậy thì ta sẽ đi ngược lại. Từ vị trí
$$
\begin{equation*}
\begin{bmatrix}
x_{n}\\
y_{n}
\end{bmatrix}\rightarrow \begin{bmatrix}
x_{1}\\
y_{1}
\end{bmatrix}
\end{equation*}
$$
Ta có sẵn danh sách ma trận của các bước đi, nên ta nhân lần lượt nghịch đảo các bước đi này vào ma trận tọa độ và kiểm tra xem ma trận kết quả có phải là ma trận nguyên hay không là được. Kiểm tra thêm điều kiện về bit length là oke.  

```python
from Crypto.Util.number import *
from sage.all import *
from pwn import *

def format_matrix(m):
    vals = [int(x) for x in m.list()]
    block = b''.join([x.to_bytes(2, 'big') for x in vals])
    return "0x" + block.hex()


limit = 0xe5db6a6d765b1ba6e727aa7a87a792c49bb9ddeb2bad999f5ea04f047255d5a72e193a7d58aa8ef619b0262de6d25651085842fd9c385fa4f1032c305f44b8a4f92b16c8115d0595cebfccc1c655ca20db597ff1f01e0db70b9073fbaa1ae5e489484c7a45c215ea02db3c77f1865e1e8597cb0b0af3241cd8214bd5b5c1491f
io = remote("catch.chal.idek.team" ,1337)

for round in range(1,21):
    io.recvuntil(f"👉 Hunt {round}/20 begins!".encode())
    io.recvline()
    co = io.recvline_contains(b'Co-location:')
    start_pos = eval(co.decode().split(":",1)[1].strip())
    mind = io.recvline_contains(b"Cat's hidden mind:")
    mind_data = mind.decode().split(":", 1)[1].strip()
    io.recvuntil(b'The chase is on!')
    final = io.recvline_contains(b'Cat now at:')
    end_pos = eval(final.decode().split(":", 1)[1].strip())
    data = bytes.fromhex(mind_data)
    step = [data[i:i+8] for i in range(0,1000,8)]
    matrices = [[int.from_bytes(part[i:i+2],'big') for i in range (0,8,2)] for part in step]
    matrices_step = [Matrix(ZZ,[[a[0],a[1]],[a[2],a[3]]]) for a in matrices]
    found = False
    origin = []
    xn, yn = end_pos
    x1, y1 = start_pos
    while not found: 
        for m in matrices_step:
            x_temp, y_temp = m.inverse() * vector([xn,yn])
            if x_temp.is_integer() and y_temp.is_integer():
                x_temp = int(x_temp)
                y_temp = int(y_temp)
                if xn.bit_length()>=x_temp.bit_length() and yn.bit_length()>=y_temp.bit_length():
                    origin.append(m)
                    xn = x_temp
                    yn = y_temp
                    if xn == x1 and yn == y1:
                        found = True
                        break
    path = list(reversed(origin))
    to_send = [format_matrix(m) for m in path]
    full_path = ''.join([m[2:] for m in to_send])  # Bỏ "0x" prefix để nối lại
    io.sendlineafter(b'Path to recall (hex):', full_path.encode())
    res = io.recvline()
    print(f"xong {round} : {res.decode()}")

flag = io.recvall(timeout=2).decode()
print(flag)
io.close()
```

## crypto/Diamond Ticket

Source code của bài:

```python
from Crypto.Util.number import *

#Some magic from Willy Wonka
p = 170829625398370252501980763763988409583
a = 164164878498114882034745803752027154293
b = 125172356708896457197207880391835698381

def chocolate_generator(m:int) -> int:
    return (pow(a, m, p) + pow(b, m, p)) % p

#The diamond ticket is hiding inside chocolate
diamond_ticket = open("flag.txt", "rb").read()
assert len(diamond_ticket) == 26
assert diamond_ticket[:5] == b"idek{"
assert diamond_ticket[-1:] == b"}"
diamond_ticket = bytes_to_long(diamond_ticket[5:-1])

flag_chocolate = chocolate_generator(diamond_ticket)
chocolate_bag = []

#Willy Wonka are making chocolates
for i in range(1337):
    chocolate_bag.append(getRandomRange(1, p))

#And he put the golden ticket at the end
chocolate_bag.append(flag_chocolate)

#Augustus ate lots of chocolates, but he can't eat all cuz he is full now :D
remain = chocolate_bag[-5:]

#Compress all remain chocolates into one
remain_bytes = b"".join([c.to_bytes(p.bit_length()//8, "big") for c in remain])

#The last chocolate is too important, so Willy Wonka did magic again
P = getPrime(512)
Q = getPrime(512)
N = P * Q
e = bytes_to_long(b"idek{this_is_a_fake_flag_lolol}")
d = pow(e, -1, (P - 1) * (Q - 1))
c1 = pow(bytes_to_long(remain_bytes), e, N)
c2 = pow(bytes_to_long(remain_bytes), 2, N) # A small gift

#How can you get it ?
print(f"{N = }")
print(f"{c1 = }")
print(f"{c2 = }") 

"""
N = 85494791395295332945307239533692379607357839212287019473638934253301452108522067416218735796494842928689545564411909493378925446256067741352255455231566967041733698260315140928382934156213563527493360928094724419798812564716724034316384416100417243844799045176599197680353109658153148874265234750977838548867
c1 = 27062074196834458670191422120857456217979308440332928563784961101978948466368298802765973020349433121726736536899260504828388992133435359919764627760887966221328744451867771955587357887373143789000307996739905387064272569624412963289163997701702446706106089751532607059085577031825157942847678226256408018301
c2 = 30493926769307279620402715377825804330944677680927170388776891152831425786788516825687413453427866619728035923364764078434617853754697076732657422609080720944160407383110441379382589644898380399280520469116924641442283645426172683945640914810778133226061767682464112690072473051344933447823488551784450844649
"""
```

Phân tích: Đầu tiên ta có 3 tham số $p,a,b$ và hàm `chocolate_generator(m)`. Nó sẽ nhận vào số mũ $m$ và trả về $a^{m}+b^{m} \bmod p$. 

Tiếp theo cách flag được mã hóa trong bài này như sau:

```python
diamond_ticket = open("flag.txt", "rb").read()
assert len(diamond_ticket) == 26
assert diamond_ticket[:5] == b"idek{"
assert diamond_ticket[-1:] == b"}"
diamond_ticket = bytes_to_long(diamond_ticket[5:-1])
flag_chocolate = chocolate_generator(diamond_ticket)
```

`flag_chocolate` chính là $a^{flag}+b^{flag} \bmod p$. Và ta phải giải để tìm lại `flag` từ thông tin này. 


```python
for i in range(1337):
    chocolate_bag.append(getRandomRange(1, p))
```
Hàm này tạo một danh sách `chocolate_bag` gồm các số ngẫu nhiên trong khoảng $[1,p]$ nhưng sau đó chỉ lấy 5 số cuối trong đó bao gồm flag của ta. 

```python
chocolate_bag.append(flag_chocolate)
#Augustus ate lots of chocolates, but he can't eat all cuz he is full now :D
remain = chocolate_bag[-5:]
```

Sau đó nó sẽ nối các phần tử trong `remain` lại và mã hóa bằng RSA

```python
remain_bytes = b"".join([c.to_bytes(p.bit_length()//8, "big") for c in remain])

#The last chocolate is too important, so Willy Wonka did magic again
P = getPrime(512)
Q = getPrime(512)
N = P * Q
e = bytes_to_long(b"idek{this_is_a_fake_flag_lolol}")
d = pow(e, -1, (P - 1) * (Q - 1))
c1 = pow(bytes_to_long(remain_bytes), e, N)
c2 = pow(bytes_to_long(remain_bytes), 2, N) # A small gift
```

Trước tiên mình cần tìm lại `remain_bytes` từ hai giá trị $c1$ và $c2$. 

$$
\begin{array}{l}
c_{1} =m^{e}\bmod N\\
c_{2} =m^{2}\bmod N
\end{array}
$$
Với $e$ được tạo bởi `e = bytes_to_long(b"idek{this_is_a_fake_flag_lolol}")` là một số lẻ. 
Bây giờ giả sử ta có $\displaystyle c_{1} =m^{a}$ và $\displaystyle c_{2} =m^{b}$. Muốn tính lại $\displaystyle m$ ta sẽ làm như sau: Ta gọi $\displaystyle g=\gcd( a,b)$. Đối với bài này thì $\displaystyle g=1$. Như vậy theo định lí Bezout tồn tại $\displaystyle u,v$ để $\displaystyle au+bv=1$. 

Sau đó ta sẽ tính $\displaystyle c_{1}^{u} =m^{au}$ và $\displaystyle c_{2}^{v} =m^{vb}$ và tính $\displaystyle c_{1}^{u} \times c_{2}^{v} =m^{au+vb} =m$ và khôi phục lại được giá trị của $\displaystyle m$ ban đầu. Nếu như $\displaystyle g >1$ thì ta có thể lấy `nth_root(g)` của nó .

Script cho bước này:


```python
from Crypto.Util.number import *
from sage.all import *


N = 85494791395295332945307239533692379607357839212287019473638934253301452108522067416218735796494842928689545564411909493378925446256067741352255455231566967041733698260315140928382934156213563527493360928094724419798812564716724034316384416100417243844799045176599197680353109658153148874265234750977838548867
c1 = 27062074196834458670191422120857456217979308440332928563784961101978948466368298802765973020349433121726736536899260504828388992133435359919764627760887966221328744451867771955587357887373143789000307996739905387064272569624412963289163997701702446706106089751532607059085577031825157942847678226256408018301
c2 = 30493926769307279620402715377825804330944677680927170388776891152831425786788516825687413453427866619728035923364764078434617853754697076732657422609080720944160407383110441379382589644898380399280520469116924641442283645426172683945640914810778133226061767682464112690072473051344933447823488551784450844649
e = bytes_to_long(b"idek{this_is_a_fake_flag_lolol}")
def attack(n, e1, c1, e2, c2):
    g, u, v = xgcd(e1, e2)
    p1 = pow(c1, u, n) if u > 0 else pow(pow(c1, -1, n), -u, n)
    p2 = pow(c2, v, n) if v > 0 else pow(pow(c2, -1, n), -v, n)
    return int(ZZ(int(p1 * p2) % n).nth_root(g))
remain_bytes = attack(N,e,c1,2,c2)
print(remain_bytes)
```
`remain_bytes` có `len == 80 bytes` được tạo thành từ 5 phần, mỗi phần `16 bytes` chính là `len` của số nguyên tố `p`. Vậy ta tách nó thành 5 phần bằng nhau và lấy phần cuối chính là `flag_chocolate` của ta. 

```python=
print(remain_bytes)
remain_bytes = long_to_bytes(remain_bytes)
print(len(remain_bytes))
remain = [
    int.from_bytes(remain_bytes[i:i + 16], "big")
    for i in range(0, 80, 16)
]
flag_chocolate = remain[-1]
print(flag_chocolate)
# 99584795316725433978492646071734128819
```

Tiếp theo ta sẽ giải DLP. 

Bây giờ ta có $p,a,b$ và $a^m + b^m \bmod p$. 

Kiểm tra order: 
```python
sage: p = 170829625398370252501980763763988409583
sage: factor(p-1)
2 * 40841 * 50119 * 51193 * 55823 * 57809 * 61991 * 63097 * 64577
sage:
```
Order của nhóm khá smooth. 

Nhưng ta cần tìm order của hai số $a$ và $b$. 

```python
sage: p = 170829625398370252501980763763988409583
....: a = 164164878498114882034745803752027154293
....: b = 125172356708896457197207880391835698381
sage: K = Zmod(p)
sage: a = K(a)
sage: b = K(b)
sage: print(a.multiplicative_order())
85414812699185126250990381881994204791
sage: print(b.multiplicative_order())
85414812699185126250990381881994204791
sage: order1 = a.multiplicative_order()
sage: order2 = a.multiplicative_order()
sage: assert order1 == order2
sage: order = p-1
sage: print(order/order1)
2
sage:
```
Vậy cấp của $a$ và $b$ là $(p-1)/2$. 
Về cơ bản thì không thể giải được bài toán nếu như giữ nguyên cả hai số $a$ và $b$ được. Nên mình đã thử tìm một số $k$ sao cho $b=a^k \bmod p$ coi sao. 

```python
sage: k  = discrete_log(b,a,order1)
sage: print(k)
73331
sage:
```
Đưa về bài toán $a^m+  a^{km} \bmod p$.

Bây giờ mình muốn tìm lại $a^m$ nên đã thử dựng đa thức $f = x + x^k -c$.

Vấn đề là số mũ $k$ khá lớn nên để tìm lại nghiệm khá tốn thời gian nên mình xài một `trick lỏ` học được sau giải `MaltaCTF` vừa rồi. https://github.com/ctf-mt/maltactf-2025-quals/blob/master/crypto/grammar-nazi/solution/solve.sage

Ta đã biết với  $\displaystyle K$ là một trường hữu hạn có đặc số nguyên tố $\displaystyle p$ thì $\displaystyle x^{p^{n}} -x=x\prod _{u_{i} \in K^{*}}( x-u_{i})$ với $\displaystyle K^{*} =K\backslash \{0\}$. 

Ở đây ta đang làm việc với $K=GF(p)$ và một nhóm con của nó là nhóm các thặng dư bậc hai vì bậc của $a$ là $(p-1)/2$. Nhóm con của một nhóm cyclic cũng là một nhóm cyclic cho nên mình sẽ dựng một đa thức khác là $g = x^r - x$ trong đó $r = (p-1)/2 + 1$. 

Vấn đề là trong sage khi gọi $g$ như vậy thì gặp lỗi 

```
OverflowError: cannot fit 'int' into an index-sized integer
```
Do số mũ quá lớn nên sage không xử lí được. Để khắc phục thì mình lấy `f.gcd(pow(x,r,f)-x).roots(multiplicities=False)` là được.

```python
K = Zmod(p)
a = K(a)
b = K(b)
order1 = a.multiplicative_order()
order2 = b.multiplicative_order()
r = (p-1)//2 + 1
print(order1 ,'\n')
print(order2)
# a^m + b^m = c mod p 
k = discrete_log(b,a)
# k = 73331
c = K(flag_chocolate)
P = PolynomialRing(K, 'a')
x = P.gen()
f = x  + x**k - c 
res = f.gcd(pow(x,r,f)-x).roots(multiplicities=False)
print(res)
# 126961729658296101306560858021273501485
```
```python=
a_m = K(126961729658296101306560858021273501485)
m0 = discrete_log(a_m,a,order1)
# m0 = 4807895356063327854843653048517090061
```
Bước tiếp theo là tìm lại $m$ ban đầu. Ta biết $a^m = a^{m_0} \bmod p$ thì $m\equiv m_0 \bmod order$. Vấn đề là $m0$ chỉ có 122 bits trong khi $m$ gốc ban đầu có gồm 20 bytes tức là 160 bits ??

Khúc này trong giải mình bị skill issue nên brute k ra. Sau mình có biết được có thể dùng BigInt của Cpp hoặc Rust để brute cx được

```rust
use num_bigint::BigUint;
use num_traits::Num;
use std::str;

fn is_printable_ascii(byte: u8) -> bool {
    byte >= 0x20 && byte < 0x7f
}

fn main() {
    let mut m = BigUint::from_str_radix("4807895356063327854843653048517090061", 10).unwrap();
    let order = BigUint::from_str_radix("85414812699185126250990381881994204791", 10).unwrap();

    while m.to_bytes_be().len() <= 20 {
        let flag = m.to_bytes_be();
        if flag.len() == 20 && flag.iter().all(|&b| is_printable_ascii(b)) {
            if let Ok(s) = str::from_utf8(&flag) {
                println!("{}", s);
            }
        }
        m += &order;
    }
}
```
## crypto/Sadness ECC
Source code của bài: 

```python
from Crypto.Util.number import *
from secret import n, xG, yG
import ast

class DummyPoint:
    O = object()

    def __init__(self, x=None, y=None):
        if (x, y) == (None, None):
            self._infinity = True
        else:
            assert DummyPoint.isOnCurve(x, y), (x, y)
            self.x, self.y = x, y
            self._infinity = False

    @classmethod
    def infinity(cls):
        return cls()

    def is_infinity(self):
        return getattr(self, "_infinity", False)

    @staticmethod
    def isOnCurve(x, y):
        return "<REDACTED>"

    def __add__(self, other):
        if other.is_infinity():
            return self
        if self.is_infinity():
            return other

        # ——— Distinct‑points case ———
        if self.x != other.x or self.y != other.y:
            dy    = self.y - other.y
            dx    = self.x - other.x
            inv_dx = pow(dx, -1, n)
            prod1 = dy * inv_dx
            s     = prod1 % n

            inv_s = pow(s, -1, n)
            s3    = pow(inv_s, 3, n)

            tmp1 = s * self.x
            d    = self.y - tmp1

            d_minus    = d - 1337
            neg_three  = -3
            tmp2       = neg_three * d_minus
            tmp3       = tmp2 * inv_s
            sum_x      = self.x + other.x
            x_temp     = tmp3 + s3
            x_pre      = x_temp - sum_x
            x          = x_pre % n

            tmp4       = self.x - x
            tmp5       = s * tmp4
            y_pre      = self.y - tmp5
            y          = y_pre % n

            return DummyPoint(x, y)

        dy_term       = self.y - 1337
        dy2           = dy_term * dy_term
        three_dy2     = 3 * dy2
        inv_3dy2      = pow(three_dy2, -1, n)
        two_x         = 2 * self.x
        prod2         = two_x * inv_3dy2
        s             = prod2 % n

        inv_s         = pow(s, -1, n)
        s3            = pow(inv_s, 3, n)

        tmp6          = s * self.x
        d2            = self.y - tmp6

        d2_minus      = d2 - 1337
        tmp7          = -3 * d2_minus
        tmp8          = tmp7 * inv_s
        x_temp2       = tmp8 + s3
        x_pre2        = x_temp2 - two_x
        x2            = x_pre2 % n

        tmp9          = self.x - x2
        tmp10         = s * tmp9
        y_pre2        = self.y - tmp10
        y2            = y_pre2 % n

        return DummyPoint(x2, y2)

    def __rmul__(self, k):
        if not isinstance(k, int) or k < 0:
            raise ValueError("Choose another k")
        
        R = DummyPoint.infinity()
        addend = self
        while k:
            if k & 1:
                R = R + addend
            addend = addend + addend
            k >>= 1
        return R

    def __repr__(self):
        return f"DummyPoint({self.x}, {self.y})"

    def __eq__(self, other):
        return self.x == other.x and self.y == other.y

if __name__ == "__main__":
    G = DummyPoint(xG, yG)
    print(f"{n = }")
    stop = False
    while True:
        print("1. Get random point (only one time)\n2. Solve the challenge\n3. Exit")
        try:
            opt = int(input("> "))
        except:
            print("❓ Try again."); continue

        if opt == 1:
            if stop:
                print("Only one time!")
            else:
                stop = True
                k = getRandomRange(1, n)
                P = k * G
                print("Here is your point:")
                print(P)

        elif opt == 2:
            ks = [getRandomRange(1, n) for _ in range(2)]
            Ps = [k * G for k in ks]
            Ps.append(Ps[0] + Ps[1])

            print("Sums (x+y):", [P.x + P.y for P in Ps])
            try:
                ans = ast.literal_eval(input("Your reveal: "))
            except:
                print("Couldn't parse."); continue

            if all(P == DummyPoint(*c) for P, c in zip(Ps, ans)):
                print("Correct! " + open("flag.txt").read())
            else:
                print("Wrong...")
            break

        else:
            print("Farewell.") 
            break
```


Phân tích: Bài này xoay quanh class chính là `DummyPoint` gồm các điểm trên một đường cong Elliptic với hai công thức cộng và nhân. 

Công thức cộng như sau:

```python
    def __add__(self, other):
        if other.is_infinity():
            return self
        if self.is_infinity():
            return other

        # ——— Distinct‑points case ———
        if self.x != other.x or self.y != other.y:
            dy    = self.y - other.y
            dx    = self.x - other.x
            inv_dx = pow(dx, -1, n)
            prod1 = dy * inv_dx
            s     = prod1 % n

            inv_s = pow(s, -1, n)
            s3    = pow(inv_s, 3, n)

            tmp1 = s * self.x
            d    = self.y - tmp1

            d_minus    = d - 1337
            neg_three  = -3
            tmp2       = neg_three * d_minus
            tmp3       = tmp2 * inv_s
            sum_x      = self.x + other.x
            x_temp     = tmp3 + s3
            x_pre      = x_temp - sum_x
            x          = x_pre % n

            tmp4       = self.x - x
            tmp5       = s * tmp4
            y_pre      = self.y - tmp5
            y          = y_pre % n

            return DummyPoint(x, y)

        dy_term       = self.y - 1337
        dy2           = dy_term * dy_term
        three_dy2     = 3 * dy2
        inv_3dy2      = pow(three_dy2, -1, n)
        two_x         = 2 * self.x
        prod2         = two_x * inv_3dy2
        s             = prod2 % n

        inv_s         = pow(s, -1, n)
        s3            = pow(inv_s, 3, n)

        tmp6          = s * self.x
        d2            = self.y - tmp6

        d2_minus      = d2 - 1337
        tmp7          = -3 * d2_minus
        tmp8          = tmp7 * inv_s
        x_temp2       = tmp8 + s3
        x_pre2        = x_temp2 - two_x
        x2            = x_pre2 % n

        tmp9          = self.x - x2
        tmp10         = s * tmp9
        y_pre2        = self.y - tmp10
        y2            = y_pre2 % n

        return DummyPoint(x2, y2)
```

Mình không biết dạng chính xác của phương trình này là gì nên chỉ có thể đi phân tích xem phép cộng được thực hiện như thế nào. 
**Trường hợp 1:** Cộng hai điểm $(x,y)$ và $(x',y')$ phân biệt. 

```
(x,y) + (x',y')
dy = y - y'
dx = x - x'
inv_dx = (x-x')^-1 mod n 
prod1 = dy ** inv_dx = (y-y')/(x-x') mod n 
s = prod1 % n
inv_s = s^-1 mod n = (x-x')/(y-y') mod n 
s3 = inv_s ^ 3
tmp1 = s * x
d = y - tmp1
d_minus = d - 1337
neg_three = -3 ???? wtf 
tmp2 = -3 * (d - 1337)
tmp3 = tmp2 * inv_s 
sum_x = x + x'
x_temp = tmp3  + s3
x_pre = x_temp - sum_x 
x = x_pre % n

tmp4 = x - x'
tmp5 = s * tmp4
y_pre = y - tmp5
y = y_pre % n 

=> trả về (x,y) mới là kết quả của phép cộng
```
$$
\begin{gather*}
( x,y) +( x',y') =\left( x^{+} ,y^{+}\right)\\
x^{+} =3( 1337-d) \times \frac{x-x'}{y-y'} +\left(\frac{x-x'}{y-y'}\right)^{3} -( x+x') \ \bmod n,\ d\ =\ y-\frac{y-y'}{x-x'} x\bmod n\\
y^{+} =y-s\left( x-x^{+}\right)\bmod n
\end{gather*}
$$
Gọn hơn ta có thể viết 

$$
\begin{gather*}
s=\frac{y-y'}{x-x'}\bmod n\\
d=y-sx\\
x^{+} =3( 1337-d) s^{-1} +s^{-3} -( x+x') \ \bmod n\\
y^{+} =y-s\left( x-x^{+}\right) \ \bmod n\\
( x,y) +( x',y') =\left( x^{+} ,y^{+}\right)
\end{gather*}
$$
**Trường hợp 2:** Point-Doubling
Tương tự ta cũng có được công thức
$$
\begin{gather*}
s=\frac{2x}{3( y-1337)^{2}} \ \bmod n\\
d=y-sx\ \bmod n\\
x^{+} =3( 1337-d) s^{-1} +s^{-3} -2x\\
y^{+} =y-s\left( x-x^{+}\right)
\end{gather*}
$$
Về cơ bản hai công thức giống hệt nhau và chỉ thay đổi cách mà $s$ được tính. 
Liên hệ lại với công thức cộng hai điểm trên trường hữu hạn thì cách tính $s$ giống nhau ở bước cộng hai điểm phân biệt
![[Pasted image 20251210092416.png]]
Bài này cho ta 3 option

**Option 1:** Lấy một điểm random trên đường cong này 
**Option 2:** Sinh 2 giá trị $k_1$ và $k_2$ sau đó tính $P_1=k_{1}G$ và $P_2=k_{2}G$ và $P_3=P_2+P_1$ và trả về cho ta danh sách `[P_1.x + P_1.y, P_2.x + P_2.y, P_3.x + P_3.y]` và ta phải nhập lại chính xác các tọa độ này `[(x1, y1), (x2, y2), (x3, y3)]` để lấy lại flag. 


Bây giờ mình sẽ khôi phục lại phương trình của đường cong này. $s$ thực ra là hệ số góc của đường thẳng nối hai điểm $P_1$ và $P_2$ trong phép cộng. Trong trường hợp hai điểm trùng nhau thì đường thẳng nối chúng cũng chính là tiếp tuyến của đường cong và ta có 
$$
\begin{gather*}
\frac{dy}{dx} =\frac{2x}{3( y-1337)^{2}}\\
\Longrightarrow 2xdx=3( y-1337)^{2} dy\\
\Longrightarrow \int 3( y-1337)^{2} dy=\int 2xdx\\
\Longrightarrow ( y-1337)^{3} =x^{2} +C
\end{gather*}
$$

Điểm kiểm tra $C$ bằng bao nhiêu thì chọn option 1 để lấy một điểm trên server. 
```python
from pwn import *
from sage.all import *
from Crypto.Util.number import * 
n = 18462925487718580334270042594143977219610425117899940337155124026128371741308753433204240210795227010717937541232846792104611962766611611163876559160422428966906186397821598025933872438955725823904587695009410689230415635161754603680035967278877313283697377952334244199935763429714549639256865992874516173501812823285781745993930473682283430062179323232132574582638414763651749680222672408397689569117233599147511410313171491361805303193358817974658401842269098694647226354547005971868845012340264871645065372049483020435661973539128701921925288361298815876347017295555593466546029673585316558973730767171452962355953
x = 9857283255232989270375116420280989264795036197519564727795184063830324007455668601751743103383226543826335563538856783696382226548553000227982952523039995075210479468061569859779384836275728613279899918701300949077434708039829880806084885806542792810310724878185170155750825677266254987100037168879682129579563274056585129108815889035320641229779520731402133385553889049674832566715227898469890183845263073984557037794627554435991774559462939962540081639422995756951487872128543869157319825862197800482596551971440500731289429866012014102228190279326524016486052868308614235267476218756514801298528177751121273480371
y = 2499252114479643575795790710705954602411799174653755001310368875923483883491785224339951820547535603881851608473085227620826380540886628194251752001192767666703431631200767911305118682580325865952197627290925085493109738811648065730327133156612774184421486802272683528815202501920841066040949636937623321239683485995073379379594722561200416772969913466780336043368113517562111007642318759465699735428286464270668463481542627946372226659604734533474834685724443547082913077024513566692477134327729630835719628197283361960308590177628961649053761847458898267144459793538380630300528766964852502281041691614814892663407
c = pow(y-1337,3,n)-pow(x,2,n)
print(c) 
```
Mình được $c=0$. Vậy coi như phương trình của ta là $x^2 = (y-1337)^3$ với modulo $n$. 

Bây giờ xét bộ 3 $\displaystyle ( x_{1} ,y_{1}) ,( x_{2} ,y_{2}) ,( x_{3} ,y_{3})$ là 3 nghiệm của phương trình này. Server cho ta biết tổng của 3 giá trị này. Hơn nữa, ta cũng có thêm ràng buộc là phương trình ở trên $\displaystyle ( y_{1} -1337)^{3} =x_{1}^{2}$. Nếu lấy $\displaystyle x_{1} +y_{1} =c$ và gọi $\displaystyle y_{1} =c-x_{1}$ thì thay lại $\displaystyle ( c-x_{1} -1337)^{3} -x_{1}^{2} =0\bmod n$. Nhưng giải tìm nghiệm của đa thức theo modulo $\displaystyle n$ không quá khả thi vì $\displaystyle n$ là hợp số, hơn nữa ta không factor $\displaystyle n$ được.

Vậy ta có thể sử dụng Groebner basis để xử lí hệ này.

```python
R = PolynomialRing(Zmod(n), ['x0', 'y0', 'x1', 'y1'])
x0, y0 , x1, y1 = R.gens()
f0 = x0+y0-sums[0]
f1 = x1+y1 - sums[1]
g0 = x0**2-(y0-1337)**3
g1 = x1**2-(y1-1337)**3
I = Ideal([f0,f1,g0,g1])
G = I.groebner_basis()
for g in G:
    print(g,'\n')
```
Sau khi in ra check thử thì mình thấy các phương trình vẫn giữ nguyên chả khác gì :v cho nên chỉ với 4 ràng buộc thì chưa đủ, ít nhất cần tạo thêm 1 ràng buộc nữa. 

Trick lỏ để làm mất đi `(y1-y0)^-1` đó là quy đồng, bằng cách nhân thêm `(y1-y0)^4`. 
Script solve:

```python
from sage.all import *
from pwn import *
from ast import literal_eval
def add_point(x0, y0, x1, y1):
    x = (2*x0 - x1 + (x0 - x1)**3 * pow((y0 - y1)**3, -1, n) + (3*(x0 - x1)*(y0 - 1337)) * pow(y1 - y0, -1, n)) % n
    y = (4011 - y0 + (x0 - x1)**2 * pow((y0 - y1)**2, -1, n) - y1) % n

p = remote("sad-ecc.chal.idek.team", 1337)
p.sendlineafter(b">", b"2")
p.recvuntil(b"(x+y): ")
sums = literal_eval(p.recvline().decode())
R = PolynomialRing(Zmod(n), names="x0,y0,x1,y1")
x0, y0, x1, y1 = R.gens()
I = R.ideal(
    x0 + y0 - sums[0],
    x1 + y1 - sums[1],
    -(2*x0 * (y1 - y0) * (y0 - y1)**3 - x1 * (y1 - y0) * (y0 - y1)**3 + (x0 - x1)**3 * (y1 - y0) + 3*(x0 - x1)*(y0 - 1337) * (y0 - y1)**3) + (4011 * (y0 - y1)**2 - y0 * (y0 - y1)**2 + (x0 - x1)**2 - y1 * (y0 - y1)**2) * (y0 - y1)**2 - sums[2] * (y0 - y1)**4,
    x0**2 - (y0-1337)**3,
    x1**2 - (y1-1337)**3
)

groebner = I.groebner_basis()

x0 = -groebner[0].coefficients()[1]
y0 = -groebner[1].coefficients()[1]
x1 = -groebner[2].coefficients()[1]
y1 = -groebner[3].coefficients()[1]
x2, y2 = add_point(x0, y0, x1, y1)

print(f"{x0 = } {y0 = }")
print(f"{x1 = } {y1 = }")
print(f"{x2 = } {y2 = }")

p.sendline(str([(x0, y0), (x1, y1), (x2, y2)]).encode())
p.interactive()
# idek{the_idea_came_from_a_Vietnamese_high_school_Mathematical_Olympiad_competition_xD}
```
## crypto/Happy ECC



Source code của bài:

```python
from sage.all import *
from Crypto.Util.number import *

# Edited a bit from https://github.com/aszepieniec/hyperelliptic/blob/master/hyperelliptic.sage
class HyperellipticCurveElement:
    def __init__( self, curve, U, V ):
        self.curve = curve
        self.U = U
        self.V = V

    @staticmethod
    def Cantor( curve, U1, V1, U2, V2 ):
        # 1.
        g, a, b = xgcd(U1, U2)   # a*U1 + b*U2 == g
        d, c, h3 = xgcd(g, V1+V2) # c*g + h3*(V1+V2) = d
        h2 = c*b
        h1 = c*a
        # h1 * U1 + h2 * U2 + h3 * (V1+V2) = d = gcd(U1, U2, V1-V2)

        # 2.
        V0 = (U1 * V2 * h1 + U2 * V1 * h2 + (V1*V2 + curve.f) * h3).quo_rem(d)[0]
        R = U1.parent()
        V0 = R(V0)

        # 3.
        U = (U1 * U2).quo_rem(d**2)[0]
        U = R(U)
        V = V0 % U

        while U.degree() > curve.genus:
            # 4.
            U_ = (curve.f - V**2).quo_rem(U)[0]
            U_ = R(U_)
            V_ = (-V).quo_rem(U_)[1]

            # 5.
            U, V = U_.monic(), V_
        # (6.)

        # 7.
        return U, V

    def parent( self ):
        return self.curve

    def __add__( self, other ):
        U, V = HyperellipticCurveElement.Cantor(self.curve, self.U, self.V, other.U, other.V)
        return HyperellipticCurveElement(self.curve, U, V)

    def inverse( self ):
        return HyperellipticCurveElement(self.curve, self.U, -self.V)

    def __rmul__(self, exp):
        R = self.U.parent()
        I = HyperellipticCurveElement(self.curve, R(1), R(0))

        if exp == 0:
            return HyperellipticCurveElement(self.curve, R(1), R(0))
        if exp == 1:
            return self

        acc = I
        Q = self
        while exp:
            if exp & 1:
                acc = acc + Q
            Q = Q + Q
            exp >>= 1
        return acc
    
    def __eq__( self, other ):
        if self.curve == other.curve and self.V == other.V and self.U == other.U:
            return True
        else:
            return False

class HyperellipticCurve_:
    def __init__( self, f ):
        self.R = f.parent()
        self.F = self.R.base_ring()
        self.x = self.R.gen()
        self.f = f
        self.genus = floor((f.degree()-1) / 2)
    
    def identity( self ):
        return HyperellipticCurveElement(self, self.R(1), self.R(0))
    
    def random_element( self ):
        roots = []
        while len(roots) != self.genus:
            xi = self.F.random_element()
            yi2 = self.f(xi)
            if not yi2.is_square():
                continue
            roots.append(xi)
            roots = list(set(roots))
        signs = [ZZ(Integers(2).random_element()) for r in roots]

        U = self.R(1)
        for r in roots:
            U = U * (self.x - r)

        V = self.R(0)
        for i in range(len(roots)):
            y = (-1)**(ZZ(Integers(2).random_element())) * sqrt(self.f(roots[i]))
            lagrange = self.R(1)
            for j in range(len(roots)):
                if j == i:
                    continue
                lagrange = lagrange * (self.x - roots[j])/(roots[i] - roots[j])
            V += y * lagrange

        return HyperellipticCurveElement(self, U, V)
 
p = getPrime(40)
R, x = PolynomialRing(GF(p), 'x').objgen()

f = R.random_element(5).monic()
H = HyperellipticCurve_(f)

print(f"{p = }")
if __name__ == "__main__":
    cnt = 0
    while True:
        print("1. Get random point\n2. Solve the challenge\n3. Exit")
        try:
            opt = int(input("> "))
        except:
            print("❓ Try again."); continue

        if opt == 1:
            if cnt < 3:
                G = H.random_element()
                k = getRandomRange(1, p)
                P = k * G
                print("Here is your point:")
                print(f"{P.U = }")
                print(f"{P.V = }")
                cnt += 1
            else:
                print("You have enough point!")
                continue

        elif opt == 2:
            G = H.random_element()
            print(f"{(G.U, G.V) = }")
            print("Give me the order !")
            odr = int(input(">"))
            if (odr * G).U == 1:
                print("Congratz! " + open("flag.txt", "r").read())
            else:
                print("Wrong...")
            break

        else:
            print("Farewell.") 
            break
```

Phần này mình chưa học nên chắc sẽ để dành up solve vào một ngày khác. 


