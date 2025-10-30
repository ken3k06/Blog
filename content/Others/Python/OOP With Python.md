

![[Pasted image 20251027163404.png]]
## Lý thuyết cơ bản

Trước tiên, lập trình hướng đối tượng là phương pháp lập trình lấy đối tượng làm nền tảng để xây dựng chương trình. Một chương trình hướng đối tượng sẽ bao gồm tập các đối tượng có quan hệ với nhau.
Hai khái niệm cơ bản trong lập trình hướng đối tượng đó là Object (đối tượng) và Class (lớp) 

**Đối tượng.**
- Trong thế giới thực, đối tượng được hiểu như là một thực thể: người, vật 
- Mỗi đối tượng bao gồm 2 thành phần: thuộc tính và thao tác (hành động)
- Ví dụ: đối tượng Chó: 
	- Thuộc tính: giới tính, màu mắt, màu lông, giống, độ cao bằng bộ PC
	- Thao tác: Sủa, cắn, chạy
- Tóm lại: Một đối tượng là 1 thực thể bao gồm thuộc tính và hành động
**Lớp.**
- Các đối tượng có các đặc tính tương tự nhau sẽ được gom chung thành lớp đối tượng 
- Một lớp đối tượng được đặc trưng bằng các thuộc tính(attribute) và các hành động (operations) (hành vi, thao tác) của các đối tượng thuộc lớp 
- Một đối tượng cụ thể thuộc một lớp được gọi là một thể hiện (instance) của lớp đó 

Như vậy, class là một tập hợp các object có đặc điểm chung về properties (các thuộc tính) nhưng các giá trị của chúng thì khác nhau. Ví dụ người A và người B thì có thể có giới tính, cân nặng khác nhau

Methods có thể được coi là các hành vi (behaviors) của object. Method có thể truy cập vào các properties, và các methods khác của class mà nó thuộc về. Methods có thể nhận và trả về giá trị, hoặc chỉ thực hiện các hành động nào đó trên object của class. 

Tiếp theo ta có khái niệm Instance. Instance là một biến, được tạo ra từ một lớp và nó giữ địa chỉ bộ nhớ của object mà class đó tạo ra. 

## Khởi tạo object trong Python 

Trong Python, method `__init__` được dùng để khởi tạo một object của một class. Initializer hay còn gọi là Constructor sẽ được tự động gọi khi một object của class được tạo. Đây là một method đặc biệt giúp ta xác định và gán giá trị cho các variables của instance. Tương tự các method khác thì constructor cũng có thể có các tham số mặc định. Tức là các tham số sẽ có sẵn khi ta gọi một object của class mà không truyền tham số nào vào object. 
```python
class Sophuc:
    def __init__(self, thuc = 0, ao = 1):
        self.thuc = thuc
        self.ao = ao 
    def xuat(self):
        print(f"{self.thuc} + {self.ao}*i")
a = Sophuc()
b = Sophuc(4,3)

a.xuat()
print('\n')
b.xuat()
```

Ngoài ra ta còn có hai khái niệm khác là protected variable và private variable

Tính đóng gói: Đóng gói là việc ta nhóm những gì có liên quan với nhau vào làm một để sau này có thể dùng với một cái tên để gọi đến. 
Đóng gói để che một số thông tin và chi tiết cài đặt nội bộ để bên ngoài không nhìn thấy. Ta cần che giấu 2 thứ
- Che giấu những gì mà mình cần giữ bí mật
- Che giấu những gì mà người dùng không cần 

Trong Python ta cũng có thể giới hạn mức độ truy cập cho các dữ liệu cụ thể bằng cách sử dụng các underscore prefix để chỉ mức độ truy cập. 
Ví dụ:
```python
class MyClass:
    def __init__(self ):
        self.var = 10
        self._protected_var = 11
        self.__private_var = 12

obj = MyClass()
print(obj.var)
print(obj._protected_var)
print(obj.__private_var)
```

![[Pasted image 20251027165002.png]]

Ở đây, ta có thể access protected var ở bên ngoài class (về cơ bản thì Python chỉ quy ước `_protected_var` là phần dữ liệu "chỉ nên" được truy cập từ bên trong class hoặc các subclass). Với `__private_var` thì ta không thể truy cập trực tiếp từ bên ngoài class bằng cách gọi `obj.__private_var`. NHƯNG, ta có thể truy cập giá trị của nó bằng `print(obj._MyClass__private_var)`

![[Pasted image 20251027165248.png]]


Đây là một cơ chế gọi là name mangling trong Python: 
Xem thêm tại : https://realpython.com/ref/glossary/name-mangling/


## Overload toán tử 
Ta có thể thay đổi ý nghĩa của một toán tử trong Python tùy thuộc vào các toán hạng được sử dụng. 
Các toán tử Python hoạt động đối với các lớp dựng sẵn. Nhưng cùng một toán tử hoạt động khác nhau với các kiểu khác nhau. Ví dụ toán tử + sẽ thực hiện phép cộng số học trên hai số, hợp nhất hai danh sách hoặc nối hai chuỗi. Tính năng này trong Python cho phép cùng một toán tử có ý nghĩa khác nhau tùy theo ngữ cảnh được gọi là nạp chồng toán tử. 

Với mỗi lớp (class) mà ta định nghĩ, thì ta cần mô phỏng lại các toán tử khác nhau tùy theo đặc tính của chúng. 
Chẳng hạn ta có ví dụ sau:
```python
class Point:
	def __init__(self, x = 0, y = 0):
		self.x = x 
		self.y = y
p1 = Point(2,4)
p2 = Point(3,5)
print(p1+p2)
```

Thì sẽ gặp ngay lỗi:
```python
unsupported operand type(s) for +: 'Point' and 'Point'

File "/home/duccorp/learnpython/oop/in.py", line 7, in <module> print(p1+p2) ~~^~~ TypeError: unsupported operand type(s) for +: 'Point' and 'Point'
```

Vấn đề ở đây là python không hề được cho biết cách để cộng hai đối tượng thuộc lớp Point. 

Để tạo toán tử cộng cho đối tượng này thì ta có thể sử dụng các special methods. Chi tiết tham khảo tại đây: https://docs.python.org/3/reference/datamodel.html#special-method-names

Special methods là các phương thức đặc biệt, cho phép ta tùy chỉnh hành vi mặc định của các toán tử hay các built-in functions. Một special methods mà ta vẫn hay sử dụng đó là `__init__`. Sau đây ta sẽ đi tìm hiểu các special methods khác và cách sử dụng chúng để overload toán tử. 



## Class variables và instance variables

Trong Python, properties được chia làm 2 loại:
- Class variables 
- Instance Variables


## Python built-in functions

Trình thông dịch của Python có cung cấp sẵn cho ta một số hàm và kiểu dữ liệu đi kèm với hàm đó và có thể được sử dụng trực tiếp ở bất kì đâu trong chương trình mà không cần import thêm thư viện. 
Ở đây mình sẽ nhắc lại một số hàm và chức năng của chúng nhằm mục đích tra cứu
### abs(x)

Trả về giá trị tuyệt đối của đối số `x` được truyền vào. Nếu như đối số `x` là số phức thì sẽ trả về độ lớn của nó
### all(iterable)

Trả về `true` nếu như mọi phần tử trong iterable là true hoặc iterable là rỗng

```python
>>> all([])
True
>>> all([1,2,3])
True
>>> all(i > 0 for i in [1,2,3])
True
>>>
```

### any(iterable)

Trả về `true` nếu như có ít nhất một phần tử trong iterable là `true`. Ngược lại trả về `false` nếu toàn bộ phần tử trong iterable là `false` hoặc iterable là rỗng

```python
>>> any([1,2,3])
True
>>> any([0,0,0,5])
True
>>>
```

Ngoài ra, khi ép các giá trị sau đây sang kiểu Bool trong Python thì giá trị của chúng sẽ là False:
```python
>>> bool(False)
False
>>> bool(None)
False
>>> bool([])
False
>>> bool({})
False
>>> bool(0)
False
>>> bool(0.0)
False
>>> bool(())
False
>>> bool(set())
False
>>> bool([1])
True
>>>
```
### bin(x)

Chuyển một số nguyên thành binary str với prefix là `0b`.
```python
>>> bin(14)
'0b1110'
>>>
```

Đối số `x` truyền vào phải là int object của Python, hoặc nếu không thì đối tượng phải có phương thức `__index__`  đóng vai trò trả về giá trị nguyên. 
Nếu không muốn có prefix `0b` đằng trước thì ta dùng cú pháp `format(14, 'b')`

```python
>>> format(14,'b')
'1110'
>>> format(14,'#b')
'0b1110'
>>>
```

### getattr(object, name , default)

Trả về giá trị của một thuộc tính của đối tượng bằng tên của thuộc tính đó. Chẳng hạn 

```python
class MyClass:
    def __init__(self ):
        self.var = 10
        self._protected_var = 11
        self.__private_var = 12

obj = MyClass()
print(getattr(obj,"var"))
# 10 
```





## Tài liệu tham khảo
1. https://github.com/niloycste/Object-Oriented-Programming-Cheatsheet
2. https://www.pythoncheatsheet.org/cheatsheet/oop-basics
3. https://realpython.com/python3-object-oriented-programming/
4. https://python-textbok.readthedocs.io/en/latest/
5. https://docs.python.org/3/tutorial/classes.html

