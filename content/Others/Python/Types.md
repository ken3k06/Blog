## Tóm tắt
Python là một ngôn ngữ lập trình hướng đối tượng. Vì vậy hầu hết mọi thứ trong Python đều là những đối tượng với những thuộc tính (properties) và phương thức (methods).

Một đối tượng bao gồm hai phần cơ bản:
- Thuộc tính (attributes) chính là những thông tin, đặc điểm của đối tượng. VD: Con mèo , có màu gì? có đuôi , 2 tai và 4 chân
- Phương thức (methods) là những thao tác, hành động mà đối tượng đó có thể thực hiện. VD Con mèo thì có thể ăn, chạy, nhảy, v.v...

Trong Python có nhiều lớp được định nghĩa sẵn. Do mọi thứ trong Python đều là một đối tượng, ví dụ như List, tuple, dictionary, string, int, ... là các lớp. Khi chúng ta khai báo biến thuộc các lớp này thì chúng là các đối tượng.
Kiểm tra lớp của các đối tượng bằng `type()` (lưu ý rằng trong bài này mình đang sử dụng Python 3.12.11)
```python
Python 3.12.11 | packaged by conda-forge | (main, Jun  4 2025, 14:45:31) [GCC 13.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> type(1)
<class 'int'>
>>> type('a')
<class 'str'>
>>> type(b'a')
<class 'bytes'>
>>> type(1.1)
<class 'float'>
>>> type([])
<class 'list'>
>>> type(())
<class 'tuple'>
>>> type({})
<class 'dict'>
>>>
```

Ngoài ra ta còn có khái niệm object trong Python. Trong Python, một object sẽ bao gồm 3 thành phần là `id,type` và `value`. Trong đó `id` có thể coi như là một mã định danh cho object đó, nó sẽ cố định khi ta khởi tạo một object. Ta có thể dùng toán tử `is` để so sánh định danh của 2 objects và gọi hàm `id()` để trả về một số nguyên đại diện cho giá trị định danh của object.

Tiếp theo ta có `type` là thông tin về lớp/kiểu mà object thuộc về. Cuối cùng là `value` là giá trị của object. 
Ví dụ:
```python
>>> x = 42
>>> y = 42
>>> x is y
True
>>> id(x)
98372389653032
>>> id(y)
98372389653032
>>> type(x)
<class 'int'>
>>> type(y)
<class 'int'>
>>> l1 = [1,2,3]
>>> l2 = [1,2,3]
>>> l1 is l2
False
>>>
```

Chi tiết về cái này mình sẽ viết trong một bài khác về classes và object. 

Tham khảo:
[1] https://docs.python.org/3/reference/datamodel.html
[2] https://docs.python.org/3/library/stdtypes.html#
[3] https://phamdinhkhanh.github.io/deepai-book/ch_appendix/appendix_OOP.html

Tiếp theo mình sẽ nói qua về các built-in types trong Python. 

## Sequences Types
Trong Python có 3 kiểu dữ liệu cơ bản dùng để biểu diễn dãy đó là `tuple,list,dict`. Ngoài ra còn có các dãy khác được thiết kế riêng cho các kiểu dữ liệu khác nhau. Chẳng hạn `bytes,bytearray` và `strings`.
### List
Lists là một sequence có thể thay đổi được (mutable), thường được dùng để lưu trữ các items cùng loại. 
Lists có thể được khởi tạo bằng các cách sau:
- `[]` dùng để khởi tạo một list rỗng
- Khởi tạo giá trị thủ công, dùng dấu phẩy để ngăn cách các items riêng biệt `[1,2,3]`
- List comprehension: `[x for x in range(5)]`
- Type constructor: `list(iterable)`, chẳng hạn `list(range(5))`
Constructor sẽ khởi tạo một list mà các items có cùng kiểu dữ liệu và thứ tự với các items của iterable. Ở đây nếu như iterable ban đầu đã là một list thì ta dùng `iterable[:]` để tạo một bản sao của nó.
Ví dụ:
```python
>>> list('abc')
['a', 'b', 'c']
>>> list(123)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'int' object is not iterable
>>>
```
Các operations với lists:

a/ `s[i] = x` : thay thế phần tử thứ `i` của `s` bởi `x`. Lưu ý rằng trong list thì chỉ mục bắt đầu từ `0`. 
b/ `del s[i]` : xóa phần tử thứ `i` của `s`
c/ `s[i:j] = t` : các phần tửvới chỉ mục `i<=k<j` sẽ được thay thế bởi giá trị của iterable `t`. 
d/ `del s[i:j]`: xóa các phần tử với chỉ mục `i<=k<j` tương đương với việc thay `s[i:j] = []`
e/ `s[i:j:k]` : list slices nhưng với bước nhảy là `k`. 
f/ `del s[i:j:k]`: tương tự như trên nhưng có thêm bước nhảy là `k`
g/ `s +=t` : nối vào sau `s`, các items của `t`.
h/ `s *= n` : lặp lại các items trong `s` đủ `n` lần. 

Note:
```python
>>> s = [[]]*3
>>> s[0].append(42)
>>> s
[[42], [42], [42]]
>>>
```
Trong python thì khi gọi `[[]]*3` sẽ không đồng nghĩa với việc ta có 3 bản copy của list rỗng `[]` mà thực chất nó sẽ tạo ra 3 bản tham chiếu độc lập đến cùng một object list. 
Do mỗi object có một id tham chiếu độc lập cho nên để tạo ra một list gồm các copy của list rỗng thì ta sẽ dùng list comprehension thay vì làm như trên. Chẳng hạn
```python
>>> s = [[] for _ in range(3)]
>>> s[0].append(42)
>>> s
[[42], [], []]
>>>
```
Ngoài ra ta còn có method `sort` cho list

Method có cú pháp cơ bản là `list.sort(key = None, reverse = False)`. Mặc định ta chỉ cần gọi `list.sort()`. Sort chấp nhận 2 tham số là `key` và `reverse`, cả hai đều để mặc định là `None` và `False` cho nên mỗi lần gọi ta không cần ghi chú thêm vào. Nhưng để truyền tham số vào thì ta bắt buộc phải gọi rõ các keywords vì `key` và `reverse` là các keyword-only arguments. 
`key` là khóa được dùng để so sánh. Chẳng hạn:
```python
words = ["banana", "apple", "cherry", "fig", "kiwi"]
words.sort(key=len)
print(words)
```
Tức là ta muốn so sánh các xâu dựa vào độ dài của chúng.  
`reverse` để mặc định là `False`tức là dãy được sắp xếp tăng dần. Còn nếu muốn dãy giảm dần ta cần gọi `reverse = True`.
