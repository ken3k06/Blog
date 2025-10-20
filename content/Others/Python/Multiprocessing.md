---
title: Multiprocessing
---
## Giới thiệu

### Process vs Thread
Process là một phiên bản của program. Process sinh ra các thread (sub-processes) để xử lí các tác vụ con. Các thread sống bên trong các process và chia sẻ cùng một không gian bộ nhớ
Còn Thread là một bước điều hành bên trong một process. Luồng hay còn gọi là thread, là một khối các câu lệnh (instructions) độc lập trong tiến trình có thể được lập lịch bởi hệ điều hành. Hay nói một cách đơn giản, thread là các hàm hay thủ tục chạy độc lập đối với chương trình chính. Chú ý thêm là một thread có thể làm bất cứ nhiệm vụ gì một process có thể làm. 
Các Threads thì về mặt bản chất giống như các processes nhỏ sống bên trong một processes và chia sẻ không gian bộ nhớ với nhau. 
Ngược lại việc chia sẻ thông tin giữa các processes chậm hơn chia sẻ giữa các threads vì các processes không chia sẻ không gian bộ nhớ. 

![[Pasted image 20251001101244.png]]



## Note cú pháp
### Process class
Trong Python khi tạo một `Process` từ `multiprocessing`, thì không đồng nghĩa với việc ta sẽ làm việc trực tiếp với tiến trình hệ điều hành (OS process) mà thay vào đó Python sẽ cung cấp cho ta một class `Process` đóng vai trò đại diện cho tiến trình con. 






## Tham khảo:
[1] https://docs.python.org/3/library/multiprocessing.html#multiprocessing.Process
[2] https://docs.python.org/3/library/threading.html#threading.Thread
