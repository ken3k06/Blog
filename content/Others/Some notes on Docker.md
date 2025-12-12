
## Các khái niệm cơ bản 

### Docker Engine
Docker Engine là phần cốt lõi của Docker, nó hoạt động như một công cụ để đóng gói ứng dụng, được xây dựng theo kiểu kiến trúc Client - Server và được cài đặt trên máy Host. 
Docker Engine có 3 phần :
- Server: Docker Daemon dùng để tạo và quản lí các Images, containers, networks và volumes.
- Rest API: controller cho docker daemon, chỉ ra những gì docker daemon sẽ làm. 
- Client: là một công cụ giúp người dùng giao tiếp với docker host. Người dùng tương tác với docker thông qua command trong terminal CLI. Docker Client sẽ sử dụng API gửi lệnh tới Docker Daemon. 

![[Pasted image 20251125205708.png]]


### Docker image vs Container 

Docker image là một file bất biến - không thay đổi, chứa các source code, lib, dependencies, tools và các files khác cần thiết cho một ứng dụng để chạy.

Docker image đôi khi còn được gọi là snapshots do tính chất read-only của chúng. Docker image được tạo ghi ta gọi `docker build`. Docker sẽ đọc Dockerfile và tạo một image mới. 
Hoặc khi ta gọi `docker pull` từ registry (các kho lưu trữ online chẳng hạn như Docker Hub).

Chúng đại diện cho một application và virtual environment của nó tại một thời điểm cụ thể.
Docker images chỉ là các mẫu, làm cơ sở để xây dựng một container. Một container cuối cùng chỉ là một image đang chạy. Khi ta tạo một container, nó sẽ thêm một lớp có thể ghi lên trên image bất biến, nghĩa là bây giờ ta có thể sửa đổi nó. 

Bởi vì Images là các file bất biến, một khi nó đã được tạo thì ta không thể sửa đổi nó. Ta chỉ có thể tạo một image mới hoặc thêm các thay đổi chồng lên trên nó. 

Image mà ở đó bạn tạo một container tồn tại riêng biệt và không thể thay đổi. Khi bạn chạy một môi trường containerized, về cơ bản, bạn tạo một bản sao đọc-ghi của image bên trong container. Lúc này nó sẽ thêm một Container Layer cho phép sửa đổi toàn bộ bản sao của image.

![[Pasted image 20251125211557.png]]


Về docker container, bản chất là nó một run-time environment mà ở đó người dùng có thể chạy một ứng dụng độc lập. Những container này rất gọn nhẹ và cho phép ta chạy ứng dụng trong đó một cách nhanh chóng và dễ dàng. 

Container là một thể hiện thực thể của một image như ta đã nhắc ở trên. Khác với image thì container là các thực thế có thể tạo, khởi động, dừng và xóa một cách nhanh chóng. 
Các container không giống như máy ảo cần ảo hóa xảy ra ở tầng phần cứng mà chúng ảo hóa ở lớp ứng dụng.
![[Pasted image 20251125213141.png]]

Nó dùng 1 máy chia sẻ kernel và làm giả môi trường để chạy một cách độc lập nên không hề tốn tài nguyên như máy ảo.

Các máy ảo sẽ sử dụng Hypervisor để giả lập phần cứng. Mỗi Hypervisor cho phép mỗi một máy ảo hoặc khách truy cập vào các lớp tài nguyên vật lý bên dưới, bao gồm CPU, bộ nhớ lưu trữ hoặc RAM.

Còn Container chỉ tạo ra:
- namespace (tách process, network, PID…)
- cgroup (giới hạn tài nguyên)
- filesystem riêng (overlayfs)
và tất cả dùng chung kernel của Host 



### Dockerfile 
Xem thêm tại đây: 
https://docs.docker.com/reference/dockerfile/
Dockerfile là một file dạng text không có phần đuôi mở rộng, chứa các đặc tả về một trường thực thi phần mềm, cấu trúc cho Docker Image. Từ những câu lệnh đó, Docker sẽ build ra Docker Image. 
Cú pháp build dockerfile sẽ là 
```
docker build -t <tên image> . 
```
Sau đó ta sẽ tiến hành chạy container từ image vừa build 
```
docker run --rm -it <tên image> 
```

Hoặc thay tên image thành images ID cũng được. 
Xem các images có sẵn trên máy bằng lệnh
```
docker images
```
Để xóa một images thì ta dùng lệnh 
```
docker rmi <Image ID>/<Image name> 
```


## Resources

[Docker - Get Started](https://docs.docker.com/get-started/docker-overview/)
