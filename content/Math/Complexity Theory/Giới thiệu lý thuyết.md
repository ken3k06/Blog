---
title: Giới thiệu lý thuyết
---
## Giới thiệu
Lý thuyết tính toán xoay quanh ba lĩnh vực trọng tâm là lý thuyết automata (Automata theory), lý thuyết về khả năng tính toán(Theory of Computation) và lý thuyết về độ phức tạp tính toán (Complexity Theory). 
Ba lĩnh vực nghiên cứu của lí thuyết tính toán tuy có nội duung nghiên cứu riêng rẽ, nhưng chúng có quan hệ mật thiết với nhau. Lí thuyết automata đề cập đến việc xây dựng các mô hình toán học về tính toán. Mục tiêu của lý thuyết về khả năng tính toán là phân chia các bài toán thành các lớp các bài toán giải được và lớp các bài toán không giải được. Trong khi đó, lý thuyết độ phức tạp tính toán phân chia các bài toán giải được thành các lớp khác nhau theo mức độ khó khăn khi giải chúng.

## Các khái niệm cơ bản

**Cận trên tiệm cận.** Ta nói rằng $f(n)$ là **O-lớn** của $g(n)$ và viết $f(n) = O(g(n))$ nếu như tồn tại các số tự nhiên $c$ và $n_0$ sao cho, đối với mọi số tự nhiên $n \geq n_0$, 
$$
f(n) \leq cg(n)
$$
Khi $f(n)=O(g(n))$ thì ta nói rằng $g(n)$ là cận trên của $f(n)$ hay chính xác hơn $g(n)$ là cận trên tiệm cận của $f(n)$. 

**Cận dưới tiệm cận.** Ta nói rằng $g(n)$ là cận dưới tiệm cận của $f(n)$ và ta viết $f(n)=\Omega(g(n))$, khi $f(n)$ là cận trên tiệm cận của $g(n)$. 


## Ngôn ngữ hình thức 

**Bảng chữ.**  Xâu các kí tự, hoặc các đặc tính nói chung, là khối (block) đóng vai trò như một đơn vị kiến thiết cơ bản trong khoa học tính toán. Bảng chữ dùng để xác định các xâu được lựa chọn phù hợp với nhu cầu sử dụng. Bảng chữ dùng để xác định các xâu được lựa chọn phù hợp với nhu cầu sử dụng. Với mục đích khảo sát khái quát , ta có định nghĩa sau đây của bảng chữ cái (alphabet)
**Định nghĩa 1.** Tập $\Sigma$ khác rỗng gồm hữu hạn hay vô hạn các kí hiệu được gọi là bảng chữ cái. Mỗi phần tử $a \in \Sigma$ được gọi là một chữ cái hay một kí hiệu.  


## Tài liệu tham khảo
[1] https://theory.cs.princeton.edu/complexity/book.pdf
[2] https://trandinhvi.wordpress.com/wp-content/uploads/2012/06/otomat-ng-van-dinh.pdf



