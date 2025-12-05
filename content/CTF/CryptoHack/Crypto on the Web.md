
Trong bài viết này mình sẽ sử dụng thư viện sau của Python để test: https://pyjwt.readthedocs.io/en/stable/

## JSON

JSON là viết tắt cho [Javascript Object Notation](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/JSON) là một loại dữ liệu dựa trên chuẩn syntax của Javascript Object. 
Ví dụ:
```json
{"username" : "duccorp",
"school": "uit",
"github": "ken3k06"
...}
```

JSON có thể được lưu vào file, có phần mở rộng là `.json` ,hoặc có thể dùng lưu lưu vào một record trong CSDL, v.v... Nó có định dạng đơn giản, bao gồm 2 phần chính đó là key và value, ngoài ra nó cũng dễ dàng sử dụng và truy vấn hơn XML rất nhiều. Thực tế, dữ liệu JSON hợp lệ có thể ở hai định dạng khác nhau: 
- Đầu tiên là dạng tập hợp các cặp key-value được bao bởi một cặp dấu ngoặc nhọn `{...}`. Như ví dụ ở trên
- Dạng thứ hai là tập hợp danh sách có thứ tự các cặp key-value được phân tách bởi dấu phẩy và được bao bởi một cặp dấu ngoặc vuông `[...]`
Ví dụ:
```json
[
	{
		"username" : "duccorp", 
		"school" : "uit",
		"github" : "ken3k06"
	},
	{
		"username" : "dangminhtu", 
		"school" : "uit",
		"github" : "little"
	},
	{
		"username" : "nguyentrongnhan",
		"school" : "uit", 
		"github" : "nhantablop"
	}
]
```


Ta nên sử dụng JSON trong tình huống nào? 
Trong trường hợp ta muốn lưu trữ dữ liệu đơn thuần, tức là dưới dạng metadata ở phía server. Chuỗi JSON sẽ được lưu vào database và sau đó khi cần thì dữ liệu sẽ được giải mã. Và ngoài ra cũng còn nhiều ứng dụng khác nhưng mình xin dành cho các bài sau để nói sâu hơn về chủ đề này.
Xem thêm tại đây: https://datatracker.ietf.org/doc/html/rfc8259

Trong Python có sẵn module `json` để ta làm việc với kiểu dữ liệu này
Để chuyển các dữ liệu trong Python sang kiểu dữ liệu JSON thì ta dùng `json.dumps` hoặc `json.dump`
```python
>>> import json
>>> data = {"username" : "duccorp", "option" : "get_flag"}
>>> json.dumps(data)
'{"username": "duccorp", "option": "get_flag"}'
>>>
```
Hai methods này khác nhau ở đâu? Đối với `json.dump`
![[Pasted image 20251205195953.png]]
Cú pháp đầy đủ của `json.dump()` trong Python sẽ là như trên. 
`obj` là object cần serialize sang json data còn `fp` là để chỉ một file-like object. Tức là khi ta chọn method `dump` thì nó sẽ ghi dữ liệu json của ta sang một file mới 
```python
>>> import json
>>> data = {"username" : "duccorp", "option" : "get_flag"}
>>> with open("a.json", "w") as f:
...     json.dump(data,f)
...
>>> with open("a.json", "r") as f:
...     d = f.read()
...
>>> print(d)
{"username": "duccorp", "option": "get_flag"}
>>>
```

Còn muốn in trực tiếp ra thì ta sẽ dùng `json.dumps`
```python
>>> json.dumps(data).encode()
b'{"username": "duccorp", "option": "get_flag"}'
>>>
```

Tương tự ta cũng sẽ có `json.load()` và `json.loads()`
```python
>>> d = json.dumps(data).encode()
>>> e = json.loads(d.decode())
>>> type(e)
<class 'dict'>
>>> e
{'username': 'duccorp', 'option': 'get_flag'}
>>> d = json.dumps(data)
>>> type(d)
<class 'str'>
>>>
```
`json.load()` thì sẽ đọc file và parse chuỗi JSON. 
Ta có bảng chuyển đổi kiểu dữ liệu như sau:

![[Pasted image 20251205200849.png]]
```python
>>> a = [{'a':1,'b':2}, {'c':3,'d':4}]
>>> json.dumps(a)
'[{"a": 1, "b": 2}, {"c": 3, "d": 4}]'
>>>
```
## JSON Web Tokens

JSON Web Token (JWT) là một tiêu chuẩn mở ([RFC 7519](https://tools.ietf.org/html/rfc7519)) nhằm xác minh thông tin an toàn giữa các bên Client-Server dưới dạng JSON object.

Xem thêm tại [đây](https://www.jwt.io/introduction#what-is-json-web-token)

Cấu trúc của một JSON Web Tokens sẽ gồm 3 phần như sau: Header,Payload và Signature và được ngăn cách nhau bởi 1 dấu phẩy. 

![[Pasted image 20251205202246.png]]

Ngoài ra ta còn có khái niệm và JOSE. JOSE là viết tắt của Javascript Object Signing and Encryption, đây là một bộ tiêu chuẩn (framework) để kí và mã hóa các đối tượng JSON. Đầy đủ về JOSE có thể đọc thêm ở [đây](https://jose.readthedocs.io/en/latest/#id8) và [đây](https://www.loginradius.com/blog/engineering/guest-post/what-are-jwt-jws-jwe-jwk-jwa), trong đó JSON là một định dạng token dựa trên JOSE để phục vụ xác thực và trao đổi thông tin. 
Token ở đây là một chuỗi dữ liệu mang tính đại diện, chẳng hạn như được dùng để biểu diễn danh tính cho một thực thể nào đó. 
Trong quá trình xác thực thì token là một chuỗi các kí tự cho phép người nhận xác thực danh tính của người gửi.
Mặt khác, JWT còn bao gồm thêm một bộ claim, dùng để truyền thông tin giữa client và server. Các claim này cho biết người phát hành token, thời gian có hiệu lực và các quyền mà token được cấp. 
![[Pasted image 20251205203534.png]]

Ta nên dùng JWT khi nào? 
- Authorization - Ủy quyền: Khi người dùng đã đăng nhập vào, mỗi request sau đó được gửi từ client sẽ bao gồm JWT, cho phép người dùng truy cập vào các routes, services và resources được cấp phép bởi token đó. [SSO - Single Sign On](https://viblo.asia/p/single-sign-on-sso-la-gi-hoat-dong-ra-sao-bWrZn4oQ5xw) là một tính năng sử dụng JWT rộng rãi hiện nay.
- Information Exchange - Trao đổi thông tin: JWT cho phép ta trao đổi thông tin một cách an toàn giữa các bên. Vì JWTs còn có thể được dùng để kí. Chi tiết ta sẽ đào sâu ở phần tiếp theo. 

Bây giờ ta sẽ nói tiếp về cấu trúc của JWT.
Như đã nói ở trên thì JWT gồm 3 thành phần chính là header, payload và signature.
### Header
Header hay còn gọi là JOSE Header, thành phần này có vai trò chứa kiểu token (JWT) và thuật toán của chữ kí chẳng hạn như HMAC SHA256 hoặc RSA
```json 
{
	"alg" : "HS256",
	"typ" : "JWT"
}
```
Sau đó JSON String này sẽ được encode theo kiểu Base64Url.
Ví dụ trong Python ta có thể dùng thư viện `base64`
```python
import json 
import jwt 
import base64
header_obj = {"alg":"HS256", "typ":"JWT"}
header_json = json.dumps(header_obj, separators=(',',':'))  # bo khoang trang 
print(header_json)
b = base64.urlsafe_b64encode(header_json.encode()).rstrip(b"=")
print(b.decode())
# {"alg":"HS256","typ":"JWT"}
# eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
```
### Payload
Phần tiếp theo là Payload, phần này sẽ chứa các claims, được hiển thị dưới dạng một chuỗi JSON và thường chỉ chứa một số lượng trường vừa đủ để giữ cho JWT nhỏ gọn.
Có 3 loại claim chủ yếu là `registered, public` và `private`. 

Ví dụ:
```json 
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```
### Signature
Để tạo chữ kí thì ta sẽ lấy phần header và payload đã được mã hóa, thêm vào đó một secret và sử dụng thuật toán được quy định trong phần header để kí. 
Ví dụ với thuật toán HMAC SHA256 thì signature sẽ được tạo ra như sau:
```
HMACSHA256(
	base64UrlEncode(Header) + '.' + base64UrlEncode(Payload), 
	secret
)
```
Chữ kí này sẽ được dùng để kiểm tra xem message có bị thay đổi trên đường đi hay không và còn dùng để xác thực người gửi JWT. 

Ví dụ:
```python
import json 
import jwt 
import base64

payload = {
  "sub": "1234567890",
  "name": "John Doe",
  "admin": True,
  "iat": 1516239022
}
secret = "a-string-secret-at-least-256-bits-long"
encode = jwt.encode(payload, secret, algorithm = 'HS256')
print(encode)
test = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWUsImlhdCI6MTUxNjIzOTAyMn0.KMUFsIDTnFmyG3nMiGM6H9FNFUROf3wh7SmqJp-QV30"
print(encode==test)
```
Test trên web sau: https://www.jwt.io/
Công thức chuẩn cho HMAC mọi người xem ở [RFC 2104](https://datatracker.ietf.org/doc/html/rfc2104)
![[Pasted image 20251205214908.png]]

