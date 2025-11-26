## Noisy Neighbour 

Source code của bài:
```python
import random
from Crypto.Util.number import getPrime, long_to_bytes
from Crypto.Cipher import AES

ticket = random.getrandbits(128)
FLAG = ""
with open('flag.txt', 'r') as flag:
    FLAG = flag.read()

p = getPrime(1024)
q = getPrime(1024)
N = p * q
phi = (p - 1) * (q - 1)

e = getPrime(16) + (random.getrandbits(128) * phi)
enc_ticket = pow(ticket, e, N)

print(f"{N=}")
print(f"{e=}")
print(f"{enc_ticket=}")

cipher = AES.new(long_to_bytes(ticket), AES.MODE_CTR)
nonce = cipher.nonce
enc_flag = cipher.encrypt(FLAG.encode())

print(f"{enc_flag, nonce=}")
```
Phân tích: 
Ở bài này ta thấy $e$ được tạo bởi 
```python
e= getPrime(16) + (random.getrandbits(128)*phi)
```
tức là nó có dạng $e=r+k\phi(n)$ với $r$ là một số nguyên tố nào đó. Cho nên khi ta lấy `ticket` lũy thừa cho giá trị này thì kết quả bằng với việc lấy `ticket` lũy thừa với $r$ theo định lý Euler. 

Để lấy được giá trị của `ticket` rồi giải mã cho flag thì ta cần tìm lại $r$ và $\phi(n)$. Thực ra ta có thể thử lấy $e-r$ với $r$ là các prime 16 bit. Ta có thể tự tạo một list các primes như vậy từ trước. Sau đó ta sẽ lấy $d$ là nghịch đảo của $e$ theo $e-r$ vì nếu $ed \equiv 1 \bmod k\phi(n)$ thì nó cũng sẽ thỏa $ed \equiv 1 \bmod \phi(n)$ và việc giải mã RSA vẫn được. 
Solve script:
```python
from Crypto.Util.number import * 
from Crypto.Cipher import AES
N=10347242542600406308094534195263088635791365996714020803160250407603636995099715433829129670160192589093770515128152510439089971458386641765448309859819378023880272965050178277879093516918807566027042642100169240017844173793930784667163759562215010481356537422986546632994001754291723194969521748076910835396937977810627980887157551885113202531423733595088875369751631232226097581969479909313254958049277471499732135617616297332871531530596176518111563310557213028740425533103112982126293232786326119238512934754974514742881890899165547139605333761970683944591937361699420431036603767467012489183290578309164784178633
e=3311986667073495779819661492647781665180928338729865042826968893121477288104028672415705332665972755867861711304085148957997662937288947383110908043717598599426017484422084809208910486092822909662298925085867663251659781025068175951771651187222278814345138470007111789992552003468482347964267103806504197977364231330649526292875722283219443425291497285240653190201781346512871589039622122806771109809220085787813190940121150761761463256791250036396820146924876913040030532187290384737376868592733044732294197676117676820815598675412056870600146382869883717018539905436358459822165326225070894181935206514146099686162267119751019096873609300804816456005907
enc_ticket=3946420937017846250393019311609396457338463614723557172414418971956390767261563151514428488890805225021688212721862533753952638354812535035364278722859438604041154655180097577414599710778354857775161040850623041785446044819204867397065653667589062151439260152909905577160138599029484856249429267771263679704326352858922042179435551285375575126876142413991900659195467217772357193174598528534725223102658732326697336473387891654610296170800740197748092566321210843941286260968460061251471684295914144882122101706465054524774059725005866235986370176677629767819073609117398726398647883974883695216900279944685266429904
enc_flag, nonce=(b'`\x8d\x9e\x1e\xd4!\xf5\xe3\xf8,\xfb\x16UV\xcc\xae\xe6G\x91F\x06\x157)\x99|;\xb0\xf5\x87\xa2R\xa8\xd4H\xd16\xa6\xd6\xd1r\xe7 C\xd6i\x83\xb9\xf9\xf7f=\xab\x16', b'\xf1\xdbF)\x91\xc5\xb4$')
nbits = 16
cand = []
start = 2**(nbits - 1)        
end = 2**nbits                
for i in range(start+1, end, 2):  
    if isPrime(i):
        cand.append(i)
print(len(cand))
for r in cand:
    e0 = e-r 
    try: 
        d = pow(e,-1,e0)
        ticket = pow(enc_ticket,d,N)
        cipher = AES.new(long_to_bytes(ticket),AES.MODE_CTR,nonce = nonce)
        flag = cipher.decrypt(enc_flag)
        print(flag)
    except ValueError as f:
        continue
```
## AES Zippy 

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
import os
import zlib
import base64
from Crypto.Cipher import AES

KEY = os.urandom(16)
USED_NONCES = []
ADMIN_SECRET = b"Glacier CTF Open"
ADMIN_LOGS = ""
NORMAL_LOGS = ""
MAX_STORAGE = 1 << 16


def decrypt(ct: bytes, nonce: bytes, tag: bytes) -> bytes:
    ad = b"GlacierCTF2025"

    cipher = AES.new(KEY, AES.MODE_GCM, nonce=nonce)
    cipher.update(ad)
    try:
        decrypted = cipher.decrypt_and_verify(ct, tag)
    except:
        raise ValueError("Invalid tag")

    return decrypted


def encrypt(pt: bytes, nonce: bytes = os.urandom(16)):
    ad = b"GlacierCTF2025"

    cipher = AES.new(KEY, AES.MODE_GCM, nonce=nonce)
    cipher.update(ad)

    ct, tag = cipher.encrypt_and_digest(pt)

    return ct, nonce, tag


def test_init():
    global ADMIN_LOGS

    pt = b"Hello GlacierCTF"

    ct, nonce, tag = encrypt(pt)
    assert pt == decrypt(ct, nonce, tag)

    ADMIN_LOGS += f"[+] Nonce: {base64.b64encode(nonce).decode()}\n"
    ADMIN_LOGS += f"[+] Tag: {base64.b64encode(tag).decode()}\n"


def get_size() -> int:
    global ADMIN_LOGS, NORMAL_LOGS, USED_NONCES

    full_state: bytes = ADMIN_LOGS.encode() + NORMAL_LOGS.encode()

    return len(zlib.compress(full_state)) + len(USED_NONCES)*16


def print_help():
    print("[0] Encrypt a file")
    print("[1] Access admin files")


def main():
    global NORMAL_LOGS,ADMIN_LOGS
    print("[+] Welcome to the Glacier encryption service")
    test_init()
    print(ADMIN_LOGS)
    while get_size() < MAX_STORAGE:
        try:
            print_help()
            choice = int(input("Choose action:\n> "))
            if choice == 0:
                pt = bytes.fromhex(input("Plaintext:\n> "))
                nonce = bytes.fromhex(input("Nonce:\n> "))

                if nonce in USED_NONCES or ADMIN_SECRET in pt:
                    return

                USED_NONCES.append(nonce)
                ct, nonce, tag = encrypt(pt, nonce)

                NORMAL_LOGS = f"{pt.hex()=} = {ct.hex()=}, {tag.hex()=}"
                print(NORMAL_LOGS)
                NORMAL_LOGS = f"{pt}"

                print(f"[+] Storage left: {get_size()}/{MAX_STORAGE} bytes")
            elif choice == 1:
                ct = bytes.fromhex(input("Ciphertext:\n> "))
                nonce = bytes.fromhex(input("Nonce:\n> "))
                tag = bytes.fromhex(input("Tag:\n> "))

                pt = decrypt(ct, nonce, tag)

                if ADMIN_SECRET in pt:
                    with open("flag.txt", "r") as flag:
                        print(f"{flag.read()}")
                return
            else:
                return
        except:
            return
    return


if __name__ == "__main__":
    main()
```
Phân tích và tóm tắt: Bài chia làm 2 phần. 
Đầu tiên ta phải tìm cách leak được giá trị nonce và tag của admin. 
Mấu chốt nằm ở hàm `get_size() -> int`
```python
def get_size() -> int:
    global ADMIN_LOGS, NORMAL_LOGS, USED_NONCES

    full_state: bytes = ADMIN_LOGS.encode() + NORMAL_LOGS.encode()

    return len(zlib.compress(full_state)) + len(USED_NONCES)*16
```
Vậy hàm này đang làm gì? 
Hàm này sẽ trả về cho ta biết độ dài của logs đang có sẵn trên server. 
Mỗi lần chạy nó sẽ tính `zlib.compress(data)` rồi cộng với `len(USED_NONCES)*16` -  giá trị này sẽ tăng lên sau mỗi lên ta gọi tới server. 
Khi gọi đến server thì nó sẽ cho ta 2 option. Option đầu tiên là để gửi plaintext và nonce của ta tới server. Nó sẽ mã hóa các giá trị trên và trả về ct, nonce, tag. 
Option 2 được dùng để leak flag từ server. 

Mọi người để ý thì khi gọi xong option 1 nó cũng sẽ trả về cho ta thêm thông tin của hàm `get_size()` với `NORMAL_LOGS` lúc này là plaintext mà ta nhập vào 
```python
print(f"[+] Storage left: {get_size()}/{MAX_STORAGE} bytes")
```

Nếu mọi người có từng làm qua bài tập này trên CryptoHack : https://aes.cryptohack.org/ctrime/ thì biết ngay được trick để giải bài này.

Hàm zlib theo mình hiểu thì nó sẽ rút gọn bớt đi các ký tự trùng lặp, sau đó sẽ nén lại. 

Mọi người có thể thử chạy để thấy sự khác biệt khi nó rút gọn các đầu vào khác nhau:
```python
import zlib known_flag="crypto{CRIM" 
known_flag=known_flag.encode() 
print(len(zlib.compress(known_flag))) print(len(zlib.compress(known_flag+b'crypto{CRIM'))) print(len(zlib.compress(known_flag+b'crypto{CRIN'))) print(len(zlib.compress(known_flag+b'crypto{CRIK')))
```
![[Pasted image 20251126102611.png]]
Phần padding thêm giống với bản gốc càng nhiều thì độ dài càng ngắn. 
Bài trên kia cũng tương tự. 
Mình sẽ gửi nhiều request đến rồi đó xem đầu vào nào làm cho độ dài của `get_size()` là nhỏ nhất thì đó chính là kí tự của `nonce` và `admin_tag`. Sau khi có được `nonce` và `admin_tag` rồi thì mình thực hiện AES - GCM Nonce Reuse Attacks để tính lại GHASH là oke. Chi tiết về attacks mình có viết trong [[Block Cipher Review]].

Solve script:
```python
from gcm_exploit import * 
from pwn import * 
import os 
LOCAL = True
if not LOCAL:
    r = remote("challs.glacierctf.com",13373,timeout=5)
else:
    r = process(["python3","aes.py"])
data = r.recvuntil(b'Choose action:')
print(data)
with open("output.txt","w") as f:
    f.write(str(data))
# r.recvuntil(b'> ')
# r.sendline(str(0))
# r.recvuntil(b'Plaintext:')
# pt = b"[+] Nonce: " + b"A" * 20
# pt = pt.hex()
# r.sendlineafter(b'> ', str(pt))
# r.interactive()
from Crypto.Cipher import AES
ADMIN_SECRET = b"Glacier CTF Open"
MAX_STORAGE = 1 << 16
ad = b"GlacierCTF2025"
known_nonce = ""
alphabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/"
queries = 0 
def query_oracle(pt:bytes):
    global queries # 344 last time
    r.recvuntil(b'> ')
    r.sendline(str(0))
    r.recvuntil(b'Plaintext:')
    pt_ = pt.hex().encode()
    nonce = os.urandom(16).hex().encode()
    r.sendlineafter(b'> ', pt_)
    r.recvuntil(b'Nonce:')
    r.sendlineafter(b'> ', nonce)
    r.recvuntil(b'Storage left:')
    line = r.recvline().strip()
    curr = int(line.split(b'/')[0])
    queries +=1
    eff = curr - 16*queries
    return eff
# lấy lại nonce trước
for pos in range(22):
    best_ch = None
    base_sz = None

    for ch in alphabet:
        cand = known_nonce + ch
        pt = (b"[+] Nonce: " + cand.encode() + b"X") * 5
        sz = query_oracle(pt)

        if base_sz is None:
            base_sz = sz
            best_ch = ch
            continue

        # nếu thấy nhỏ hơn baseline -> chọn luôn, không cần thử tiếp
        if sz < base_sz:
            best_ch = ch
            base_sz = sz
            break

    known_nonce += best_ch
    log.success(f"[nonce_admin prefix] {known_nonce}")
known_tag = ""
# lấy lại tag 
# for pos in range(22):  # 16 bytes -> base64 cũng 24 ký tự
#     best_ch = None
#     best_sz = None
#     for ch in alphabet:
#         cand = known_tag + ch
#         block = (b"[+] Tag: " + cand.encode() + b"X")*5
#         pt = block * 16

#         sz = query_oracle(pt)
#         log.info(f"[tag pos {pos}], try {cand!r} -> size {sz}")

#         if best_sz is None or sz < best_sz:
#             best_sz = sz
#             best_ch = ch
#     known_tag += best_ch
#     log.success(f"[tag_admin prefix] {known_tag}")


for pos in range(22):
    base_sz = None
    best_ch = None

    for ch in alphabet:
        cand = known_tag + ch
        pt = (b"[+] Tag: " + cand.encode() + b"X") * 5
        sz = query_oracle(pt)
        if base_sz is None:
            base_sz = sz
            best_ch = ch
            continue

        if sz < base_sz:
            base_sz = sz
            best_ch = ch
            break
    known_tag += best_ch
    log.success(f"[tag_admin prefix] {known_tag}")

known_nonce = known_nonce + "=="
known_tag = known_tag + "=="
print(known_nonce,"\n")
print(known_tag)
import base64
nonce_admin = base64.b64decode(known_nonce)
tag_admin = base64.b64decode(known_tag)

pt1 = b"B" * 64
r.recvuntil(b"> ")
r.sendline(b"0")
r.recvuntil(b"Plaintext:")
r.recvuntil(b"> ")
r.sendline(pt1.hex().encode())
r.recvuntil(b"Nonce:")
r.recvuntil(b"> ")
r.sendline(nonce_admin.hex().encode())
line = r.recvline().decode().strip()
# dạng: pt.hex()='...' = ct.hex()='...', tag.hex()='...'
import re
m = re.search(
    r"ct\.hex\(\)='([0-9a-f]+)'.*tag\.hex\(\)='([0-9a-f]+)'",
    line
)

ct1_hex, tag1_hex = m.group(1), m.group(2)
ct1 = bytes.fromhex(ct1_hex)
tag1 = bytes.fromhex(tag1_hex)

log.success(f"pt1 = {pt1}")
log.success(f"ct1 = {ct1.hex()}")
log.success(f"tag1 = {tag1.hex()}")
keystream = xor(ct1, pt1)              # KS[0:len(pt1)]
pt0 = b"Hello GlacierCTF"
ct0 = xor(pt0, keystream[:len(pt0)])
log.success(f"pt0 = {pt0}")
log.success(f"ct0 = {ct0.hex()}")
H_candidates = list(recover_possible_auth_keys(
    ad, ct0, tag_admin,
    ad, ct1, tag1
))

H = H_candidates[0]
log.success(f"H = {H}")
pt2 = b"AAAA" + ADMIN_SECRET + b"BBBB"
ct2 = xor(pt2, keystream[:len(pt2)])   # cùng nonce_admin nên cùng KS


tag2 = forge_tag(H, ad, ct0, tag_admin, ad, ct2)

log.success(f"pt2 = {pt2}")
log.success(f"ct2 = {ct2.hex()}")
log.success(f"tag2 = {tag2.hex()}")


r.recvuntil(b"Choose action:")
r.recvuntil(b"> ")
r.sendline(b"1")

r.recvuntil(b"Ciphertext:")
r.recvuntil(b"> ")
r.sendline(ct2.hex().encode())

r.recvuntil(b"Nonce:")
r.recvuntil(b"> ")
r.sendline(nonce_admin.hex().encode())

r.recvuntil(b"Tag:")
r.recvuntil(b"> ")
r.sendline(tag2.hex().encode())
print(r.recvall().decode("utf-8", "ignore"))
```

Bug: Solve script trên chỉ solve được trên Local vì khi request tới server nó chạy quá lâu nên mình bị timeout trước khi gửi hết toàn bộ request.

Có một cách xử lý đó là thay vì gửi rồi nhận từng request một thì mình có thể gửi 1 lúc 64 request rồi thực hiện phân tích trên từng request rồi rút ra sẽ nhanh hơn là gửi và nhận từng cái 1. 
Solve script (cái này được viết bởi chat GPT):

```python
import os 
import string
import sys
from pwn import * 
from gcm_exploit import * 
import base64
# r = remote("challs.glacierctf.com",13373,timeout=5)
REQUEST_COUNT = 0
r = remote("127.0.0.1",1337)
data = r.recvuntil(b'Choose action:')

print(data)
with open("output.txt","w") as f:
    f.write(str(data))
def get_size(io, payload):
    global REQUEST_COUNT
    try:
        io.sendline(b"0")
        
        io.sendlineafter(b"Plaintext:\n> ", payload.hex().encode())
        
        nonce = os.urandom(16)
        io.sendlineafter(b"Nonce:\n> ", nonce.hex().encode())
        
        REQUEST_COUNT += 1
        
        io.recvuntil(b"Storage left: ")
        line = io.recvline().decode().strip()
        raw_size = int(line.split('/')[0])
        
        compressed_size = raw_size - (REQUEST_COUNT * 16)
        
        io.recvuntil(b"Choose action:\n> ")
        
        return compressed_size
    except Exception as e:
        print(f"Error in get_size: {e}")
        print(f"Request Count: {REQUEST_COUNT}")
        return 999999

def leak_secret(io, prefix):
    known = prefix
    charset = string.ascii_letters + string.digits + "+/="
    
    print(f"[*] Leaking secret for prefix: {prefix}")
    
    global REQUEST_COUNT
    
    while True:
        candidates = {}
        
        print(f"[*] Batching {len(charset)} requests for position {len(known)}")
        
        payloads = []
        for char in charset:
            probe = (known + char).encode()
            payloads.append((char, probe))
            
        for char, probe in payloads:
            io.sendline(b"0")
            io.sendline(probe.hex().encode())
            nonce = os.urandom(16)
            io.sendline(nonce.hex().encode())
        
        for i, (char, probe) in enumerate(payloads):
            try:
                REQUEST_COUNT += 1
                
                io.recvuntil(b"Storage left: ")
                line = io.recvline().decode().strip()
                raw_size = int(line.split('/')[0])
                
                compressed_size = raw_size - (REQUEST_COUNT * 16)
                
                io.recvuntil(b"Choose action:\n> ")
                
                candidates[char] = compressed_size
            except Exception as e:
                print(f"Error in batch receive: {e}")
                print(f"Request Count: {REQUEST_COUNT}")
                return known[len(prefix):]
            
        min_size = min(candidates.values())
        best_chars = [c for c, s in candidates.items() if s == min_size]
        
        if len(best_chars) == 1:
            best_char = best_chars[0]
            known += best_char
            sys.stdout.write(f"\r[+] Found: {known}")
            sys.stdout.flush()
            
            if best_char == "\n" or len(known) > 100: 
                break
            
            if best_char == "=":
                pass

            if len(known) - len(prefix) >= 24:
                 if len(known) - len(prefix) >= 24:
                     break
        else:
            print(f"\n[!] Ambiguity: {best_chars} with size {min_size}")
            break
            
    print(f"\n[+] Leaked: {known}")
    return known[len(prefix):]
nonce_b64 = leak_secret(r, "[+] Nonce: ")
tag_b64 = leak_secret(r, "[+] Tag: ")

nonce_admin = base64.b64decode(nonce_b64)
tag_admin = base64.b64decode(tag_b64)
print(nonce_admin,"\n")
print(tag_admin)
ADMIN_SECRET = b"Glacier CTF Open"
MAX_STORAGE = 1 << 16
ad = b"GlacierCTF2025"
pt1 = b"B" * 64
r.sendline(b"0")
r.recvuntil(b"Plaintext:\n> ")
r.sendline(pt1.hex().encode())
r.recvuntil(b"Nonce:\n> ")
r.sendline(nonce_admin.hex().encode())
line = r.recvline().decode().strip()
print("[server log]:", line)

r.recvuntil(b"[+] Storage left: ")
_ = r.recvline()  

r.recvuntil(b"Choose action:\n> ")


m = re.search(r"ct\.hex\(\)='([0-9a-f]+)'.*tag\.hex\(\)='([0-9a-f]+)'", line)

ct1_hex, tag1_hex = m.group(1), m.group(2)
ct1 = bytes.fromhex(ct1_hex)
tag1 = bytes.fromhex(tag1_hex)


# ct1_hex, tag1_hex = m.group(1), m.group(2)
# ct1 = bytes.fromhex(ct1_hex)
# tag1 = bytes.fromhex(tag1_hex)
# print(ct1)

# log.success(f"pt1 = {pt1}")
# log.success(f"ct1 = {ct1.hex()}")
# log.success(f"tag1 = {tag1.hex()}")
keystream = xor(ct1, pt1)              # KS[0:len(pt1)]
pt0 = b"Hello GlacierCTF"
ct0 = xor(pt0, keystream[:len(pt0)])
# log.success(f"pt0 = {pt0}")
# log.success(f"ct0 = {ct0.hex()}")
H_candidates = list(recover_possible_auth_keys(
    ad, ct0, tag_admin,
    ad, ct1, tag1 ))

H = H_candidates[0]
print(H)
# log.success(f"H = {H}")
pt2 = b"AAAA" + ADMIN_SECRET + b"BBBB"
ct2 = xor(pt2, keystream[:len(pt2)])   # cùng nonce_admin nên cùng KS


tag2 = forge_tag(H, ad, ct0, tag_admin, ad, ct2)
print(tag2)

r.recvuntil(b"Choose action:")
r.recvuntil(b"> ")
r.sendline(b"1")

r.recvuntil(b"Ciphertext:")
r.recvuntil(b"> ")
r.sendline(ct2.hex().encode())

r.recvuntil(b"Nonce:")
r.recvuntil(b"> ")
r.sendline(nonce_admin.hex().encode())

r.recvuntil(b"Tag:")
r.recvuntil(b"> ")
r.sendline(tag2.hex().encode())
print(r.recvline().decode("utf-8", "ignore"))
```