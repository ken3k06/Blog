---
title: Z3 Solver
---

## Giới thiệu 
Z3 Solver là một SMT solver (Satisfiability Modulo Theories solver hay còn được gọi là trình chứng minh định lí) và được phát triển bởi Microsoft Research. 
Nhiệm vụ của Z3 là giải các bài toán logic có ràng buộc theo nhiều lí thuyết khác nhau chẳng hạn như số nguyên, bit-vector, mảng hay logic boolean. 
Mới đầu xài Z3 thì mình thấy nó khả ảo diệu và "magic", ném một đống biểu thức vào z3 và nó tự giải cho mình =)). Sau 1 thời gian dùng thì mình thấy nó vẫn ảo diệu
## Syntax và ví dụ

Mọi người có thể tham khảo syntax và doc của nó tại đây: 
[1] https://github.com/Z3Prover/doc/tree/master/programmingz3/code
[2] https://z3prover.github.io/api/html/z3.z3.html
[3] https://microsoft.github.io/z3guide/docs/logic/basiccommands/
[4] https://theory.stanford.edu/~nikolaj/programmingz3.html


Để sử dụng z3-API của Python mọi người có thể tải trực tiếp bằng 
```
pip install z3-solver
```
## Một số cú pháp

Để tạo một biến symbolic nguyên trong z3 ta dùng cú pháp `x = Int('x')`. Ta sẽ dùng biến `x` này để mô tả các ràng buộc cần chứng minh. Chẳng hạn như sau:
```python
from z3 import *
x = Int('x')
y = Int('y')
solve(x > 2, y < 10 ,x + 2*y ==7)
```
Kết quả trả về sẽ là
```
[y = 0, x = 7]
```


Hàm `solve` giải một hệ các ràng buộc cho trước. Trong python thì `=` để gán giá trị và các toán tử `>, <, >=, <=, ==, != ` cho các phép so sánh. 

Tiếp theo ta có ví dụ sau

```python
from z3 import *
x = Int('x')
y = Int('y')
print(simplify(x+y+2*x+3))
print(simplify(x<y+x+2))
print(simplify(And(x + 1 >= 3, x**2 + x**2 + y**2 + 2 >= 5)))
```

Kết quả đầu ra:

```python
3 + 3*x + y
Not(y <= -2)
And(x >= 2, 2*x**2 + y**2 >= 3)
```
Hàm `simplify` giúp rút gọn các biểu thức logic hoặc đại số về dạng tương đương và đơn giản hơn. 


Trong z3, các biểu thức logic được biểu diễn dưới dạng cây gọi là AST - abstract syntax tree.

Mọi người có thể xem ở đây https://vi.wikipedia.org/wiki/C%C3%A2y_c%C3%BA_ph%C3%A1p_tr%E1%BB%ABu_t%C6%B0%E1%BB%A3ng

Hiểu đơn giản thì một biểu thức được chia thành các node của một cây. Abstract có nghĩa là không quan tâm đến chi tiết cụ thể như dấu ngoặc, dấu cách, hay thứ tự viết code. Thay vào đó, nó biểu diễn cấu trúc logic theo ngữ nghĩa – tức là theo ý nghĩa toán học.

Chẳng hạn 2 biểu thức dưới đây
```python
(x+y)*2>=5
((x+y)*2)>=5
```
là tương đương nhau. 

Để duyệt qua cấu trúc cây này thì z3 có cung cấp các hàm sau:
```python
x = Int('x')
y = Int('y')
n = x + y >= 3
print("num args: ", n.num_args())
print("children: ", n.children())
print("1st child:", n.arg(0))
print("2nd child:", n.arg(1))
print("operator: ", n.decl())
print("op name:  ", n.decl().name())
```
Cái này cũng không có nhiều ý nghĩa giải bài tập lắm nên mình sẽ không đào quá sâu vào. 

Ngoài biến nguyên ta còn có biến thực như sau

```python
x=Real('x')
y=Real('y')
solve(x**2+y**2>3,x**3+y<5)
```
Các thao tác trên biến symbolic thực của z3 cũng không quá hiệu quả, thông thường người ta sẽ sử dụng CAS hoặc sage để làm việc. Lí do là vì z3 không có thuật tính toán số học dấu chấm động chính xác như các phần mềm khác. 

Bù lại z3 thực sự mạnh với các thao tác logic, bit-level

Có thể điều chỉnh độ chính xác khi làm việc với số thực bằng cú pháp `set_option(precision=30)`.
Để tạo một số hữu tỉ trong z3 ta dùng cú pháp `Q(num,den)`, gồm 2 đầu vào lần lượt là tử số và mẫu số.

Lưu ý: Khi khởi tạo `x=Real('x')` thì ta không thể lấy `x+3/2` trực tiếp được, lí do là vì `3/2` là một số dấu chấm động (float number) trong python trong khi `x` là một biến symbolic của z3. Để cộng hoặc tạo biểu thức thì ta cần cộng với `Q(3,2)`. 
Hoặc là `RealVal(3)/RealVal(2)`

Thực ra thì khi chạy thử nó cũng không gặp lỗi nhưng nên chuyển thẳng về như vậy để tính chính xác hơn và tránh lỗi không hợp lệ (maybe).
```python
from z3 import *
x = Real('x')
print(x+3/2)
print(x+Q(3,2))
print(x+RealVal(3)/RealVal(2))
```

## Boolean Logic

Z3 hỗ trợ đầy đủ các toán tử logic như And, Or, Not, Implies và If(if-then-else). Bi-implies được biểu diễn bởi `==` (tương đương).

Tạo biến bool cũng tương tự như trên ta dùng cú pháp `x=Bool('x')`

```python
p = Bool('p')
q = Bool('q')
r = Bool('r')
solve(Implies(p,q), r == Not(q), Or(Not(p),r))
```
Nó sẽ trả về một nghiệm thỏa mãn tất cả các ràng buộc đều đúng. 

Ta có thể thêm True và False để xây dựng các biểu thức boolean

```python
p = Bool('p')
q = Bool('q')
print(And(p, q, True))
print(simplify(And(p, q, True)))
print(simplify(And(p, False)))
```

## Solvers
Thay vì dùng lệnh `solve()` như ở trên thì ta có thể dùng lệnh `Solver()` để khởi tạo một tập các ràng buộc. Chẳng hạn như sau:

```python
from z3 import *
s = Solver()
x = Int('x')
y = Int('y')
s.add(x+y==10)
s.add(x>y)
if s.check() == sat:
    print(s.model())
else:
    print("vô nghiệm")
```
Để kiểm tra hệ ràng buộc có nghiệm hay không thì ta dùng lệnh `s.check()`. Nó sẽ trả về `sat` là có nghiệm hoặc `unsat` là vô nghiệm. 

Cú pháp `s.add()` để thêm ràng buộc. Ví dụ khi giải toán ta muốn giải nhiều bài toán khác nhau nhưng có chung ràng buộc thì ta có thể sử dụng lệnh `s.pop()` và `s.push()`

`s.push()` lưu trạng thái hiện tại của solver vào stack và `s.pop()` quay lại trạng thái trước push gần nhất. 
Ví dụ
```python
from z3 import *
x = Int('x')
s = Solver()
s.add(x>5)
print(s.check())
s.push()
s.add(x<0)
print(s.check())
s.pop()
print(s.model())
'''
sat
unsat
[x = 6]
'''
```
Mỗi nghiệm thỏa mãn các ràng buộc được gọi là model. Mỗi model sẽ có cấu trúc giống như một dict, ánh xạ các biến tới các giá trị thỏa mãn ràng buộc của chúng.

```python
x = Int('x')
y = Int('y')
s = Solver()
s.add(x+y==5)
s.add(x+y>2)
if s.check() == sat:
    m = s.model()
    print(m[x])
    print(m[y])
```
Có thể dùng cú pháp `decls()` để xem biến nào có trong model
```python=
m = s.model()
for d in m.decls():
    print(f"{d.name()} = {m[d]}")
```
Để tạo nhanh các biến cùng kiểu thì ta có thể dùng `x,y = Ints('x y')` (thêm s vào sau)

## List comprehension

Z3 có một số cú pháp list comprehension để khởi tạo nhiều biến thuộc cùng một kiểu dữ liệu. 

Ví dụ trong phiên bản python 3.6 trở về sau thì ta dùng 
```python
s = [Int(f"f_{i}") for i in range(5)]
```
Còn các phiên bản cũ hơn ta có thể sử dụng
```python
X = [ Int('x%s' % i) for i in range(5) ]
Y = [ Int('y%s' % i) for i in range(5) ]
```

Ngoài ra Z3Py còn cho phép ta tạo các vector với các kiểu dữ liệu khác nhau. 
```python
from z3 import *
x = IntVector('x',3)
# [x__0, x__1, x__2]
```
## Function
Trong z3 có hai loại function. Một là các interpreted function `+ - * /`. Hai là các uninterpreted function tức là những function không có nghĩa trước. Những hàm này thì z3 không gán nghĩa cho nó trước mà nó chỉ bị ràng buộc bởi những ràng buộc (constraints) mà ta đưa vào. 
Chẳng hạn mình có một hàm `f(x)=x+1`. Bây giờ trong z3 mình sẽ tạo nó bằng cách dùng cú pháp `Function`. Cụ thể
```python
f = Function('f', IntSort(), IntSort())
```
Đây là một hàm có kí hiệu là `f` và đi từ tập các số nguyên tới tập các số nguyên. 
Ví dụ:
```python
from z3 import *
x = Int('x')
y = Int('y')
f = Function('f', IntSort(), IntSort())
s = Solver()
s.add(f(f(x)) == x, f(x) == y , x!=y)
print(s.check())
m = s.model()
print(m.evaluate(f(x)))
```
## Solving Puzzles
### Dog, Cat and Mouse
Consider the following puzzle. Spend exactly 100 dollars and buy exactly 100 animals. Dogs cost 15 dollars, cats cost 1 dollar, and mice cost 25 cents each. You have to buy at least one of each. How many of each should you buy?

Lưu ý: `x = Int('x')` là một biến nguyên còn `x = IntVal(5)` là khởi tạo `x` như một giá trị cụ thể (hằng số)

Đối với bài này thì có thể làm đơn giản như sau:

```python
from z3 import *

x = Int('x') # chó 
y = Int('y') # mèo
z = Int('z') # gà
s = Solver()
s.add(x>=1 , y>=1, z>=1) # mua ít nhất 1 con mỗi loại
s.add(x*1500+100*y+25*z == 10000) # dollar sang cent
sat = s.check()
if sat:
    m = s.model()
    print(m)
```
### Sudoku
![[Pasted image 20250923090252.png]]
Đầu tiên ta cần tạo một instance để mô tả trạng thái ban đầu của bảng Sudoku.
Instance của ta trong bài này là một ma trận $9 \times 9$ trong đó mỗi ô chỉ bao gồm các chữ số từ $1$ đến $9$. Đây là điều kiện đầu tiên.
Điều kiện tiếp theo là không có 2 số nào bằng nhau nằm trên cùng 1 hàng hoặc 1 cột tức là mọi cặp số lấy trên mỗi hàng hoặc mỗi cột là phân biệt. 
Thêm nữa, mỗi block $3 \times 3$ cũng sẽ có đủ cả 9 số. 

Trong Python ta sẽ dùng list comprehension kèm với f-string như sau:
```python
from z3 import *

X = [[Int(f"x_{i}_{j}") for j in range(9)] for i in range(9)]
s = Solver()

for i in range(9):
    for j in range(9):
        s.add(And(1<=X[i][j], X[i][j] <=9))
puzzle = [[0,0,0,0,9,4,0,3,0],
            [0,0,0,5,1,0,0,0,7],
            [0,8,9,0,0,0,0,4,0],
            [0,0,0,0,0,0,2,0,8],
            [0,6,0,2,0,1,0,5,0],
            [1,0,2,0,0,0,0,0,0],
            [0,7,0,0,0,0,5,2,0],
            [9,0,0,0,6,5,0,0,0],
            [0,4,0,9,7,0,0,0,0]]

print(puzzle)
for i in range(9):
    for j in range(9):
        if puzzle[i][j]!=0:
            s.add(X[i][j] == puzzle[i][j])

for i in range(9):
    s.add(Distinct(X[i]))
for j in range(9):
    s.add(Distinct([X[i][j] for i in range(9)]))
for a in range(3):
    for b in range(3):
        block = [X[3*a+i][3*b+j] for i in range(3) for j in range(3)]
        s.add(Distinct(block))
if s.check() == sat:
    m = s.model()
    r = [[m.evaluate(X[i][j]) for j in range(9)] for i in range(9)]
    for row in r:
        print(row)
else:
    print("unsat")
```


### Custom Crypto
```python
f=open("flag.txt", "r")
flag = f.read()

g = open("key.txt" , "r")
key = g.read()

key = key[0:4]

def enc(text,key):
    encrypted = []
    for i in range(int(round(len(text)/4))):
        shifted = spicy(text[i*4:(i+1)*4],i,key)
        encrypted.append(shifted)
    return encrypted



def spicy(text,offset,key):
    res = []
    for p in range(len(text)):
        res.append(int((ord(text[p])+offset)^ord(key[p])))
    return res

flat_list = []
for sublist in enc(flag,key):
    for item in sublist:
        flat_list.append(item)

f=open("enc.txt","w+")
f.write(str(flat_list))

```
```
[28, 24, 1, 9, 9, 19, 93, 93, 94, 2, 26, 13, 6, 92, 61, 11, 15, 39, 91, 91, 20, 28, 54, 8, 17, 89, 23, 61]
```
Phân tích source:

Flag và key được gọi ra. Key bị truncate chỉ còn lại 4 kí tự đầu. 
Hàm enc hoạt động như sau: Nó chia plaintext thành 4 phần. Đưa vào hàm spicy và ghép vào ct. 

Hàm spicy: Với mỗi kí tự `p` trong plaintext. Nó lấy giá trị ASCII của kí tự đó rồi cộng với offset. Giá trị này lại được xor với kí tự ở vị trí `p` của key. Vậy thì chỉ cần biết được key thì có thể khôi phục lại flag được. 
Hai hàm `rev_spicy` và `decrypt` thì có thể đảo ngược logic nhưng vấn đề là ta không biết key. Mặc dù key chỉ có 4 kí tự nhưng nếu brute toàn bộ thì không thể vì có tới 256 trường hợp cho mỗi kí tự. 

Ta biết prefix của flag là `pwned{` nên tạo hệ các ràng buộc là oke

```python
from z3 import *
def spicy(text,offset,key):
    res = []
    for p in range(len(text)):
        res.append(int((ord(text[p])+offset)^ord(key[p])))
    return res

def rev_spicy(text,offset,key):
    res = []
    for p in range(len(text)):
        val = (text[p]^ord(key[p]))- offset
        res.append(chr(val))
    return ''.join(res)
def enc(text,key):
    encrypted = []
    for i in range(int(round(len(text)/4))):
        shifted = spicy(text[i*4:(i+1)*4],i,key)
        encrypted.append(shifted)
    return encrypted
def decrypt(ct,key):
    # ct = [enc1,enc2,enc3,enc4]
    res = []
    for i in range(len(ct)):
        p = rev_spicy(ct[i],i,key)
        res.append(p)
    return ''.join(res)
ct = [28, 24, 1, 9, 9, 19, 93, 93, 94, 2, 26, 13, 6, 92, 61, 11, 15, 39, 91, 91, 20, 28, 54, 8, 17, 89, 23, 61]
print(ct)
prefix = 'pwned'
# 5 kí tự đầu của flag, 4 kí tự đầu mã hóa với offset là 0 còn kí tự thứ 5 offset là 1

key = [BitVec(f'k{i}',8) for i in range(4)]
s = Solver()

for i in range(4):
    s.add(((ord(prefix[i])+0) ^ key[i]) == ct[i])

s.add(((ord(prefix[4])+1)^key[0]) == ct[4])
for k in key:
    s.add(k >= 32, k <= 126)
# thêm điều kiện kí tự k printable

if s.check() == sat:
    m = s.model()
    key = ''.join([chr(m[k].as_long()) for k in key])
print(key)
ct = [ct[i*4:(i+1)*4] for i in range(len(ct)//4)]
print(decrypt(ct,key))
```