
Tóm tắt tình huống hiện tại: Chuyện là sắp tới mình có tham gia tổ chức WCO4 bên Inseclab và có thể sẽ cần demo một số chall CTF cho mảng Crypto. Nếu bây giờ muốn demo một bài theo kiểu server, có host, port để mọi người có thể nc vào và tương tác thì phải làm sao? 
## Set-up

### Socket and Python 

Có thể code 1 server đơn giản bằng cách sử dụng module socket của Python như sau:
```python
#!/usr/bin/python3

import socket 
import threading 
from concurrent.futures import ThreadPoolExecutor
from secrets import randbits
from sympy import nextprime
import random
import os 

e = random.randint(500,1000)

def encrypt(inp):
	p = nextprime(randbits(1024))
	q = nextprime(randbits(1024))
	n = p * q
	c = [pow(ord(m), e, n) for m in inp]
	return [n, c]
def handle_client(conn, addr):
    print(f"Connect from {addr}")
    
    conn.settimeout(5)
    try: 
        msg = b'Welcome to the WCO4 RSA Service!\n'
        msg += b'Please choose one of the following options\n'
        msg += b'1: Encrypt a message\n'
        msg += b'2: View the encrypted flag\n'
        msg += b'3: Exit\n> '
        conn.sendall(msg)
        while True:
            try:
                data = conn.recv(1024)
            except socket.timeout:
                try:
                    conn.sendall(b"Too slow")
                except:
                    pass
                break 
            if not data:
                break
            choice = data.strip()
            if choice == b'3':
                break 

            elif choice == b'1':
                conn.sendall(b'Enter a message and the server will encrypt it with a random N!\n> ')
                data = conn.recv(1024)
                if not data:
                    break


                plaintext = data.decode().strip()

                n, c = encrypt(plaintext)


                resp  = "Your randomly chosen N:\n> {}\n".format(n)
                resp += "Your encrypted message:\n> {}\n\n".format(c)
                conn.sendall(resp.encode())


                conn.sendall(b'1: Encrypt a message\n2: View the encrypted flag\n3: Exit\n> ')

            elif choice == b'2':
                data = 'W1{fake_flag}' 
                plaintext = data.strip()
                n, c = encrypt(plaintext)

                resp  = "Your randomly chosen N:\n> {}\n".format(n)
                resp += "Your encrypted flag:\n> {}\n\n".format(c)
                conn.sendall(resp.encode())

                conn.sendall(b'1: Encrypt a message\n2: View the encrypted flag\n3: Exit\n> ')

            else:
                conn.sendall(b'Invalid option. Please choose 1, 2 or 3.\n> ')
                    
    except Exception as e:
        print(f"Error: {e}")
    finally: 
        conn.close()
        print(f"Closed {addr}")

def main():
      server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
      server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
      server.bind(('127.0.0.1',1337))
      server.listen(64)
      print("Server started on port 1337...")
      with ThreadPoolExecutor(max_workers=os.cpu_count()) as executor:
        try:
            while True:
                conn, addr = server.accept()
                print(f"Accepted connection from {addr}")
                executor.submit(handle_client, conn, addr)
        except KeyboardInterrupt:
            print("\nShut down server")
        finally:
            server.close()

if __name__ == "__main__":
    main()
```

Giải thích: Đầu tiên là setup cho socket server side. 
Khi gọi 

```python
socket.socket(socket.AF_INET, socket.SOCK_STREAM)
```
 
 `socket.AF_INET` có nghĩa là ta sẽ mở một socket sử dụng IPv4 còn `socket.SOCK_STREAM` là sử dụng giao thức TCP. `server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)` để cài đặt socket trước khi binding port. Ở đây `socket.SO_REUSEADDR` để có thể sử dụng lại địa chỉ của port nếu ta muốn restart socket server. Ví dụ muốn debug nhanh hay đại loại vậy. 
Phần này thì mình cũng chưa thực sự hiểu rõ lắm. Nên có gì mọi người hãy tham khảo trên doc chính thức của Python.
```
https://docs.python.org/3.12/library/socket.html
```
Sau khi thiết lập xong thì mình sẽ binding tới `127.0.0.1:1337`. Địa chỉ `127.0.0.1` được gọi là loopback IP, `127.0.0.1` là địa chỉ nội bộ của máy tính cho mạng IPv4, là địa chỉ mạng bên trong của chính máy tính. Nếu ta cài đặt một dịch vụ mạng trên máy tính của mình, như hệ thống máy chủ web, thì địa chỉ nội bộ luôn là `127.0.0.1`. 
Ví dụ sau khi đoạn code trên thì sau đó mình có thể connect tới `127.0.0.1:1337` bằng lệnh `nc` để bắt đầu tương tác với chương trình được. Nhưng tất nhiên người dùng bên ngoài sẽ không thể tương tác được với chương trình này. Để làm được thì cần port forwarding , ví dụ như chạy trên VPS hoặc đơn giản hơn là sử dụng Docker. 
### Docker 
Mình có notes một số thứ về docker và cách setup tại [[Some notes on Docker]]
Ngoài ra mọi người có thể xem thêm trên Doc của Docker để biết thêm cách sử dụng. 


Các dịch vụ để tạo tunnel:  

## Ngrok

Có thể tải ngrok thông qua snap. Nếu chưa có snap thì có thể tải như sau: 
```
sudo apt update
sudo apt install snapd
sudo snap install ngrok
```
Sau đó thêm file thực thi của ngrok vào đường dẫn hiện tại. Vì tải bằng snap nên file thực thi của nó sẽ ở `/snap/bin`.
```
echo 'export PATH=$PATH:/snap/bin' >> ~/.zshrc    
source ~/.zshrc
```

Doc đầy đủ về ngrok ở đây: https://ngrok.com/docs/agent
Sau đó xác thực ngrok agent để xài:
```
ngrok config add-authtoken $YOUR_AUTHTOKEN
```

Nhưng mình gặp một vấn đề đó là mình không có thẻ để xác thực. Nếu không xác thực được thì ngrok không cho mình sử dụng dịch vụ TCP endpoints của nó. 

![[Pasted image 20251122115737.png]]

## Playit

Tải nó tại đây: https://playit.gg/support/run-on-linux/
Sau đó mọi người config theo hướng dẫn là được. 

Good luck! 






