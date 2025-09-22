---
title: Hash Function
---
## Giới thiệu
Một số bài viết:
[1] https://eprint.iacr.org/2004/035.pdf
[2] https://faculty.cc.gatech.edu/~aboldyre/teaching/Fall05cs6260/m-birthday.pdf
[3] https://preshing.com/20110504/hash-collision-probabilities/
[4] https://www.cit.ctu.edu.vn/~pnkhang/cours/atbmtt/chuong%204-%20ham%20bam.pdf
[5] https://hackmd.io/@tvdat20004/HkxCf9eLZR
[6] https://www.youtube.com/watch?v=wv8aiqWE3Iw&t=5102s

## Tổng quan
Các hàm băm $\displaystyle ( H)$ tạo ra bản nhận dạng (fingerprint) cho một tập tin, thông điệp hay một khối dữ liệu truyền đi nhằm kiểm tra tính toàn vẹn. Một số đặc tính của hàm băm có thể kể đến như sau:
- $\displaystyle H$ có thể được áp dụng trên khối dữ liệu có độ dài bất kì
- $\displaystyle H$ tạo đầu ra có độ dài cố định
- $\displaystyle H( x)$ tính toán mọi $\displaystyle x$ tương đối dễ dàng, tạo điều kiện để có thể cài đặt trên phần cứng lẫn phần mềm được thiết thực
- Với bất kì giá trị băm $\displaystyle h$, không thể tính được (Pre-image resistance) $\displaystyle x$ sao cho $\displaystyle H( x) =h$. Hàm $\displaystyle H$ như vậy được gọi là hàm một chiều.
- Weak collision resistance: với bất kì giá trị $\displaystyle x$, không thể tính được $\displaystyle y\neq x$ sao cho $\displaystyle H( y) =H( x)$
- Strong collision resistance: Không thể tính được một cặp $\displaystyle ( x,y)$ sao cho $\displaystyle H( x) =H( y)$. 
##  Bài tập

## Jack's Birthday Hash

Trong bài này có nhắc đến avalanche effect hay còn gọi là hiệu ứng tuyết lở, tức là chỉ cần có một thay đổi nhỏ trong đầu vào của hàm Hash cũng sẽ làm đầu ra thay đổi đáng kể. 
Chẳng hạn như minh họa dưới đây: 

![image](https://hackmd.io/_uploads/SJj-4XdWlx.png)
Ở bài này, ta xét một hàm hash là `JACK11` với đầu ra là một chuỗi bit có độ dài là 11. Ta có `JACK11(secret)=01011001101`. Câu hỏi đặt ra là ta cần hash số lượng đầu vào là bao nhiêu để có $50\%$ xác suất xảy ra collision với secret của Jack.

Đọc bài viết sau đây: https://preshing.com/20110504/hash-collision-probabilities/


## Jack's Birthday Confusion
## Collider 

Server của bài: `socket.cryptohack.org 13389`
Source code của bài:

```python
import hashlib
from utils import listener


FLAG = "crypto{???????????????????????????????????}"


class Challenge():
    def __init__(self):
        self.before_input = "Give me a document to store\n"
        self.documents = {
            "508dcc4dbe9113b15a1f971639b335bd": b"Particle physics (also known as high energy physics) is a branch of physics that studies the nature of the particles that constitute matter and radiation. Although the word particle can refer to various types of very small objects (e.g. protons, gas particles, or even household dust), particle physics usually investigates the irreducibly smallest detectable particles and the fundamental interactions necessary to explain their behaviour.",
            "cb07ff7a5f043361b698c31046b8b0ab": b"The Large Hadron Collider (LHC) is the world's largest and highest-energy particle collider and the largest machine in the world. It was built by the European Organization for Nuclear Research (CERN) between 1998 and 2008 in collaboration with over 10,000 scientists and hundreds of universities and laboratories, as well as more than 100 countries.",
        }

    def challenge(self, msg):
        if "document" not in msg:
            self.exit = True
            return {"error": "You must send a document"}

        document = bytes.fromhex(msg["document"])
        document_hash = hashlib.md5(document).hexdigest()

        if document_hash in self.documents.keys():
            self.exit = True
            if self.documents[document_hash] == document:
                return {"error": "Document already exists in system"}
            else:
                return {"error": f"Document system crash, leaking flag: {FLAG}"}

        self.documents[document_hash] = document

        if len(self.documents) > 5:
            self.exit = True
            return {"error": "Too many documents in the system"}

        return {"success": f"Document {document_hash} added to system"}


import builtins; builtins.Challenge = Challenge # hack to enable challenge to be run locally, see https://cryptohack.org/faq/#listener
"""
When you connect, the 'challenge' function will be called on your JSON
input.
"""
listener.start_server(port=13389)
```

Phân tích source code: 

Đầu tiên ta được cho 2 documents: 
```python
        self.documents = {
            "508dcc4dbe9113b15a1f971639b335bd": b"Particle physics (also known as high energy physics) is a branch of physics that studies the nature of the particles that constitute matter and radiation. Although the word particle can refer to various types of very small objects (e.g. protons, gas particles, or even household dust), particle physics usually investigates the irreducibly smallest detectable particles and the fundamental interactions necessary to explain their behaviour.",
            "cb07ff7a5f043361b698c31046b8b0ab": b"The Large Hadron Collider (LHC) is the world's largest and highest-energy particle collider and the largest machine in the world. It was built by the European Organization for Nuclear Research (CERN) between 1998 and 2008 in collaboration with over 10,000 scientists and hundreds of universities and laboratories, as well as more than 100 countries.",
        }
```
Khi gọi tới server ta sẽ gửi một `msg` có chứa một document và server sẽ tính hash md5 của nó
```python=
        document = bytes.fromhex(msg["document"])
        document_hash = hashlib.md5(document).hexdigest()
```
Một điều thú vị là mình thử tính hash md5 của 2 đoạn văn trên thì nó chính là cái key đằng trước luôn.

![image](https://hackmd.io/_uploads/By3An6d-gl.png)

Điều kiện đằng sau đó cũng nêu rõ không được nhập lại document có giá trị hash trùng với key:
```python
if document_hash in self.documents.keys():
    self.exit = True
```
Điều kiện để leak flag là như dưới đây:

```python
 if self.documents[document_hash] == document:
                return {"error": "Document already exists in system"}
            else:
                return {"error": f"Document system crash, leaking flag: {FLAG}"}
```
Tức là ta cần tìm một document mà giá trị hash của nó trùng với một trong các giá trị hash đã tính nhưng nội dung thì khác với các document còn lại. 
Nói cách khác là tìm một collision. 

Mình đọc được một bài viết và lụm được 2 file có nội dung khác nhau nhưng md5 hash thì lại giống nhau: 
https://crypto.stackexchange.com/questions/1434/are-there-two-known-strings-which-have-the-same-md5-hash-value.

Script giải:
```python
from pwn import *
import json
host, port = "socket.cryptohack.org", 13389
r = remote(host, port)
with open("message1.bin", "rb") as f:
    file1_hex = f.read().hex()
with open("message2.bin", "rb") as f:
    file2_hex = f.read().hex()
payload1 = {"document": file1_hex}
payload2 = {"document": file2_hex}
r.sendlineafter("Give me a document to store\n", json.dumps(payload1).encode())
response1 = r.recvline().decode().strip()
print(json.loads(response1))
r.sendline(json.dumps(payload2).encode())
response = r.recvline().decode().strip()
print(response)
```
`crypto{m0re_th4n_ju5t_p1g30nh0le_pr1nc1ple}`

## Hash stuffing 
Source code của bài:
```python
# 2^128 collision protection!
BLOCK_SIZE = 32

# Nothing up my sleeve numbers (ref: Dual_EC_DRBG P-256 coordinates)
W = [0x6b17d1f2, 0xe12c4247, 0xf8bce6e5, 0x63a440f2, 0x77037d81, 0x2deb33a0, 0xf4a13945, 0xd898c296]
X = [0x4fe342e2, 0xfe1a7f9b, 0x8ee7eb4a, 0x7c0f9e16, 0x2bce3357, 0x6b315ece, 0xcbb64068, 0x37bf51f5]
Y = [0xc97445f4, 0x5cdef9f0, 0xd3e05e1e, 0x585fc297, 0x235b82b5, 0xbe8ff3ef, 0xca67c598, 0x52018192]
Z = [0xb28ef557, 0xba31dfcb, 0xdd21ac46, 0xe2a91e3c, 0x304f44cb, 0x87058ada, 0x2cb81515, 0x1e610046]

# Lets work with bytes instead!
W_bytes = b''.join([x.to_bytes(4,'big') for x in W])
X_bytes = b''.join([x.to_bytes(4,'big') for x in X])
Y_bytes = b''.join([x.to_bytes(4,'big') for x in Y])
Z_bytes = b''.join([x.to_bytes(4,'big') for x in Z])

def pad(data):
    padding_len = (BLOCK_SIZE - len(data)) % BLOCK_SIZE
    return data + bytes([padding_len]*padding_len)

def blocks(data):
    return [data[i:(i+BLOCK_SIZE)] for i in range(0,len(data),BLOCK_SIZE)]

def xor(a,b):
    return bytes([x^y for x,y in zip(a,b)])

def rotate_left(data, x):
    x = x % BLOCK_SIZE
    return data[x:] + data[:x]

def rotate_right(data, x):
    x = x % BLOCK_SIZE
    return  data[-x:] + data[:-x]

def scramble_block(block):
    for _ in range(40):
        block = xor(W_bytes, block)
        block = rotate_left(block, 6)
        block = xor(X_bytes, block)
        block = rotate_right(block, 17)
    return block

def cryptohash(msg):
    initial_state = xor(Y_bytes, Z_bytes)
    msg_padded = pad(msg)
    msg_blocks = blocks(msg_padded)
    for i,b in enumerate(msg_blocks):
        mix_in = scramble_block(b)
        for _ in range(i):
            mix_in = rotate_right(mix_in, i+11)
            mix_in = xor(mix_in, X_bytes)
            mix_in = rotate_left(mix_in, i+6)
        initial_state = xor(initial_state,mix_in)
    return initial_state.hex()
```
Phân tích: Bài này cho ta một hàm hash `cryptohash(x)`. Đầu tiên nó sẽ tạo ra một `iv` bằng cách XOR hai giá trị `Y_bytes` và `Z_bytes`. msg ban đầu của ta sẽ được pad theo kiểu pkcs#7. Bước tiếp theo nó sẽ chia dữ liệu ra thành các blocks có kích thước bằng nhau sau đó sẽ tiến hành tính toán hash.

Cách attack bài này đó là mình sẽ lợi dụng hàm pad như script dưới đây: Đầu tiên mình tạo m1 gồm 32 bytes `b'\x01'` rồi sau đó tạo một m2 chỉ gồm 31 bytes `b'\x01'`. Lúc này khi đưa vào hàm hash để tính thì bước đầu tiên nó làm sẽ là pad cho đủ 32 bytes. Do m2 thiếu đúng 1 bytes cho nên nó sẽ pad thêm vào `b'\x01'` và chính là m1. 
```python
import json
from pwn import *
BLOCK_SIZE = 32
def pad(data):
    padding_len = (BLOCK_SIZE - len(data)) % BLOCK_SIZE
    return data + bytes([padding_len]*padding_len)
m1=b'\x01'*32
print(m1)
m2=b'\x01'*31
print(len(m2))
print(m2)
assert m1==pad(m2)
r = remote('socket.cryptohack.org', 13405)
response = r.recvuntil(b'JSON: ')
print(response)
r.send(json.dumps({'m1': m1.hex(), 'm2': m2.hex()}).encode())
flag = r.recvline()
print(flag)
```
`crypto{Always_add_padding_even_if_its_a_whole_block!!!}`

## PriMeD5

Source code của bài:
```python
from Crypto.PublicKey import RSA
from Crypto.Hash import MD5
from Crypto.Signature import pkcs1_15
from Crypto.Util.number import long_to_bytes, isPrime
import math
from utils import listener
# from secrets import N, E, D

FLAG = "crypto{??????????????????}"


key = RSA.construct((N, E, D))
sig_scheme = pkcs1_15.new(key)


class Challenge():
    def __init__(self):
        self.before_input = "Primality checking is expensive so I made a service that signs primes, allowing anyone to quickly check if a number is prime\n"

    def challenge(self, msg):
        if "option" not in msg:
            return {"error": "You must send an option to this server."}

        elif msg["option"] == "sign":
            p = int(msg["prime"])
            if p.bit_length() > 1024:
                return {"error": "The prime is too large."}
            if not isPrime(p):
                return {"error": "You must specify a prime."}

            hash = MD5.new(long_to_bytes(p))
            sig = sig_scheme.sign(hash)
            return {"signature": sig.hex()}

        elif msg["option"] == "check":
            p = int(msg["prime"])
            sig = bytes.fromhex(msg["signature"])
            hash = MD5.new(long_to_bytes(p))
            try:
                sig_scheme.verify(hash, sig)
            except ValueError:
                return {"error": "Invalid signature."}

            a = int(msg["a"])
            if a < 1:
                return {"error": "`a` value invalid"}
            if a >= p:
                return {"error": "`a` value too large"}
            g = math.gcd(a, p)
            flag_byte = FLAG[:g]
            return {"msg": f"Valid signature. First byte of flag: {flag_byte}"}

        else:
            return {"error": "Unknown option."}


import builtins; builtins.Challenge = Challenge # hack to enable challenge to be run locally, see https://cryptohack.org/faq/#listener
listener.start_server(port=13392)
```
Phân tích: Bài này cho ta hai option là sign và check. Để lấy lại flag thì ta cần phải chọn option check. Server sẽ check và trả về một phần của flag:
```python
a = int(msg["a"])
            if a < 1:
                return {"error": "`a` value invalid"}
            if a >= p:
                return {"error": "`a` value too large"}
            g = math.gcd(a, p)
            flag_byte = FLAG[:g]
            return {"msg": f"Valid signature. First byte of flag: {flag_byte}"}
```

Nếu chữ kí là hợp lệ thì nó sẽ gửi về cho ta `g` bytes đầu tiên của flag. Vấn đề là ... ta biết rằng nếu $p$ là số nguyên tố thì ta chỉ có thể có $gcd(a,p)=1$ hoặc $gcd(a,p)=p$. Hơn nữa ta không thể xài trick lỏ gửi $a$ là bội của $p$ tới server được vì server sẽ loại trường hợp $\displaystyle a\geqslant p$. =))) Ý tưởng của mình đó là vì option check nó không check xem số $p$ mà mình gửi tới có phải là số nguyên tố hay không. Vậy mình chỉ cần tạo một hợp số rồi chọn $a$ là ước của nó là được. 
Tiếp theo đó là sig được kí từ bên phía server nên mình không thể tự khôi phục lại sig được. Mình buộc phải gửi trước 1 số nguyên tố tới server để lấy sig rồi dùng sig này để verfiy cho hợp số ??? Vậy là ta cần chọn một cặp số nguyên tố - hợp số mà có hash giống nhau

Có thể sinh ra một cặp số như vậy bằng cách sử dụng Length Extension Attack của MD5:
```python
# https://crypto.stackexchange.com/questions/105669/quickest-way-to-find-md5-collision
from Crypto.Util.number import isPrime, bytes_to_long, long_to_bytes
import hashlib

x = "4dc968ff0ee35c209572d4777b721587d36fa7b21bdc56b74a3dc0783e7b9518afbfa200a8284bf36e8e4b55b35f427593d849676da0d1555d8360fb5f07fea2"
y = "4dc968ff0ee35c209572d4777b721587d36fa7b21bdc56b74a3dc0783e7b9518afbfa202a8284bf36e8e4b55b35f427593d849676da0d1d55d8360fb5f07fea2"

print("x : ", bytes_to_long(bytes.fromhex(x)))

print("md5(x) : ", hashlib.md5(bytes.fromhex(x)).hexdigest())
print("md5(y) : ", hashlib.md5(bytes.fromhex(y)).hexdigest())

z = 1

xx = 0
yy = 0

while True:
    # append 1s till prime
    xx = bytes_to_long(bytes.fromhex(x) + long_to_bytes(z))
    yy = bytes_to_long(bytes.fromhex(y) + long_to_bytes(z))
    if isPrime(xx) and not isPrime(yy):
        break
    z += 2

print("x+z :", xx)
print("y+z :", yy)

print("md5(x+z) : ", hashlib.md5(long_to_bytes(xx)).hexdigest())
print("md5(y+z) : ", hashlib.md5(long_to_bytes(yy)).hexdigest())
```
Ta được 2 số 
```
p1=1042949915673747639548394979539773519387432406920217853474982925582324441002369106807062644005773384014539089496972340217284225886262811961269251256830829063
p2=1042949915673747639548394979539773519387432406920217853474982925582324441002369106807076447498466965142113959008696894268189128104207757197289383619865780743
```
Script giải bài:
```python
import hashlib
from pwn import *
import json
r=remote("socket.cryptohack.org",13392)
p1=1042949915673747639548394979539773519387432406920217853474982925582324441002369106807062644005773384014539089496972340217284225886262811961269251256830829063
p2=1042949915673747639548394979539773519387432406920217853474982925582324441002369106807076447498466965142113959008696894268189128104207757197289383619865780743
payload1 = {"option": "sign","prime":p1}
r.recvline()
r.send(json.dumps(payload1).encode())
response=r.recvline().decode().strip()
payload=json.loads(response)
print(payload)
sig=payload["signature"]
payload2={"option":"check","prime":p2,"signature":sig,"a":298319899459}
r.send(json.dumps(payload2).encode())
response=r.recvline().decode().strip()
print(response)
```

`crypto{MD5_5uck5_p4rt_tw0}`
## Twin Keys
Source code của bài:
```python
import os
import random
from Crypto.Hash import MD5
from utils import listener

KEY_START = b"CryptoHack Secure Safe"
FLAG = b"crypto{????????????????????????????}"


def xor(a, b):
    assert len(a) == len(b)
    return bytes(x ^ y for x, y in zip(a, b))


class SecureSafe:
    def __init__(self):
        self.magic1 = os.urandom(16)
        self.magic2 = os.urandom(16)
        self.keys = {}

    def insert_key(self, key):
        if len(self.keys) >= 2:
            return {"error": "All keyholes are already occupied"}
        if key in self.keys:
            return {"error": "This key is already inserted"}

        self.keys[key] = 0
        if key.startswith(KEY_START):
            self.keys[key] = 1

        return {"msg": f"Key inserted"}

    def unlock(self):
        if len(self.keys) < 2:
            return {"error": "Missing keys"}

        if sum(self.keys.values()) != 1:
            return {"error": "Invalid keys"}

        hashes = []
        for k in self.keys.keys():
            hashes.append(MD5.new(k).digest())

        # Encrypting the hashes with secure quad-grade XOR encryption
        # Using different randomized magic numbers to prevent the hashes
        # from ever being equal
        h1 = hashes[0]
        h2 = hashes[1]
        for i in range(2, 2**(random.randint(2, 10))):
            h1 = xor(self.magic1, xor(h2, xor(xor(h2, xor(h1, h2)), h2)))
            h2 = xor(xor(xor(h1, xor(xor(h2, h1), h1)), h1), self.magic2)

        assert h1 != bytes(bytearray(16))

        if h1 == h2:
            return {"msg": f"The safe clicks and the door opens. Amongst its secrets you find a flag: {FLAG}"}
        return {"error": "The keys does not match"}


class Challenge():
    def __init__(self):
        self.securesafe = SecureSafe()
        self.before_input = "Can you help find our lost keys to unlock the safe?\n"

    def challenge(self, your_input):
        if not 'option' in your_input:
            return {"error": "You must send an option to this server"}
        elif your_input['option'] == 'insert_key':
            key = bytes.fromhex(your_input["key"])
            return self.securesafe.insert_key(key)
        elif your_input['option'] == 'unlock':
            return self.securesafe.unlock()
        else:
            return {"error": "Invalid option"}


import builtins; builtins.Challenge = Challenge # hack to enable challenge to be run locally, see https://cryptohack.org/faq/#listener
listener.start_server(port=13397)
```
Phân tích: Điều kiện để server nhả về flag là như sau:
```python
        if h1 == h2:
            return {"msg": f"The safe clicks and the door opens. Amongst its secrets you find a flag: {FLAG}"}
        return {"error": "The keys does not match"}
```

Trước đó thì hai giá trị này được đưa vào một phép xor với 2 giá trị random. 
```python
        self.magic1 = os.urandom(16)
        self.magic2 = os.urandom(16)
```
Nên tương tự như các bài khác, ta cần tạo ra 2 msg có prefix giống nhau nhưng khác nhau ở phần còn lại, đồng thời MD5 hash của chúng phải bằng nhau. 

Hmmm mình đi tìm hiểu một số tool thì có một tool gọi là Hashclash có hỗ trợ việc tạo ra các file như vậy. 
Tải tool về tại [đây](https://github.com/cr-marcstevens/hashclash)
Sau khi tải về ta chạy các lệnh sau:
`echo -n "CryptoHack Secure Safe22" > prefix.txt`
`../scripts/generic_ipc.sh prefix.txt`

Lý do mình thêm 22 ở sau vì tool yêu cầu độ dài của prefix nên chia hết cho 64 (64 bytes) hoặc ít nhất nó là bội của 4. 

Sau khi chạy thì nó sẽ trả về hai file `collision1.bin` và `collision2.bin`
![image](https://hackmd.io/_uploads/SkE94WoWge.png)

Có thể kiểm tra md5 sum của chúng như sau:
![image](https://hackmd.io/_uploads/S1KTEbobxx.png)

V là oke

```python
from pwn import *
import json
host, port = "socket.cryptohack.org", 13397
r = remote(host, port)
with open("collision1.bin", "rb") as f:
    k1 = f.read().hex()
with open("collision2.bin", "rb") as f:
    k2 = f.read().hex()
print(r.recv().decode())
print(k1)
print(k2)
payload1 = {"option":"insert_key","key":k1}
r.sendline(json.dumps(payload1).encode())
r.recvline()
payload2 = {"option":"insert_key","key":k2}
r.sendline(json.dumps(payload2).encode())
r.recvline()
payload3 = {"option":"unlock"}
r.sendline(json.dumps(payload3).encode())
response=r.recvline().decode().strip()
print(response)
```
`crypto{MD5_15_0n_4_c0ll151On_c0uRz3}`

## No Difference
Source code của bài:
```python
from utils import listener

SBOX = [
    0xf0, 0xf3, 0xf1, 0x69, 0x45, 0xff, 0x2b, 0x4f, 0x63, 0xe1, 0xf3, 0x71, 0x44, 0x1b, 0x35, 0xc8,
    0xbe, 0xc0, 0x1a, 0x89, 0xec, 0x3e, 0x1d, 0x3a, 0xe3, 0xbe, 0xd3, 0xcf, 0x20, 0x4e, 0x56, 0x22,
    0xe4, 0x43, 0x9a, 0x6f, 0x43, 0xa9, 0x87, 0x37, 0xec, 0x2, 0x3b, 0x8a, 0x7a, 0x13, 0x7e, 0x79,
    0xcc, 0x92, 0xd7, 0xd1, 0xff, 0x5e, 0xe2, 0xb1, 0xc9, 0xd3, 0xda, 0x40, 0xfb, 0x80, 0xe6, 0x30,
    0x79, 0x1a, 0x28, 0x13, 0x1f, 0x2c, 0x73, 0xb9, 0x71, 0x9e, 0xa6, 0xd5, 0x30, 0x84, 0x9d, 0xa1,
    0x9b, 0x6d, 0xf9, 0x8a, 0x3d, 0xe9, 0x47, 0x15, 0x50, 0xb, 0xe2, 0x3d, 0x3f, 0x1, 0x59, 0x9b,
    0x85, 0xe4, 0xe5, 0x90, 0xe2, 0x2d, 0x80, 0x5e, 0x6b, 0x77, 0xa1, 0x10, 0x99, 0x72, 0x7f, 0x86,
    0x1f, 0x25, 0xa3, 0xea, 0x57, 0x5f, 0xc4, 0xc6, 0x7d, 0x7, 0x15, 0x90, 0xcb, 0x8c, 0xec, 0x11,
    0x9b, 0x59, 0x1, 0x3f, 0x3d, 0xe2, 0xb, 0x50, 0x15, 0x47, 0xe9, 0x3d, 0x8a, 0xf9, 0x6d, 0x9b,
    0xa1, 0x9d, 0x84, 0x30, 0xd5, 0xa6, 0x9e, 0x71, 0xb9, 0x73, 0x2c, 0x1f, 0x13, 0x28, 0x1a, 0x79,
    0x11, 0xec, 0x8c, 0xcb, 0x90, 0x15, 0x7, 0x7d, 0xc6, 0xc4, 0x5f, 0x57, 0xea, 0xa3, 0x25, 0x1f,
    0x86, 0x7f, 0x72, 0x99, 0x10, 0xa1, 0x77, 0x6b, 0x5e, 0x80, 0x2d, 0xe2, 0x90, 0xe5, 0xe4, 0x85,
    0x22, 0x56, 0x4e, 0x20, 0xcf, 0xd3, 0xbe, 0xe3, 0x3a, 0x1d, 0x3e, 0xec, 0x89, 0x1a, 0xc0, 0xbe,
    0xc8, 0x35, 0x1b, 0x44, 0x71, 0xf3, 0xe1, 0x63, 0x4f, 0x2b, 0xff, 0x45, 0x69, 0xf1, 0xf3, 0xf0,
    0x30, 0xe6, 0x80, 0xfb, 0x40, 0xda, 0xd3, 0xc9, 0xb1, 0xe2, 0x5e, 0xff, 0xd1, 0xd7, 0x92, 0xcc,
    0x79, 0x7e, 0x13, 0x7a, 0x8a, 0x3b, 0x2, 0xec, 0x37, 0x87, 0xa9, 0x43, 0x6f, 0x9a, 0x43, 0xe4,
]
FLAG = "crypto{??????????????????}"


# permute has the following properties:
# permute(permute(x)) = x
# permute(a) ^ permute(b) = permute(a ^ b)
def permute(block):
    result = [0 for _ in range(8)]
    for i in range(8):
        x = block[i]
        for j in range(8):
            result[j] |= (x & 1) << i
            x >>= 1
    return result


def substitute(block):
    return [SBOX[x] for x in block]


def hash(data):
    if len(data) % 4 != 0:
        return None

    state = [16, 32, 48, 80, 80, 96, 112, 128]
    for i in range(0, len(data), 4):
        block = data[i:i+4]
        state[4] ^= block[0]
        state[5] ^= block[1]
        state[6] ^= block[2]
        state[7] ^= block[3]
        state = permute(state)
        state = substitute(state)

    for _ in range(16):
        state = permute(state)
        state = substitute(state)

    output = []
    for _ in range(2):
        output += state[4:]
        state = permute(state)
        state = substitute(state)

    return bytes(output)


class Challenge:
    def __init__(self):
        self.before_input = '"The difference between treason and patriotism is only a matter of dates."\n'

    def challenge(self, msg):
        a = bytes.fromhex(msg['a'])
        b = bytes.fromhex(msg['b'])
        if len(a) % 4 != 0 or len(b) % 4 != 0:
            return {"error": "Inputs must be multiple of the block length!"}
        if a == b:
            return {"error": "Identical inputs are not allowed!"}
        if hash(a) == hash(b):
            return {"flag": f"Well done, here is the flag: {FLAG}"}
        else:
            return {"error": "The hashes don't match!"}


import builtins; builtins.Challenge = Challenge # hack to enable challenge to be run locally, see https://cryptohack.org/faq/#listener
listener.start_server(port=13395)
```

Phân tích: Bài này cho ta một hàm hash custom. Có thể tóm tắt lại các bước như sau.
Đầu tiên ta có một bảng SBOX. Bảng này dùng trong hàm `substitue` để thay mỗi byte trong block thành 1 byte trong bảng. 

Tiếp theo là hàm Hash của ta. 

Hàm hash này yêu cầu dữ liệu đầu vào phải có độ dài chia hết cho 4. Sau đó nó sẽ chia data thành các block có độ dài là 4. Và xử lí riêng cho từng block.

```python
    state = [16, 32, 48, 80, 80, 96, 112, 128]
    for i in range(0, len(data), 4):
        block = data[i:i+4]
        state[4] ^= block[0]
        state[5] ^= block[1]
        state[6] ^= block[2]
        state[7] ^= block[3]
        state = permute(state)
        state = substitute(state)
```
Mỗi kí tự trong block sẽ được XOR lần lượt với các phần tử trong mảng state. Sau mỗi lần XOR xong thì state sẽ được truyền vào hàm permute rồi qua một lần hàm `substitute` nữa. 
Sau đó thì nó lặp lại liên tiếp 2 hàm permute với substitute rồi output ra kết quả hash.

Điều kiện để trả về flag như sau:
```python
    def challenge(self, msg):
        a = bytes.fromhex(msg['a'])
        b = bytes.fromhex(msg['b'])
        if len(a) % 4 != 0 or len(b) % 4 != 0:
            return {"error": "Inputs must be multiple of the block length!"}
        if a == b:
            return {"error": "Identical inputs are not allowed!"}
        if hash(a) == hash(b):
            return {"flag": f"Well done, here is the flag: {FLAG}"}
        else:
            return {"error": "The hashes don't match!"}
```
Ta cần nhập 2 msg có hash bằng nhau như mọi bài trc thôi.
Vì hàm hash này chủ yếu hoạt động xoay quay 2 hàm chính là permute với substitute nên mình nghĩ là cần phải khai thác điểm yếu của 2 hàm này. 
Lướt sơ qua thì mình thấy rằng bảng tra cứu SBOX không thực sự là đơn ánh 1-1 tức là có một số kí tự bị lặp lại trong bảng. Vậy thì ý tưởng của mình là như sau: Ở bước xử lí đầu tiên trước khi đưa vào vòng lặp 16 lần, mình cần chọn 2 msg, sao cho sau khi qua hàm permute sẽ cho output khác nhau nhưng thay vào bảng SBOX thì lại cho kqua giống nhau. Nếu sau bước này 2 msg là giống nhau thì ở 16 lần lặp sau đó kết quả cũng sẽ giữ nguyên không đổi.

Nhưng vấn đề của cách này đó là sau khi tìm được 2 msg thỏa sub qua SBOX bằng nhau thì khi gọi permute để đảo lại ta không thể đảm bảo 4 phần tử đầu tiên của nó trùng với state. 

Script:
```python
SBOX = [
    0xf0, 0xf3, 0xf1, 0x69, 0x45, 0xff, 0x2b, 0x4f, 0x63, 0xe1, 0xf3, 0x71, 0x44, 0x1b, 0x35, 0xc8,
    0xbe, 0xc0, 0x1a, 0x89, 0xec, 0x3e, 0x1d, 0x3a, 0xe3, 0xbe, 0xd3, 0xcf, 0x20, 0x4e, 0x56, 0x22,
    0xe4, 0x43, 0x9a, 0x6f, 0x43, 0xa9, 0x87, 0x37, 0xec, 0x2, 0x3b, 0x8a, 0x7a, 0x13, 0x7e, 0x79,
    0xcc, 0x92, 0xd7, 0xd1, 0xff, 0x5e, 0xe2, 0xb1, 0xc9, 0xd3, 0xda, 0x40, 0xfb, 0x80, 0xe6, 0x30,
    0x79, 0x1a, 0x28, 0x13, 0x1f, 0x2c, 0x73, 0xb9, 0x71, 0x9e, 0xa6, 0xd5, 0x30, 0x84, 0x9d, 0xa1,
    0x9b, 0x6d, 0xf9, 0x8a, 0x3d, 0xe9, 0x47, 0x15, 0x50, 0xb, 0xe2, 0x3d, 0x3f, 0x1, 0x59, 0x9b,
    0x85, 0xe4, 0xe5, 0x90, 0xe2, 0x2d, 0x80, 0x5e, 0x6b, 0x77, 0xa1, 0x10, 0x99, 0x72, 0x7f, 0x86,
    0x1f, 0x25, 0xa3, 0xea, 0x57, 0x5f, 0xc4, 0xc6, 0x7d, 0x7, 0x15, 0x90, 0xcb, 0x8c, 0xec, 0x11,
    0x9b, 0x59, 0x1, 0x3f, 0x3d, 0xe2, 0xb, 0x50, 0x15, 0x47, 0xe9, 0x3d, 0x8a, 0xf9, 0x6d, 0x9b,
    0xa1, 0x9d, 0x84, 0x30, 0xd5, 0xa6, 0x9e, 0x71, 0xb9, 0x73, 0x2c, 0x1f, 0x13, 0x28, 0x1a, 0x79,
    0x11, 0xec, 0x8c, 0xcb, 0x90, 0x15, 0x7, 0x7d, 0xc6, 0xc4, 0x5f, 0x57, 0xea, 0xa3, 0x25, 0x1f,
    0x86, 0x7f, 0x72, 0x99, 0x10, 0xa1, 0x77, 0x6b, 0x5e, 0x80, 0x2d, 0xe2, 0x90, 0xe5, 0xe4, 0x85,
    0x22, 0x56, 0x4e, 0x20, 0xcf, 0xd3, 0xbe, 0xe3, 0x3a, 0x1d, 0x3e, 0xec, 0x89, 0x1a, 0xc0, 0xbe,
    0xc8, 0x35, 0x1b, 0x44, 0x71, 0xf3, 0xe1, 0x63, 0x4f, 0x2b, 0xff, 0x45, 0x69, 0xf1, 0xf3, 0xf0,
    0x30, 0xe6, 0x80, 0xfb, 0x40, 0xda, 0xd3, 0xc9, 0xb1, 0xe2, 0x5e, 0xff, 0xd1, 0xd7, 0x92, 0xcc,
    0x79, 0x7e, 0x13, 0x7a, 0x8a, 0x3b, 0x2, 0xec, 0x37, 0x87, 0xa9, 0x43, 0x6f, 0x9a, 0x43, 0xe4,
]
FLAG = "crypto{??????????????????}"
# permute has the following properties:
# permute(permute(x)) = x
# permute(a) ^ permute(b) = permute(a ^ b)
def permute(block):
    result = [0 for _ in range(8)]
    for i in range(8):
        x = block[i]
        for j in range(8):
            result[j] |= (x & 1) << i
            x >>= 1
    return result
def substitute(block):
    return [SBOX[x] for x in block]
def hash(data):
    if len(data) % 4 != 0:
        return None

    state = [16, 32, 48, 80, 80, 96, 112, 128]
    for i in range(0, len(data), 4):
        block = data[i:i+4]
        state[4] ^= block[0]
        state[5] ^= block[1]
        state[6] ^= block[2]
        state[7] ^= block[3]
        state = permute(state)
        print(state)
        state = substitute(state)
    for _ in range(16):
        state = permute(state)
        state = substitute(state)
    output = []
    for _ in range(2):
        output += state[4:]
        state = permute(state)
        state = substitute(state)
    return bytes(output)
def inv_permute(block):
    return permute(block)
a = [0,0,0,0]
b = [0,0,0,0]
state = [16, 32, 48, 80, 80, 96, 112, 128]

for _ in range(2):
    state = permute(state)
    state = substitute(state)
    a+=state[4:]
    b+=state[4:]
    state[4:] = [0]*4
a = a[:-4]
print(hash(b))
print(b)
assert hash(a) == hash(b)
from pwn import *
import json
r=remote("socket.cryptohack.org" ,13395)
r.recvline()
r.sendline(json.dumps({"a" : bytes(a).hex(), "b" : bytes(b).hex()}))
print(r.recvline().decode().strip())
```
`crypto{n0_d1ff_n0_pr0bl3m}`

## Mixed Up
Source code của bài:
```python
from hashlib import sha256
import os
from utils import listener


FLAG = b"crypto{???????????????????????????????}"


def _xor(a, b):
    return bytes([_a ^ _b for _a, _b in zip(a, b)])

def _and(a, b):
    return bytes([_a & _b for _a, _b in zip(a, b)])

def shuffle(mixed_and, mixed_xor):
    return bytes([mixed_xor[i%len(mixed_xor)] for i in mixed_and])


class Challenge():
    def __init__(self):
        self.before_input = "Oh no, how are you going to unmix this?\n"

    def challenge(self, msg):
        if "option" not in msg:
            return {"error": "You must send an option to this server."}

        elif msg["option"] == "mix":
            if not "data" in msg:
                return {"error": "Please send hex-encoded data"}

            data = bytes.fromhex(msg["data"])
            if len(data) < len(FLAG):
                data += os.urandom(len(FLAG) - len(data))

            mixed_and = _and(FLAG, data)
            mixed_xor = _xor(_xor(FLAG, data), os.urandom(len(FLAG)))

            very_mixed = shuffle(mixed_and, mixed_xor)
            super_mixed = sha256(very_mixed).hexdigest()

            return {"mixed": super_mixed}

        else:
            return {"error": "Invalid option"}


import builtins; builtins.Challenge = Challenge # hack to enable challenge to be run locally, see https://cryptohack.org/faq/#listener
"""
When you connect, the 'challenge' function will be called on your JSON
input.
"""
listener.start_server(port=13402)

```
Phân tích:
Chall cho ta nhập vào một chuỗi giá trị (option duy nhất ta được chọn là option "mix"). Lúc này server sẽ lấy data của ta và thực hiện AND nó với Flag ban đầu. Sau đó nó tiếp tục XOR data của ta với Flag và XOR tiếp với một chuỗi ngẫu nhiên khác.
Sau đó 2 giá trị trên sẽ được đưa vào hàm mixed và trả về cho ta giá trị hash SHA256 của nó. 

Đầu tiên mình xem lại hàm shuffle nó đang làm gì:
```python
def shuffle(mixed_and, mixed_xor):
    return bytes([ mixed_xor[i % len(mixed_xor)] for i in mixed_and ])
```
Tức là nó lặp qua từng bytes `i` của `mixed_and` rồi sau đó đổi thành `mixed_xor[i % len(FLAG)]`.
Mình nghĩ đây có thể là điểm yếu để khai thác :V? Và hơn thế nữa là server cho mình gửi nhiều lần (ngon) nên mình sẽ tìm cách kiểm soát đầu vào coi sao. 
**Ý tưởng 1.** Mình thử gửi các chuỗi bytes có dạng đặc biệt một chút. Chẳng hạn `b'\xff' * l` hoặc `b'\x00'*l` với `l = len(FLAG)`. Ở đây bài cho ta `len(FLAG) = 39`
Sẽ có 4 giá trị được tính:
```python
            mixed_and = _and(FLAG, data)
            mixed_xor = _xor(_xor(FLAG, data), os.urandom(len(FLAG)))

            very_mixed = shuffle(mixed_and, mixed_xor)
            super_mixed = sha256(very_mixed).hexdigest()
```

Đầu tiên là `mixed_and`. 
Nếu như `data = b'\xff' * l` thì `_and(FLAG,data) = FLAG`. Nhưng khi tới bước tiếp theo khi vào hàm XOR thì nó sẽ đảo các bit của `FLAG` lại và khi XOR với `os.urandom()` thì nó cũng không ra đuộc chuỗi giá trị có gì đặc biệt. 
Còn nếu mình gửi `b'\x00' * l` thì sao.
Lúc này `mixed_and = 0`. 
Sau đó khi đưa vào hàm XOR thì FLAG được giữ nguyên và được XOR với `os.urandom()`
Lúc này mình để ý tới hàm `shuffle`
Giá trị `i` dùng để tính chỉ số bây giờ sẽ toàn là `00` cho nên `mixed_xor` của ta bây giờ chỉ chứa các phần tử ở vị trí `0` của mảng ban đầu. Như vậy thì sao?
Giả sử ta biết giá trị `super_mixed`, ta biết đây là SHA256 của 1 chuỗi bytes có độ dài là flag với các kí tự được lặp lại. Các kí tự đều chỉ nằm trong khoảng $[0,255]$. Nếu bruteforce ta có thể tìm lại được kí tự này, bằng cách tính SHA256 với các đầu vào cho trước, kí tự này cũng chính là kí tự đầu của `mixed_xor`. Nếu biết kí tự đầu của `mixed_xor` thì ta cũng . . . không làm được gì =)) ta chỉ biết `mixed_xor` là XOR giữa flag và một bytes random nào đó thôi. Nhưng từ cách phân tích này mình có thể định hướng được bước đi tiếp theo cho bản thân đó là tìm cách precompute các giá trị có thể có từ image của SHA256 để tìm lại flag. 

**Ý tưởng 2.** 
Bây giờ, thay vì gửi full `b'\x00' * l` thì mình chỉ gửi `b'\x00' * (l-1)` coi sao. 
Thì lúc này vẫn như trên ta sẽ có `mixed_and` sẽ chứa toàn các kí tự 0 với độ dài là `l-1` và sẽ được pad thêm 1 bytes cuối ngẫu nhiên. 

Tương tự với `mixed_xor` cũng là một chuỗi bytes có độ dài `l` trong đó kí tự cuối của FLAG đã được XOR với 1 bytes ngẫu nhiên. Sau đó ta sẽ XOR giá trị này với một chuỗi bytes ngẫu nhiên khác. 
