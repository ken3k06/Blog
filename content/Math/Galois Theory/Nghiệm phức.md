Ta gọi một biểu thức $f$ có dạng

$$ 
c_0X^{n}+c_1X^{n-1}+...+c_n(c_0 \neq 0) 
$$

trong đó $X$ là biến số còn $c_i$ là những hệ số cho trước là một đa thức. Số $n$ được gọi là bậc của đa thức $f$ và được kí hiệu là $\deg(f)$. Hệ số đầu là $c_0$ và hệ số tự do là $c_n$.

Phương trình đại số là một phương trình có dạng $f(X)=0$, trong đó $f$ là một đa thức bậc dương. Khi đó $\deg(f)$ được gọi là bậc của phương trình.

Như ta đã học ở cấp 2 thì không phải phương trình nào cũng có nghiệm thực. Chẳng hạn xét phương trình bậc 2 như sau

$$ 
aX^2+bX+c=0 \ (a \neq 0) 
$$

có nghiệm khi và chỉ khi biệt thức $\Delta=b^{2}-4ac$ không âm. Trường hợp giá trị này âm thì phương trình có nghiệm phức.

Định lí sau đây được gọi là định lí cơ bản của đại số. Nó cho thấy nếu ta mở rộng việc xét nghiệm lên các số phức thì mọi phương trình đại số với hệ số thực đều có nghiệm phức.

**Định lí 1.** Mọi phương trình đại số với hệ số phức đều có nghiệm trong tập số phức.

Chứng minh định lí này nằm ngoại phạm vi của bài viết nên mình xin phép không đề cập tới. Mọi người có thể tự tham khảo thêm các nguồn trên mạng nếu có hứng thú.

Việc xét nghiệm của một phương trình đại số có thể quy về bài toán phân tích đa thức thành các thừa số có dạng $X-a$.

**Bổ đề 2.** Đa thức $f(X)$ có nghiệm là $a$ khi và chỉ khi $f(X)$ có thể viết dưới dạng $f(X)=(X-a)g(X)$ với $g(X)$ là một đa thức.

Như vậy ta lại có được kết quả như dưới đây:

**Định lí 3.** Mọi đa thức $f(X)\neq 0$ với hệ số phức đều có thể viết dưới dạng

$$ 
f(X)=c (X-a_1)^{n_1}...(X-a_r)^{n_r} 
$$

trong đó $c$ là một số phức, $a_1,...,a_r$ là các số phức khác nhau và $n_1,...,n_r$ là các số nguyên dương.

Ta có thể chứng minh kết quả trên bằng quy nạp và bổ đề 2.

**Hệ quả 4.** Mọi phương trình đại số bậc $n \geqslant 0$ với hệ số phức đều có đúng $n$ nghiệm phức, kể cả bội số.

Ví dụ. Xét phương trình dạng $X^n-1=0$. Đặt

$$ 
\epsilon_n:=\cos \frac{2\pi}{n} + \sin \frac{2\pi}{n}i 
$$

Từ công thức de Moivre ta thấy

$$ 
(\epsilon)^t = \cos(2t\pi) + \sin(2t\pi)i = 1 
$$

Vậy với mỗi $t$ như vậy thì ta lại có một nghiệm của phương trình với

$$ 
(\epsilon_n)^t:=\cos \frac{2\pi t}{n} + \sin \frac{2\pi t}{n}i 
$$

Cho nên $1,\epsilon,...,\epsilon^{n-1}$ là $n$ số phức khác nhau và chúng cùng chia vòng tròn đơn vị thành $n$ phần bằng nhau.

![[Pasted image 20251022164549.png]]

Hệ số của một đa thức có mối liên hệ chặt chẽ với nghiệm của đa thức thông qua các công thức sau đây, được gọi là hệ thức Viet.

**Bổ đề 5.** Cho $f=X^n+c_1X^{n-1}+...+c_n$. Các số $a_1,a_2,...,a_n$ (không nhất thiết phải khác nhau) là các nghiệm của $f$ khi và chỉ khi với mọi $t=1,2,...,n$ ta có:

$$ 
\sum_{1 \leq i_1 < ... <i_t \leq n}a_{i_i}...a_{i_t} = (-1)^{t}c_t. 
$$
