

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
### Private attributes 
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

Tóm lại: 
- Đối với Python, tất cả các attributes được mặc định là Public. 
- Trong Python, không có khái niệm private thực sự. Ta chỉ có quy ước để tạo một private attributes đó là sử dụng double leading underscores `__`. 
Còn vì sao python không có thì: 
![[Pasted image 20251126163513.png]]


Đọc thêm tại: https://www.pythonsnacks.com/p/why-python-does-not-have-private-methods


Ngoài private properties thì ta cũng có private method. Để truy cập thì ta cũng sẽ dùng cơ chế name mangling như trên đó là thêm prefix `_<Class_name>`. 
Ví dụ:
```python
class MyClass:
    my_school = "UIT"
    def __init__(self, name = None, age = None):
        self.name = name
        self.__age = age  
    def __getage(self):
        print(self.__age)
a = MyClass(age = 21)
a._MyClass__age = 22 
a._MyClass__getage()

```



Cuối cùng trong phần này là về deconstructor. 
Phương thức hủy hay deconstructor là phương thức sẽ được gọi khi ta hủy một class. Nó luôn được thực thi cuối cùng khi chúng ta khởi tạo một class. Để khai báo một phương thức hủy thì cú pháp sẽ như sau:
```python
def __del__(self):
	# code 
	print("End of life")
```

`__del__` sẽ mặc định được gọi ở cuối sau khi ta thực hiện truy xuất các phương thức trong class xong.


```python
class MyClass:
    my_school = "UIT"
    def __init__(self, name = None, age = None):
        self.name = name
        self.__age = age  
    def __del__(self):
        print("Hủy")

a = MyClass(name = "Minh",age = 21)
print(a.name,"\n")
print(a.my_school,"\n")
print(a._MyClass__age)
```
![[Pasted image 20251126164042.png]]


Để giải phóng các thuộc tính thì ta sử dụng keyword `del`. 
Xem thêm tại: https://stackoverflow.com/questions/6146963/when-is-del-useful-in-python
Ví dụ:
```python
    def __del__(self):
        del self.name
        del self.__age
        print("Hủy")
```

## Overload toán tử 
Ta có thể thay đổi ý nghĩa của một toán tử trong Python tùy thuộc vào các toán hạng được sử dụng. 
Các toán tử Python hoạt động đối với các lớp dựng sẵn. Nhưng cùng một toán tử hoạt động khác nhau với các kiểu khác nhau. Ví dụ toán tử + sẽ thực hiện phép cộng số học trên hai số, hợp nhất hai danh sách hoặc nối hai chuỗi. Tính năng này trong Python cho phép cùng một toán tử có ý nghĩa khác nhau tùy theo ngữ cảnh được gọi là nạp chồng toán tử. 

Với mỗi lớp (class) mà ta định nghĩa, thì ta cần mô phỏng lại các toán tử khác nhau tùy theo đặc tính của chúng. 
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

Special methods là các phương thức đặc biệt, cho phép ta tùy chỉnh hành vi mặc định của các toán tử hay các built-in functions. Một special methods mà ta vẫn hay sử dụng đó là `__init__`. 
Các special methods khác thì mọi người tham ở link doc trên là đầy đủ nhất. 



## Class variables và instance variables

Trong Python, properties được chia làm 2 loại:
- Class variables 
- Instance Variables

### Class variables 
Tất cả các object của class đều được phép truy cập và thay đổi giá trị của class variable. Khi thay đổi giá trị của class variable thì giá trị của property này sẽ thay đổi trong tất cả các object của class. 



Thay đổi class var qua chính class: 
```python
class MyClass:
    school_name = "UIT"
    def __init__(self, name=None):
        if name is not None:
            self.name = name

a = MyClass()
print(a.school_name)
MyClass.school_name = "hcmus"
print(a.school_name)
```


Lưu ý là: Class vars được chia sẻ cho tất cả các object thuộc class và có thể thay đổi nó bằng cách sử dụng bất cứ object nào. Ví dụ thay vì `MyClass.school_name = ...` thì ta có thể gọi luôn `a.school_name = ...`

### Instance variables 
Instance variables là của riêng với mỗi objects. Sự thay đổi ở instance variables của object nào thì chỉ ảnh hưởng đến object đó.

Khác nhau cơ bản của 2 loại biến trên nằm ở cách khai báo chúng. Class vars thì được khai báo ngoài `__init__` còn instance var thì được khai báo bên trong scope của `__init__`
. Chẳng hạn 
```python
class MyClass:
    school_name = "UIT"
    def __init__(self, name):
        self.name = name
```


## Methods 

Ta đã nói về methods ở trên. Bây giờ ta sẽ đào sâu hơn về nó. 
Như ta đã biết thì object sẽ tương tác với properties của nó thông qua method. Có 3 loại method chính trong Python
1. Instance methods
2. Class methods
3. Static methods

### Instance methods
Instance method là một method được định nghĩa bên trong class và luôn nhận tham số đầu tiên là `self`, đại diện cho chính object đang gọi method đó. 
Cụ thể, `self` parameter là một tham chiếu đến object hiện tại của class và được sử dụng để truy cập các variables và methods thuộc về class. 
Một điểm thú vị nữa là nó không phải là một Python Keyword, tức là ta muốn đặt cái gì cũng được. 

### Class methods 

Class methods là methods làm việc với class vars và có thể truy cập bằng cách sử dụng `Class name` thay vì object. Class method có thể được truy cập bằng cách sử dụng tên class mà không cần tạo class object. 

Để khai báo class methods thì ta cần sử dụng decorator `@classmethod`. Method này sẽ nhận tham số đầu tiên là `cls` (class) thay vì `self`. 
Ví dụ:
```python
class MyClass:
    my_school = "UIT"
    def __init__(self, name = None):
        self.name = name
    @classmethod
    def change_name(cls, new_name):
        cls.my_school = new_name 

a = MyClass()
print(a.my_school)
MyClass.change_name("HCMUS")
print(a.my_school)
```


### Static methods 
Static methods là method được dùng chỉ giới hạn ở phạm vi class. Chúng không tương tác với class variables hay instance variables. Chúng được sử dụng như các utility functions bên trong class. Chẳng hạn ta muốn tạo một class AES thì ta có thể thêm method `xor` để thực hiện các phép biến đổi trong scheme, v.v...

Để khai báo statice methods thì ta sử dụng `@staticmethod` decorator. Nó không nhận `cls` hay `self` làm argument. Tóm lại, static method không nhận hay biết bất cứ thứ gì về state của class. 

Statice methods có thể được gọi thông qua class hay object đều được. 
```python
class MyClass:
    my_school = "UIT"
    def __init__(self, name = None):
        self.name = name
    @classmethod
    def change_name(cls, new_name):
        cls.my_school = new_name 
    @staticmethod
    def check():
        print("Ok")

a = MyClass()
print(a.my_school)
MyClass.change_name("HCMUS")
print(a.my_school)
a.check()
MyClass.check()
```


## Information hiding 

Để đảm bảo rằng dữ liệu được truy cập và sử dụng đúng mục đích và an toàn (bảo mật) thì chúng ta sẽ giấu đi các hoạt động bên trong class và chỉ cung cấp một giao diện (interface) mà qua đó thế giới bên ngoài có thể tương tác với class mà không cần biết điều gì đang xảy ra bên trong. 
Information hiding được chia làm 2 thành phần chính đó là encapsulation(tính đóng gói) và abstraction(tính trừu tượng)

### Tính đóng gói
Encapsulation là một kĩ thuật lập trình cơ bản được sử dụng để ẩn dữ liệu trong OOP. Có thể hiểu, tính đóng gói là việc giấu tất cả dữ liệu, methods vào bên trong và chúng ta sẽ thao tác với dữ liệu, methods đó bên trong class. Những thứ bên trong sẽ không thể bị sửa đổi hay truy cập bởi codes bên ngoài từ các nơi khác của chương trình

Có hai câu hỏi cần phải đặt ra đó là: 
- Khi muốn truy xuất dữ liệu private từ các đối tượng thì phải làm thế nào 
- Khi muốn cập nhật dữ liệu private từ các đối tượng thì phải làm thế nào
Đặc điểm quan trọng của phương thức truy vấn là nó không nên thay đổi trạng thái hiện tại của đối tượng. 
Để có thể truy cập vào các private properties từ bên ngoài class, chúng ta sẽ dùng `getter` và `setter`. 
- `getter` là method cho phép đọc giá trị của property 
-  `setter` là method cho phép chỉnh sửa giá trị của property 
Trong python, để thực hiện điều này thì ta sẽ sử dụng `@property` decorator 
Ví dụ:
```python
class MySchool:
    def __init__(self, name, age):
        if not name:
            raise ValueError("Invalid Input")
        self.__name = name 
        self.__age = age 
    def __str__(self):
        return f"{self.__name} is {self.__age} years old"
    @property
    def name(self):
        return self.__name 
    @name.setter
    def name(self, name):
        self.__name = name 

A = MySchool("Duc", "21")
Name = A.name
print(A)
print(Name)
A.name = "Chau"
print(A)
```
![[Pasted image 20251203163851.png]]

Một số lưu ý: Đầu tiên là tên của getter và setter phải trùng với tên của property mà ta muốn truy vấn. 

### Tính kế thừa
Inheritance giúp tăng khả năng tái sử dụng code bằng cách cung cấp cho chúng ta cách để tạo một class mới từ một class hiện có. Class mới (class con/child class) sẽ kế thừa tất cả các non-private attributes từ class hiện có (class cha/parent class).
Ta sử dụng inheritance khi mối quan hệ giữa 2 object là **IS A**. Chẳng hạn **Car IS A Vehicle**. 
Giả sử phần mềm chúng ta được tạo ra để quản lý Vehicle. Chúng ta sẽ tạo ra class Vehicle và nó sẽ là parent class của các child class là Car, Bicycle hay Train. 
Ví dụ:
```python
class Animal:
    def __init__(self,name, legs):
        self.name = name
        self.legs = legs
    def speak(self):
        print(f"Hello, Im a {self.name}")

class Dog(Animal):
    def __init__(self,name, legs):
        super().__init__(name,legs)
    def speak(self):
        print(f"Hello, Im a {self.name}", "gâu gâu")
        
A = Dog("Doggy",legs=4)
A.speak()
```


Tại sao trong Python lại đẻ ra thêm hàm `super()`, trong khi đó có thể khai báo các thuộc tính chung của các đối tượng 1 lần duy nhất trong lớp Animal rồi kể từ đó ta chỉ cần define các class method khác nhau cho từng đối tượng là được. Chẳng hạn như đoạn code trên thì mọi người có thể bỏ luôn dòng `__init__(self,name,legs)` của class Dog thì nó vẫn chạy bình thường. 
Vậy việc sinh ra `super()` có ý nghĩa gì? 

`super()` function được phát huy tác dụng khi chúng ta triển khai inheritance. Nó được sử dụng trong child class để tham chiếu đến attributes của parent class mà không cần đặt tên rõ ràng cho các methods, variables. 
Nó làm cho code dễ quản lý hơn và không cần dùng tên của parent class để truy cập các attributes của parent class. 
Ví dụ đơn giản:
```python
class Gun:
    armor = 30
class AK47(Gun):
    armor = 20
    def display(self):
        print("Default armor for gun class: ", super().armor)
        print("Armor for AK47 type: ", self.armor)
```

![[Pasted image 20251203171001.png]]

### Method Resolution Order (MRO)
MRO có thể hiểu đơn giản là trình tự kế thừa của lớp. MRO của một lớp có thể được truy xuất bằng phương thức `mro()`
MRO sẽ được tạo để đảm bảo các lớp chỉ được liệt kê một lần và các lớp con phải được gọi trước lớp cha.
Thêm dòng `AK47.mro()` vào ví dụ trên: 

![[Pasted image 20251203193937.png]]

Khi sử dụng một phương thức với đối tượng thuộc lớp AK47, chương trình sẽ tìm kiếm phương thức dựa trên thứ tự MRO như trên. Đầu tiên sẽ tìm kiếm phương thức trong class AK47, nếu không có thì sẽ tìm đến Parent là Gun rồi cuối cùng là Object (base class mặc định cho mọi loại dữ liệu Python)
```python
class Gun:
    armor = 30
    def display(self):
        print("Testing")
class AK47(Gun):
    armor = 20
    def display(self):
        print("Base armor is: ", self.armor)
        
B = AK47()
B.display()
print(AK47.mro())
```

![[Pasted image 20251203195109.png]]

Method display của AK47 sẽ được gọi trước.

Tiếp theo là về hàm `super()`
Hàm `super()` sẽ nhận tham số đầu vào là gì?
Nó sẽ nhận hai tham số đầu vào là `type` và `object`, dưới dạng `super(type, object)`. 
- `type` sẽ nhận giá trị kiểu lớp để khi tìm kiếm phương thức hoặc thuộc tính, chương trình sẽ tìm các lớp cha sau `type` trong MRO của lớp. Dựa vào `type` ta có thể quyết định phương thức cần gọi được cài đặt trong lớp cha hoặc lớp cha của cha
- `object` sẽ nhận vào một đối tượng để ràng buộc với phương thức, hoặc thuộc tính được gọi bởi super. 
Tóm lại `super(type, object).method()` có thể hiểu là `object.method()` với `method` được cài đặt trong lớp cha của `type`. Ví dụ ở trên , nếu ta muốn gọi method `display` của lớp cha `Gun` thì ta sẽ gọi
```python
def display(self):
	super(AK47, self).display()
```
Hoặc muốn truyền thêm tham số vào:
```python
class Gun:
	armor = 30
	def display(self, armor):
		print("Testing", armor)
class AK47(Gun):
	armor = 20
	def display(self):
		super(AK47,self).display(50)
        
B = AK47()
B.display()
print(AK47.mro())
```


### Tính đa hình trong Python
Trong lập trình, polymorphism hay còn gọi là đa hình, đề cập đến việc cùng 1 object thể hiện các hành vi khác nhau. 
Ví dụ trong class Geometry ta có thể có các object  Circle hoặc Square, với properties của chúng là khác nhau và ngoài ra cách tính diện tích của 2 hình này cũng khác nhau. 

Bây giờ, ta muốn thiết kế một method để tính diện tích các hình, nếu ta khai báo `get_area_<name>` tương ứng với từng hình thì sẽ khó để nhớ vì mỗi hình là một tên khác nhau. Cách giải quyết đó là define một methods `get_area` trong Parent class mà không implement gì trong đó. Mỗi child class sẽ kế thừa methods ấy và tự implement tương ứng. 
Ví dụ:
```python
import math 
class Shape:
        def __init__(self):
                pass 
        def get_area(self):
                pass 
        def get_circum(self):
                pass
class Square(Shape):
        def __init__(self,side):
                self.side = side 
        def get_area(self):
                return self.side*self.side 
        def get_circum(self):
                return self.side*4
class Circle(Shape):
        pi = math.pi
        def __init__(self, radius):
                self.radius = radius
        def get_area(self):
                return self.radius*self.radius*self.pi
        def get_circum(self):
                d = self.radius*2
                return d*self.pi  
C = Square(5)
area = C.get_area()
print(area)
print(C.get_circum())

D = Circle(4)
print(D.get_area())
```

Ở ví dụ trên, nếu một child class implement lại một method đã được định nghĩa ở parent class thì nó được gọi là method overriding. 
Nói thêm về phần này như sau: Method overriding là hiện tượng nhiều method có cùng tên, tuy nhiên số lượng parameters hoặc type của parameters được nạp vào là khác nhau. Overloading tức là việc làm cho một methods thực hiện các operations khác nhau dựa trên args của nó. 
Ở python thì ta chỉ có thể nạp chồng ngầm (implicitly overloaded) chứ không thể nạp chồng rõ ràng:
Ví dụ:
```python
class Demo:
	def __init__(self,a, b):
		self.a = a 
		self.b = b 
	def display(self, c, d):
		print(self.a)
		print(self.b)
		print(c)
		print(d)
	def display(self, c, d ,e):
		print(self.a)
		print(self.b)
		print(c)
		print(d)
		print(e)
A = Demo(1,2)
A.display(1,2)
```

Khi khai báo như vậy thì sẽ gặp lỗi: 
![[Pasted image 20251203205749.png]]
Python sẽ gọi method cuối cùng mà ta khai báo khi chúng ta gọi. 

Như vậy để thực hiện method overloading trong Python ta phải sử dụng một cách khác. Ở đây ta sẽ thêm vào `@dispatch` decorator.
Đây không phải thư viện có sẵn của Python mà ta cần phải tải về gói Pip của nó `pip install multipledispatch`
```python
from multipledispatch import dispatch
class Demo:
	def __init__(self,a, b):
		self.a = a 
		self.b = b 
	@dispatch(int, int)
	def display(self, c, d):
		print(self.a)
		print(self.b)
		print(c)
		print(d)
	@dispatch(int, int ,int)
	def display(self, c, d ,e):
		print(self.a)
		print(self.b)
		print(c)
		print(d)
		print(e)
A = Demo(1,2)
A.display(3,4)
```

### Tính trừu tượng

Ở phần này ta sẽ nói về tính trừu tượng cũng như một số thứ về ABC, abstract method trong Python. 

Đầu tiên là khái niệm về tính trừu tượng. Tính trừu tượng là một trong những nguyên lí cơ bản của lập trình hướng đối tượng. Nó được sử dụng để ẩn đi các chi tiết triển khai phức tạp và chỉ hiển thị những gì cần thiết cho người dùng. Tính trừu tượng giúp giảm độ phức tạp của hệ thống, tăng tính bảo trì và tái sử dụng mã nguồn.

Ví dụ: Khi chúng ta đi rút tiền ở cây ATM, việc của ta là đưa thẻ vào và nhập mật khẩu, phần còn lại máy ATM hoạt động như thế nào, xác thực ra làm sao ta hoàn toàn không quan tâm miễn là số tiền ta rút ra nhỏ hơn số dư trong tài khoản là được. 

Tiếp theo là khái niệm về interface. Interface được sử dụng để định nghĩa các hành vi của một nhóm đối tượng đó. Ví dụ một con chó thì có behaviors là ngủ, sau này khi ta tạo ra một con chó thì dù nó có là loại chó nào đi chăng nữa cũng sẽ có hành vi là ngủ. 
Một interface sẽ khai báo ra các methods của nó, các methods này không có nội dung cụ thể , nên được gọi là abstract method. Class mà implements interface này phải có tất cả các methods được khai báo trong interface và phải định nghĩa nội dung của methods. Như vậy interface về mặt bản chất là một tiêu chuẩn mà các class implement nó phải tuân thủ. Các class con kế thừa class cha với abstract method thì nó bắt buộc phải override tất cả các abstract method của class cha. 


Trong Python thì không có interface, nên để triển khai tính trừu tượng ta sẽ sử dụng module `abc`. 

**Cú pháp**
Để định nghĩa một lớp trừu tượng trong Python, ta cần kế thừa từ `ABC` (Abstract Base Class) và sử dụng decorator `@abstractmethod` để đánh dấu các phương thức trừu tượng.
```python
class MyAbstractClass(ABC):
    @abstractmethod
    def my_abstract_method(self):
        pass 
```
Ngoài ra, trong một lớp trừu tượng, ta có thể có cả các phương thức trừu tượng và không trừu tượng. Các phương thức không trừu tượng có thể có triển khai cụ thể và có thể được sử dụng bởi các lớp con.

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def sound(self):
        pass

    def sleep(self):
        print("This animal is sleeping.")

class Dog(Animal):
    def sound(self):
        return "Woof"

class Cat(Animal):
    def sound(self):
        return "Meow"
dog = Dog()
cat = Cat()


print(dog.sound())  
print(cat.sound())  
dog.sleep()         
cat.sleep()         
```


Tới đây thì coi như ta nắm được các khái niệm cơ bản về OOP trong Python. 

## Bonus: Python built-in functions

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



## Bài tập vận dụng
### Bài 1
![[Pasted image 20251126164853.png]]

Giải:
```python
class SoPhuc:
    # tạo lập số phức 
    def __init__(self, re = 0, img = 1):
        self.re = re
        self.img = img 
    # xuất bằng print
    def __str__(self):
        if self.img >= 0:
            return f"{self.re} + {self.img}i"
        else:
            return f"{self.re} - {-self.img}i"
    # nhập số 
    def nhap(self):
        self.re = float(input("Nhập phần thực: "))
        self.img = float(input("Nhập phần ảo: "))
    # thay đổi giá trị thực và ảo 
    @property
    def re(self):
        return self._re 
    @re.setter
    def re(self, val):
        self._re = val 
    @property
    def img(self):
        return self._img 
    @img.setter
    def img(self, val):
        self._img = val 
    def __add__(self, other):
        return SoPhuc(self.re + other.re, self.img + other.img)
    def __sub__(self, other):
        return SoPhuc(self.re - other.re, self.img - other.img)
    def __mul__(self,other):
        return SoPhuc(self.re * other.re - self.img * other.img, self.re * other.img + self.img * other.re)
    def __truediv__(self, other):
        return SoPhuc((self.re * other.re + self.img * other.img) / (other.re**2 + other.img**2), (self.img * other.re - self.re * other.img) / (other.re**2 + other.img**2))
    def __eq__(self, other):
        return self.re == other.re and self.img == other.img
    
if __name__ == "__main__":
    a = SoPhuc()
    print("Nhập số phức A:")
    a.nhap()
    b = SoPhuc()
    print("Nhập số phức B:")
    b.nhap()
    print(f"\nA = {a}")
    print(f"B = {b}")
    print(f"\nA + B = {a + b}")
    print(f"A - B = {a - b}")
    print(f"A * B = {a * b}")
    print(f"A / B = {a / b}")
    if a == b:
        print("A va B bang nhau")
    else:
        print("A va B khac nhau")
    # thay đổi giá trị 
    a.re = 10 
    a.img = 7 
    print("New a:" ,a)
```

### Bài 2
```
Xây dựng 2 lớp CCVinHome và CCBcon được kế thừa từ lớp ChungCu. Biết rằng ChungCu bao gồm các thuộc tính như sau:
	Tên chung cư (ten), 
	Số tầng (soTang), 
	Diện tích chung cư (dienTich), 
	Tên người quản lý (tenQL), 
	Tên đại diện sở hữu (soHuu)
	
Lớp CCVinHome thì tên đại diện người sở hữu sẽ là “Vinhomes”. Lớp CCBcon thì tên đại diện người sở hữu sẽ là “Bcons”. Vào cuối tuần tất cả các quản lý tòa nhà đề phải gửi phiếu thông báo về tình trạng tòa nhà cho ban quản lý chung cư khu vực (guiThongBao), tiêu đề của thông báo là: “Tên người quản lý – Tên chung cư – Tên đại diện sở hữu”. Ví dụ: “Nguyễn Văn A – Chung cư UITer – Vinhomes”.

1. Áp dụng kế thừa, đa hình xây dựng chương trình với các lớp phù hợp. Cho phép ban quản lý chung cư khu vực nhập vào số lượng chung cư Vinhomes và Bcons.

2. Ban quản lý chung cư khu vực Làng Đại Học (khu vực chỉ có chung cư Vinhomes và Bcons) vào cuối tuần sẽ nhận được thông báo về tình trạng của các chung cư. Danh sách các tiêu đề mà ban quản lý chung cư cuối tuần nhận được sẽ là?
	Ví dụ: Có 2 chung cư: 1 chung cư Vinhomes và 1 chung cư Bcons.
		“Nguyễn Văn A – Chung cư UITer – Vinhomes
		Nguyễn Văn B – Chung cư USSHer – Bcons”

3. Tất cả các chung cư trong Làng Đại Học đều là chung cư cho thuê (sẽ phải trả tiền phòng mỗi tháng). Mỗi tầng của một chung cư đều có 6 phòng diện tích bằng nhau. Tiền thuê phòng mỗi tháng của các phòng được tính dựa theo diện tích của chung cư và đại diện sở hữu chung cư. Vậy số tiền mỗi tháng ban quản lý chung cư Làng Đại Học thu về sẽ là bao nhiêu? Biết rằng:
	Vinhomes:
		Diện tích > 600 m^2 : 10 – 15 triệu / phòng
		Diện tích <= 600 m^2: 6 – 10 triệu / phòng
	Bcons: 
		Diện tích > 600 m^2 : 8 – 12 triệu / phòng
		Diện tích <= 600 m^2: 5 – 8 triệu / phòng
		
Lưu ý: Tiền thuê phòng của các phòng thuộc một chung cư sẽ là như nhau. 
Ví dụ: Chung cư Vinhomes có 12 tầng, diện tích 700 m^2 thì số tiền thuê phòng của chung cư đó sẽ là hàm tienPhong() được tính theo công thức: random(10 → 15) * 12 *6
```

Phân tích đề: 
Yêu cầu xây dựng 2 lớp CCVinHome và CCBcon kế thừa từ lớp ChungCu -> Cần xác định nó có những properties và methods chung nào. 
Method chung là `guiThongBao` và các properties chung là 
```
Tên chung cư (ten), 
Số tầng (soTang), 
Diện tích chung cư (dienTich), 
Tên người quản lý (tenQL), 
Tên đại diện sở hữu (soHuu)
```

Câu hỏi đầu tiên: 
```
1. Áp dụng kế thừa, đa hình xây dựng chương trình với các lớp phù hợp. Cho phép ban quản lý chung cư khu vực nhập vào số lượng chung cư Vinhomes và Bcons.
```


## Tài liệu tham khảo
1. https://github.com/niloycste/Object-Oriented-Programming-Cheatsheet
2. https://www.pythoncheatsheet.org/cheatsheet/oop-basics
3. https://realpython.com/python3-object-oriented-programming/
4. https://python-textbok.readthedocs.io/en/latest/
5. https://docs.python.org/3/tutorial/classes.html
6. https://viblo.asia/p/ham-super-trong-python-va-mot-so-van-de-lien-quan-Ny0VGAR8JPA

