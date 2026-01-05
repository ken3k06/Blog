---
title: Multiprocessing
---
## Process vs Thread 
Đầu tiên ta cần học cách phân biệt giữa hai khái niệm process và thread 

Process là quá trình hoạt động của một ứng dụng. Ví dụ khi ta click chuột vào trình duyệt Chrome, một process chạy ứng dụng Chrome sẽ được khởi tạo. 
Khi mở Windows Task Manager, ở mục process ta sẽ thấy được các tiến trình này 
![[Pasted image 20260105095826.png]]

Còn thread là một bước điều hành bên trong một process. Một process dĩ nhiên có thể chứa nhiều thread bên trong nó. Khi chúng ta chạy ứng dụng Chrome, hệ điều hành tạo ra một process và bắt đầu chạy các thread chính của process đó. 

Điểm quan trọng cần ghi nhớ là một thread có thể làm bất cứ nhiệm vụ gì một process có thể làm. Tuy nhiên vì một process có thể chứa nhiều thread, mỗi thread có thể coi như là một process nhỏ. Điểm khác biệt mấu chốt giữa thread và process là công việc mỗi cái thường phải làm. 

Một điểm khác biệt nữa đó là nhiều thread nằm trong cùng một process dùng một không gian bộ nhớ giống nhau, trong khi process thì không. Điều này cho phép các thread đọc và viết cùng một kiểu cấu trúc dữ liệu, giao tiếp dễ dàng giữa các thread với nhau. Giao thức giữa các process hay còn gọi là IPC thì phức tạp hơn. 


 Đối với thread, ta còn có một thuật ngữ đó là multi-thread tức là đa luồng. 
 Chẳng hạn trong process Chrome sẽ gồm 1 thread để render giao diện, 1 thread xử lí network, 1 thread chạy JS , v.v...
 
Để tạo nhiều thread thì dễ dàng hơn so với process vì chúng không cần các địa chỉ nhớ riêng rẽ. Ngoài ra việc chạy đa luồng cần được lập trình một cách chi tiết vì các thread chia sẻ các cấu trúc chung mà chỉ sử dụng được bởi từng thread vào mỗi thời điểm. Khác với thread, các process không dùng chung địa chỉ nhớ.


## Concurrency vs Parallelism 

Bây giờ giả sử máy tính của ta đang làm việc trên một dự án phần mềm. Dự án phần mềm gồm 3 task là Task A, Task B, Task C và máy của ta chỉ có một nhân CPU duy nhất, ta coi CPU này như một lập trình viên của đội Dev đang thực hiện nhiệm vụ. Có 3 hướng tiếp cận để xử lí nhiệm vụ này

Đầu tiên, nếu như máy chỉ có duy nhất 1 nhân CPU thì lúc này, lập trình viên A sẽ phải thực hiện tuần tự (Sequential) các công việc. 
- Giải quyết Task A
- Xong Task A
- Giải quyết Task B 
- Xong Task B 
- Giải quyết Task C


![[Pasted image 20260105101634.png]]

Tuy nhiên, trên thực tế thì máy tính của ta có nhiều CPU hơn thế. Vậy thì ta cần tìm cách để làm việc hiệu quả hơn bằng cách chia ra nhiều người làm mỗi task khác nhau: 
- Lập trình viên A làm task A
- Lập trình viên B làm task B 
- Lập trình viên C làm task C 


![[Pasted image 20260105101801.png]]

Cách tổ chức như trên được gọi là Parallelism

Cuối cùng là Concurrency (Đồng thời). Xử lí đồng thời cũng giống với việc xử lý song song nhằm mục đích để xử lý nhiều tác vụ trong cùng một thời điểm. Tuy nhiên xử lý đồng thời lại có sự khác biệt thông qua cách thức xử lí. Ở đây, ta sẽ chia mỗi task trong 3 task đó thành những sub task nhỏ hơn, mỗi lập trình viên sẽ phải thực hiện một sub task (không nhất định sub task thuộc task nào miễn sao không có 2 người cùng làm một sub task). Bằng cách này ta có thể chia công việc thành nhiều phần nhỏ nhằm tận dụng thời gian chết của mỗi lập trình viên để xử lí subtask. 

![[Pasted image 20260105102035.png]]
## Global Interpreter Lock 

Trong Python có một cơ chế gọi là GIL - Global Interpreter Lock. Vậy thì nó là gì?

Về cơ bản Python Global Interpreter Lock là một cơ chế quản lý luồng (Thread) chỉ cho phép Python sử dụng một luồng duy nhất để thực thi các lệnh lập trình trong một chương trình. Điều này mang ý nghĩa là tại một thời điểm một processs của python chỉ có một luồng duy nhất được thực thi. 


## Multiprocessing module 


## concurrent.futures 

Ta sẽ tìm hiểu về Executor object và Future object trong phần này.

Executor object là một object thuộc về class `concurrent.futures.Executor`. Class này là một ABC , cung cấp cho ta các methods để thực thi bất đồng bộ. 

Tiếp theo, trong Python có một khái niệm gọi là callable object tức là các đối tượng có thể được gọi. Chẳng hạn như một hàm, một method cho class object hoặc các object có method `__call__`

Lúc này `Future` sẽ encapsulates(đóng gói) kết quả và trạng thái của quá trình thực thi bất đồng bộ của một callable và một future instances sẽ được khởi tạo bằng cách gọi `Executor.submit()` hoặc import trực tiếp từ `concurrent.futures`.

Các method của Executor gồm có: 
1. submit 
Như đã nói ở trên thì method `Executor.submit()` sẽ tạo ra một Future object. Cú pháp đầy đủ sẽ là
```python
submit(fn, /.., *args, **kwargs)
```

Ví dụ 
```python
with ThreadPoolExecutor(max_workers = os.cpu_count()) as executor:
    future = executor.submit(pow, 323, 1235)
    print(future.result())
```
2. map
Cú pháp 
```python
map(fn, *iterables, timeout=None, chunksize = 1, buffersize = None)
```
Về cách sử dụng thì tương tự như `map(fn, *iterables)` mặc định của python 
```python
def f(x):
    return x*x 
with ThreadPoolExecutor(max_workers = os.cpu_count()) as executor:
    futures = [executor.submit(f, i) for i in range(10)]
    for future in as_completed(futures):
        print(future.result())
# map binh thuong
for res in map(f, range(10)):
    print(res)
```

3. shutdown 
Cú pháp
```python
shutdown(wait = True, cancel_futures = False)
```
Method này có tác dụng giải phóng bộ nhớ sau khi các futures chạy xong. Method này phải được gọi ở cuối chương trình, nếu như ta gọi `Executor.submit, Executor.map` sau khi gọi `shutdown` thì chương trình sẽ raise lỗi `RuntimeError`.

Nếu `wait = True` thì method này sẽ không trả về kết quả cho tới khi toàn bộ các pending futures chạy xong và các tài nguyên đi cùng với executor được giải phóng hoàn toàn. 
Còn đối với tham số `cancel_futures = False` thì có nghĩa là nó sẽ cancel tất cả các pending futures mà executor chưa khởi chạy. 

### ProcessPoolExecutor

ProcessPoolExecutor là một subclass của Executor sử dụng pool of processes để thực thi các callable một cách bất đồng bộ.


## Tham khảo:
[1] https://docs.python.org/3/library/multiprocessing.html#multiprocessing.Process
[2] https://docs.python.org/3/library/threading.html#threading.Thread
[3] https://docs.python.org/3/library/concurrent.futures.html#concurrent.futures.ProcessPoolExecutor
