## Đại số tuyến tính
Giới thiệu lại một số khái niệm cơ bản
## Không gian Vector

Khái niệm không gian vector là một trong những trụ cột quan trọng của bộ môn đại số tuyến tính. Việc hiểu rõ bản chất của không gian vector giúp ta xây dựng một nền tảng vững chắc phục vụ cho việc tiếp cận các khái niệm cao cấp hơn sau này. Trong bài viết này tác giả sẽ trình bày vắn tắt lại một số kết quả quan trọng liên quan đến không gian vector. 

## Khái niệm 
Ta sẽ quy ước $\displaystyle \text{K}$ là một trường. 
#### Định nghĩa 1. Không gian vector
Tập hợp $\displaystyle V$ được gọi là một không gian vector trên $\displaystyle \text{K}$ nếu nó được trang bị hai phép toán, phép toán đầu tiên là phép cộng hai vector, kí hiệu là $\displaystyle +$, phép toán thứ hai là phép nhân một vector với vô hướng $\displaystyle a$, kí hiệu là $\displaystyle \times$. Cụ thể, như sau 

- Phép cộng hai vector : là một ánh xạ  $\displaystyle +:V\times V\rightarrow V$ , ví dụ $\displaystyle ( \alpha ,\beta )\rightarrow \alpha +\beta$
- Phép nhân hai vector: là một ánh xạ  $\displaystyle \times :\text{K} \times V\rightarrow V$ , ví dụ : $\displaystyle ( a,\alpha )\rightarrow a\alpha$ với $\displaystyle a\in \text{K} ,\alpha \in V$

Ngoài ra $\displaystyle V$ cũng thỏa mãn tính chất là một nhóm Abel đối với phép cộng và các mệnh đề về phân phối, giao hoán tương tự như khi làm việc trên tập số thực. Ở đây ta gọi các phần tử của $\displaystyle V$ là các vector còn các phần tử của $\displaystyle \text{K}$ là các vô hướng. 

## Độc lập tuyến tính và phụ thuộc tuyến tính

#### Định nghĩa 2. Tổ hợp tuyến tính, biểu thị tuyến tính

- Một tổ hợp tuyến tính của các vector $\displaystyle \alpha _{1} ,\alpha _{2} ,...,\alpha _{n} \in V$ là một biểu thức có dạng 
$$
\begin{equation*}
\sum _{i=1}^{n} a_{i} \alpha _{i} =a_{1} \alpha _{1} +...+a_{n} \alpha _{n}
\end{equation*}
$$
trong đó $\displaystyle a_{i} \in \text{K}$ là các vô hướng.

- Giả sử $\displaystyle \alpha =a_{1} \alpha _{1} +...+a_{n} \alpha _{n}$ thì ta nói rằng vector $\displaystyle \alpha$ biểu thị tuyến tính được qua hệ các vector $\displaystyle \alpha _{1} ,...,\alpha _{n}$. 


Ngoài ra một vector có thể có nhiều biểu thị tuyến tính khác nhau qua các hệ vector phân biệt. Biểu thị tuyến tính cũng có tính chất bắc cầu, tức là với hệ vector $\displaystyle ( \alpha _{1} ,...,\alpha _{n})$, ta nói hệ biểu diễn được qua hệ vector $\displaystyle ( \beta _{1} ,...,\beta _{m})$ nếu như mỗi vector trong hệ $\displaystyle ( \alpha _{1} ,...,\alpha _{n})$ đều biểu thị tuyến tính được qua hệ $\displaystyle ( \beta _{1} ,...,\beta _{m})$, và tương tự nếu hệ $\displaystyle ( \beta _{1} ,...,\beta _{m})$ biểu thị tuyến tính được qua hệ $\displaystyle ( \gamma _{1} ,...,\gamma _{k})$ thì khi đó hệ $\displaystyle ( \alpha _{1} ,...,\alpha _{n})$ biểu thị tuyến tính được qua hệ $\displaystyle ( \gamma _{1} ,...,\gamma _{k})$.

#### Định nghĩa 3. Độc lập tuyến tính và phụ thuộc tuyến tính. 

Hệ $\displaystyle ( \alpha _{1} ,...,\alpha _{n})$ được gọi là độc lập tuyến tính nếu hệ thức 
$$
\begin{equation*}
a_{1} \alpha _{1} +...+a_{n} \alpha _{n} =0
\end{equation*}
$$
xảy ra khi và chỉ khi $\displaystyle a_{1} =...=a_{n} =0$

Ngược lại hệ $\displaystyle ( \alpha _{1} ,...,\alpha _{n})$ được gọi là phụ thuộc tuyến tính nếu hệ thức trên xảy ra và có ít nhất một giá trị $\displaystyle a_{i} \neq 0$

## Cơ sở và số chiều của không gian vector 
#### Định nghĩa 4. Hệ sinh và cơ sở

a/ Một hệ vector của $\displaystyle V$ được gọi là một hệ sinh của $\displaystyle V$ nếu mọi vector của $\displaystyle V$ đều biểu thị tuyến tính được qua hệ đó. 

b/ Một hệ vector của $\displaystyle V$ được gọi là một cơ sở của $\displaystyle V$ nếu mọi vector của $\displaystyle V$ đều được biểu thị tuyến tính một cách duy nhất qua hệ đó. 


Từ đây ta có các khẳng định sau về hệ sinh và cơ sở là tương đương nhau 

i/ $\displaystyle ( \alpha _{1} ,...,\alpha _{n})$ là một cơ sở của $\displaystyle V$
ii/ $\displaystyle ( \alpha _{1} ,...,\alpha _{n})$ là một hệ sinh độc lập tuyến tính của $\displaystyle V$
iii/ $\displaystyle ( \alpha _{1} ,...,\alpha _{n})$ là một hệ vector độc lập tuyến tính cực đại của $\displaystyle V$.

Chứng minh đơn giản như sau:

Từ i/ suy ra ii/ : $\displaystyle ( \alpha _{1} ,...,\alpha _{n})$ là một cơ sở của $\displaystyle V$. Với ràng buộc tuyến tính $\displaystyle 0=0\alpha _{1} +...+0\alpha _{n}$ thì vì $\displaystyle ( \alpha _{1} ,...,\alpha _{n})$ là một cơ sở của $\displaystyle V$ nên biểu diễn trên là duy nhất kéo theo $\displaystyle ( \alpha _{1} ,...,\alpha _{n})$ là một hệ sinh độc lập tuyến tính của $\displaystyle V$

Từ ii/ suy ra iii/ : $\displaystyle ( \alpha _{1} ,...,\alpha _{n})$ là một hệ sinh độc lập tuyến tính đồng nghĩa với việc mọi vector trong $\displaystyle V$ đều được biểu thị tuyến tính qua hệ và nó cũng là một hệ vector độc lập tuyến tính cực đại vì với $\displaystyle \beta \in V$ bất kì thì $\displaystyle \beta$ biểu thị tuyến tính được qua $\displaystyle ( \alpha _{1} ,...,\alpha _{n})$ cho nên $\displaystyle ( \alpha _{1} ,...,\alpha _{n} ,\beta )$ không còn độc lập tuyến tính

Từ iii/ qua i/ : Một hệ vector độc lập tuyến tính cực đại trong $\displaystyle V$ thì với mọi vector $\displaystyle \beta$ khác thuộc $\displaystyle V$ đều phải được biểu thị tuyến tính qua hệ này, có nghĩa là hệ này sinh ra $\displaystyle V$ và biểu diễn này là duy nhất. Vì giả sử rằng có hai biểu diễn là khác nhau tức là có ít nhất hai hệ số khác nhau giữa hai biểu diễn. Nếu lấy hiệu thì hệ không còn độc lập tuyến tính sinh ra mâu thuẫn. 
#### Định nghĩa 5. Hữu hạn sinh
- Một không gian vector được gọi là hữu hạn sinh nếu như nó có một hệ sinh gồm hữu hạn phần tử. 
#### Định nghĩa 6. Chiều của không gian 
- Số phần tử của mỗi cơ sở của $\displaystyle K$-không gian vector hữu hạn sinh $\displaystyle V\neq \{0\}$ được gọi là số chiều của $\displaystyle V$ trên trường $\displaystyle K$. Kí hiệu là $\displaystyle \dim V$. Quy ước $\displaystyle \dim V=0$ khi $\displaystyle V=\{0\}$.

**Định lí.** Giả sử $\displaystyle V\neq \{0\}$ là một không gian vector hữu hạn sinh. Khi đó, $\displaystyle V$ có một cơ sở gồm hữu hạn phần tử. Hơn nữa, mọi cơ sở của $\displaystyle V$ đều có số phần tử bằng nhau. 

*Chứng minh.*

Trước hết ta có một bổ đề sau: Trong không gian vector $\displaystyle V$, giả sử hệ vector $\displaystyle ( \alpha _{1} ,...,\alpha _{r})$ độc lập tuyến tính và biểu thị tuyến tính được qua hệ $\displaystyle ( \beta _{1} ,...,\beta _{s})$ thì ta có $\displaystyle r\leqslant s$.

Ta chứng minh bổ đề trên như sau: Theo giả thiết ta có một biểu thị tuyến tính như sau 
$$
\begin{equation*}
\alpha _{1} =a_{1} \beta _{1} +...+\beta _{s}
\end{equation*}
$$

Vì hệ $\displaystyle ( \alpha _{1} ,...,\alpha _{n})$ độc lập tuyến tính cho nên ta có thể giả sử $\displaystyle \alpha _{1} \neq 0$ và giả sử không mất tính tổng quát rằng $\displaystyle a_{1} \neq 0$. Khi đó $\displaystyle \beta _{1}$ có một biểu thị tuyến tính như sau:
$$
\begin{equation*}
\alpha _{1} a_{1}^{-1} -\sum _{j=2}^{s} \beta _{j}\left( a_{j} a_{1}^{-1}\right) =\beta _{1}
\end{equation*}
$$

Như vậy $\displaystyle \beta _{1}$ biểu thị tuyến tính được qua hệ $\displaystyle ( \alpha _{1} ,\beta _{2} ,...,\beta _{s})$,và khi đó $\displaystyle ( \alpha _{1} ,...,\alpha _{r})$ biểu thị tuyến tính qua $\displaystyle ( \beta _{1} ,...,\beta _{s})$ còn $\displaystyle ( \beta _{1} ,...,\beta _{s})$ lại biểu thị tuyến tính được qua $\displaystyle ( \alpha _{1} ,...,\beta _{s})$ cho nên $\displaystyle ( \alpha _{1} ,...,\alpha _{r})$ biểu thị tuyến tính được qua $\displaystyle ( \alpha _{1} ,...,\beta _{s})$. Lí do có biểu diễn trên là vì: ta đã có $\displaystyle \beta _{1}$ biểu thị tuyến tính được qua $\displaystyle ( \alpha _{1} ,...,\beta _{s})$. Tương tự với $\displaystyle \beta _{2}$ cũng biểu thị tuyến tính được qua $\displaystyle ( \alpha _{1} ,\beta _{2} ,...,\beta _{s})$ bằng cách lấy mọi vô hướng của các số $\displaystyle \alpha _{1} ,\beta _{i} ,i\neq 2$ đều bằng không thì ta có được một biểu thị tuyến tính. 

Bây giờ tiếp tục ta sẽ chứng minh được rằng $\displaystyle ( \alpha _{1} ,...,\alpha _{r})$ biểu thị tuyến tính được qua $\displaystyle ( \alpha _{1} ,..,\alpha _{i} ,\beta _{i+1} ,...,\beta _{s})$ trong đó $\displaystyle i\leqslant \min\{r,s\}$. Ta sẽ quy nạp. Đầu tiên với $\displaystyle i=1$ thì mệnh đề đúng theo điều vừa chỉ ra ở trên. Giả sử nó đúng tới $\displaystyle i$ và ta sẽ chứng minh $\displaystyle i+1$ cũng đúng trong trường hợp $\displaystyle i+1\leqslant \min\{r,s\}$. 

Ta có $\displaystyle ( \alpha _{1} ,...,\alpha _{r})$ biểu thị tuyến tính được qua $\displaystyle ( \alpha _{1} ,...,\alpha _{i} ,\beta _{i+1} ,...,\beta _{s})$. Như vậy $\displaystyle \alpha _{i+1}$ biểu thị tuyến tính được qua $\displaystyle ( \alpha _{1} ,...,\alpha _{i} ,\beta _{i+1} ,...,\beta _{s})$ cho nên ta có 
$$
\begin{equation*}
\alpha _{i+1} =\sum _{j=1}^{i} \gamma _{j}^{( i+1)} \alpha _{j} +\sum _{j=i+1}^{s} \lambda _{j}^{( i+1)} \beta _{j}
\end{equation*}
$$
Ta có hệ $\displaystyle ( \alpha _{1} ,...,\alpha _{r})$ là một hệ độc lập tuyến tính cho nên khi đó có ít nhất một giá trị $\displaystyle \lambda _{j}^{i+1} \neq 0$ vì nếu không thì $\displaystyle \alpha _{i+1}$ biểu thị tuyến tính qua $\displaystyle ( \alpha _{1} ,...,\alpha _{i} ,...,\alpha _{r})$ là mẫu thuẫn vì $\displaystyle ( \alpha _{1} ,...,\alpha _{r})$ là một hệ độc lập tuyến tính. Tương tự như trên ta cũng suy ra $\displaystyle \beta _{i+1}$ biểu thị tuyến tính được qua hệ $\displaystyle ( \alpha _{1} ,...,\alpha _{i} ,\alpha _{i+1} ,\beta _{i+2} ,...,\beta _{s})$. Cho nên $\displaystyle (\alpha _{1} ,..,\alpha _{i} ,\beta _{i+1} ,...,\beta _{s})$ biểu thị tuyến tính qua hệ $\displaystyle ( \alpha _{1} ,...,\alpha _{i} ,\alpha _{i+1} ,\beta _{i+2} ,...,\beta _{s})$. Suy ra ta có điều phải chứng minh. Bây giờ nếu $\displaystyle r >s$ thì ta suy ra $\displaystyle i=s$. Khi đó $\displaystyle ( \alpha _{1} ,...,\alpha _{r})$ biểu thị tuyến tính qua hệ $\displaystyle ( \alpha _{1} ,...,\alpha _{s})$ là mâu thuẫn với giả sử hệ độc lập tuyến tính. Vậy $\displaystyle r\geqslant s$.

Bây giờ ta sẽ quay trở lại chứng minh định lí ban đầu.

Giả sử $\displaystyle ( \gamma _{1} ,...,\gamma _{s})$ là một hệ sinh hữu hạn của $\displaystyle V$. Ta gọi $\displaystyle ( \alpha _{1} ,...,\alpha _{r})$ là một hệ độc lập tuyến tính trong $\displaystyle V$. Hệ này biểu thị tuyến tính được qua $\displaystyle ( \gamma _{1} ,...,\gamma _{s})$ theo định nghĩa của hệ sinh. Suy ra theo bổ đề thì $\displaystyle r\leqslant s$. Ta tiếp tục bổ sung vào trong hệ $\displaystyle ( \alpha _{1} ,...,\alpha _{r})$ các vector để sao cho hệ vẫn là hệ độc lập tuyến tính và rõ ràng, quá trình này phải dừng lại sau hữu hạn bước và hệ thu được là hệ vector độc lập tuyến tính cực đại trong $\displaystyle V$. Vì là hệ vector độc lập tuyến tính cực đại nên mỗi vector trong $\displaystyle V$ được biểu thị duy nhất qua hệ này. Suy ra ta có điều phải chứng minh. 

Cuối cùng là một định lí, có thể coi như là hệ quả của kết quả trên. 

**Định lí.** Giả sử $\displaystyle V$ là một không gian vector hữu hạn sinh. Khi đó mọi hệ sinh của $\displaystyle V$ đều chứa một cơ sở. Mọi hệ độc lập tuyến tính trong $\displaystyle V$ đều có thể được bổ sung để trở thành một cơ sở của $\displaystyle V$. Nếu $\displaystyle \dim V=n$, thì mọi hệ độc lập tuyến tính gồm $\displaystyle n$ vector của $\displaystyle V$ đều là một cơ sở.

Ngoài ra người ta cũng nhận xét được rằng, trong một không gian vector vô hạn sinh (tức là không hữu hạn sinh), hai cơ sở bất kì đều có cùng lực lượng. Nhưng một hệ vector độc lập tuyến tính có cùng lực lượng với cơ sở thì không nhất thiết là một cơ sở. 


#### Định nghĩa 7. Tọa độ
Bộ vô hướng $\displaystyle ( a_{1} ,...,a_{n})$ xác định bởi điều kiện $\displaystyle \alpha =\sum _{i=1}^{n} a_{i} \alpha _{i}$ được gọi là tọa độ của vector $\displaystyle \alpha$ trong cơ sở $\displaystyle ( \alpha _{1} ,\alpha _{2} ,...,\alpha _{n})$. Vô hướng $\displaystyle a_{i}$ được gọi là tọa độ thứ $\displaystyle i$ của $\displaystyle \alpha$ trong cơ sở đó. 

Bây giờ ta cùng xem xét tọa độ của một vector trong những cơ sở khác nhau thì có liên quan với nhau như thế nào. Xét hai cơ sở $\displaystyle ( \beta _{1} ,...,\beta _{n})$ và $\displaystyle ( \alpha _{1} ,...,\alpha _{n})$ của không gian vector $\displaystyle V$. Như vậy mỗi vector $\displaystyle \beta _{i}$ biểu thị tuyến tính được qua $\displaystyle ( \alpha _{1} ,...,\alpha _{n})$ tức là có các số $\displaystyle \gamma _{i}^{( j)}$ sao cho 
$$
\begin{equation*}
\beta _{j} =\sum _{i=1}^{n} \gamma _{i}^{( j)} \alpha _{i}
\end{equation*}
$$
Giả sử $\displaystyle \alpha$ có tọa độ lần lượt là $\displaystyle ( a_{1} ,...,a_{n})$ và $\displaystyle ( b_{1} ,...,b_{n})$ trong hai cơ sở $\displaystyle ( \alpha _{1} ,...,\alpha _{n})$ và $\displaystyle ( \beta _{1} ,...,\beta _{n})$. Thì khi đó 
$$
\begin{equation*}
\alpha =\sum _{j=1}^{n} b_{j} \beta _{j} =\sum _{j=1}^{n} b_{j}\sum _{i=1}^{n} \gamma _{i}^{( j)} \alpha _{i} =\sum _{j=1}^{n}\left(\sum _{i=1}^{n} b_{j} \gamma _{i}^{( j)}\right) \alpha _{i} =\sum _{j=1}^{n} a_{j} \alpha _{j}
\end{equation*}
$$
Và do mỗi biểu thị tuyến tính của $\displaystyle \alpha$ trong $\displaystyle ( \alpha _{1} ,...,\alpha _{n})$ là duy nhất cho nên ta có 
$$
\begin{equation*}
a_{j} =\sum _{i=1}^{n} b_{j} \gamma _{i}^{( j)} ,j=1,2,...,n
\end{equation*}
$$

## Không gian con - Hạng của một hệ vector

#### Định nghĩa 8. Không gian con

Tập con không rỗng $\displaystyle W\subset V$ được gọi là một không gian vector con của $\displaystyle V$ nếu như $\displaystyle W$ cũng đóng kín đối với hai phép toán trên $\displaystyle V$, tức là 
$$
\begin{gather*}
\alpha +\beta \in W,\forall \alpha ,\beta \in W\\
a\alpha \in W,\forall a\in \text{K} ,\alpha \in W
\end{gather*}
$$
**Mệnh đề 1.** Nếu $\displaystyle W$ là một không gian vector con của $\displaystyle V$ thì ta cũng có $\displaystyle \dim W\leqslant \dim V$.

Kết quả trên là hệ quả trực tiếp của khái niệm về số chiều của một không gian vector. Cụ thể với mỗi hệ độc lập tuyến tính trong $\displaystyle W$ thì cũng độc lập tuyến tính trong $\displaystyle V$. Ngoài ra mỗi phần tử của hệ độc lập tuyến tính đều được biểu thị tuyến tính thông qua cơ sở của $\displaystyle V$ cho nên ta có $\displaystyle \dim W\leqslant \dim V$. Dấu bằng xảy ra khi và chỉ khi $\displaystyle \dim W=\dim V=n$ hay $\displaystyle W=V$, tức là khi đó mọi cơ sở của $\displaystyle W$ cũng là cơ sở của $\displaystyle V$

**Mệnh đề 2.** Giao của một họ bất kì các không gian vector con của $\displaystyle V$ cũng là một không gian vector con của $\displaystyle V$. 

Thật vậy, xét một họ các không gian vector con của $\displaystyle V$ là $\displaystyle \{V_{i}\}_{i\in I}$ thì khi đó $\displaystyle \cap _{i\in I} V_{i}$ cũng thỏa mãn tính đóng đối với phép cộng và nhân. 

#### Định nghĩa 9. Không gian vector sinh bởi $X$
Giả sử $\displaystyle X$ là một tập con của không gian vector $\displaystyle V$. Giao của tất cả các không gian vector con của $\displaystyle V$ mà chứa $\displaystyle X$ được gọi là không gian vector con của $\displaystyle V$ sinh bởi $\displaystyle X$ và được kí hiệu là $\displaystyle \mathcal{L}( X)$. 

Từ định nghĩa, ta suy ra được rằng $\displaystyle \mathcal{L}( X)$ là không gian vector con nhỏ nhất của $\displaystyle V$ mà chứa $\displaystyle X$


Khi đó $\displaystyle \mathcal{L}( X)$ là tập hợp các tổ hợp tuyến tính của các phần tử của $\displaystyle X$. Nói riêng nếu $\displaystyle X=\{\gamma _{1} ,...,\gamma _{k}\}$ thì 
$$
\begin{equation*}
\mathcal{L}( X) =\left\{\sum _{i=1}^{k} a_{i} \gamma _{i} |a_{i} \in \text{K}\right\}
\end{equation*}
$$
Thật vậy, tập hợp các tổ hợp tuyến tính của $\displaystyle X$ chính là một không gian con của $\displaystyle V$ mà chứa $\displaystyle X$. Mặt khác, mọi tổ hợp tuyến tính của $\displaystyle X$ đều nằm trong mọi không gian vector con của $\displaystyle V$ mà chứa $\displaystyle X$. Vì với mỗi không gian vector con $\displaystyle W\subset V$ mà $\displaystyle W$ chứa $\displaystyle X$ thì khi đó các phần tử của $\displaystyle X$ cũng thỏa mãn tính đóng đối với phép cộng và nhân vô hướng trên $\displaystyle W$. Điều này dẫn tới mọi tổ hợp tuyến tính của $\displaystyle X$ cũng nằm trong $\displaystyle W$. 

Tiếp theo ta xét về số chiều của $\displaystyle \mathcal{L}( X)$. 

**Nhận xét:** Số chiều của không gian $\displaystyle \mathcal{L}( X)$ được gọi là hạng của tập hoặc hệ vector $\displaystyle X$ và được kí hiệu là $\displaystyle \text{rank}( X)$. Tương tự ta gọi một tập con các vector của $\displaystyle X$ là tuyến tính cực đại nếu như ta thêm bất kì vector nào trong $\displaystyle X$ vào tập đó thì tập sẽ trở thành tập con phụ thuộc tuyến tính. Như vậy, để tính hạng của $\displaystyle \mathcal{L}( X)$ ta sẽ đếm số vector của mỗi tập con độc lập tuyến tính cực đại trong $\displaystyle X$
.


**Hệ quả:** Hai tập con độc lập tuyến tính cực đại trong $\displaystyle \mathcal{L}( X)$ thì có số phần tử bằng nhau. 


## Tổng và tổng trực tiếp

Ta giả sử $\displaystyle W_{1} ,...,W_{n}$ là các không gian vector con của $\displaystyle V$. Khi đó tập hợp 
$$
\begin{equation*}
W_{1} +...+W_{n} =\{\alpha _{1} +...+\alpha _{n} |\alpha _{i} \in W_{i} ,i=1,..,n\}
\end{equation*}
$$
hiển nhiên lập nên một không gian vector con của $\displaystyle V$.

#### Định nghĩa 10. Tổng của các không gian vector
Không gian vector $\displaystyle \sum _{i=1}^{n} W_{i}$ được gọi là tổng của các không gian vector con $\displaystyle W_{1} ,...,W_{n}$. 

Khi đó mỗi vector $\displaystyle \alpha$ thuộc không gian vector trên có thể được viết dưới dạng 
$$
\alpha =\alpha _{1} +...+\alpha _{n} ,\alpha _{i} \in W_{i}
$$

Tuy vậy, cách viết trên không phải là duy nhất. Vì thế ta đi đến một khái niệm chặt hơn như sau.

#### Định nghĩa 11. Tổng trực tiếp
Nếu mọi vector trong không gian $\displaystyle \sum _{i=1}^{n} W_{i}$ đều được viết duy nhất dưới dạng $\displaystyle \alpha =\alpha _{1} +...+\alpha _{n}$ thì khi đó ta gọi $\displaystyle \sum _{i=1}^{n} W_{i}$ là tổng trực tiếp của các không gian vector $\displaystyle W_{i}$ và kí hiệu là $\displaystyle W_{1} \oplus ...\oplus W_{n}$. Từ định nghĩa trên ta đi đến các tính chất nhằm giúp ta xác định khi nào tổng trên thỏa mãn là một tổng trực tiếp của các không gian vector con.

**Định lí.** $\displaystyle \sum _{i=1}^{n} W_{i}$ là tổng trực tiếp khi và chỉ khi điều kiện sau đây được thỏa mãn:

$$
\displaystyle W_{i} \cap \left(\sum _{j\neq i} W_{j}\right) =\{0\} ,i=1,2,...,n
$$


Ta có định lí sau đây khi nói về số chiều của tổng các không gian vector: 

**Định lí.**  Giả sử $\displaystyle U$ và $\displaystyle W$ là một không gian vector con của một không gian vector $\displaystyle V$ hữu hạn chiều. 
Khi đó ta có 
$$
\begin{equation*}
\dim U+\dim W=\dim( U+W) +\dim( U\cap W)
\end{equation*}
$$
*Chứng minh.*
Giả sử $\displaystyle \{\alpha _{1} ,...,\alpha _{r}\}$ là một cơ sở cho $\displaystyle U\cap W$. Nếu $\displaystyle U\cap W=\{0\}$ thì ta coi như $\displaystyle r=0$. Ta bổ sung hệ này để có một cơ sở $\displaystyle \{\alpha _{1} ,...,\alpha _{r} ,\beta _{1} ,...,\beta _{s}\}$ của $\displaystyle U$ và một cơ sở $\displaystyle \{\alpha _{1} ,...,\alpha _{r} ,\gamma _{1} ,...,\gamma _{t}\}$ của $\displaystyle W$. Ta sẽ chứng minh rằng $\displaystyle \{\alpha _{1} ,...,\alpha _{r} ,\beta _{1} ,...,\beta _{s} ,\gamma _{1} ,...,\gamma _{t}\}$ là một cơ sở của $\displaystyle U+W$. Rõ ràng $\displaystyle \{\alpha _{1} ,...,\alpha _{r} ,\beta _{1} ,...,\beta _{s} ,\gamma _{1} ,...,\gamma _{t}\}$ là một hệ sinh của $\displaystyle U+W$. 
Với mỗi $\displaystyle \alpha \in U+W$ được viết dưới dạng 
$$
\begin{equation*}
\alpha =\text{u} +\text{w} ,\text{u} \in U,\text{w} \in W
\end{equation*}
$$
Bây giờ, để chứng minh tính độc lập tuyến tính, ta giả sử có một ràng buộc tuyến tính 
$$
\begin{equation*}
a_{1} \alpha _{1} +...+a_{r} \alpha _{r} +b_{1} \beta _{1} +...+b_{s} \beta _{s} +c_{1} \gamma _{1} +...c_{t} \gamma _{t} =0
\end{equation*}
$$
với $\displaystyle a_{i} ,b_{j} ,c_{k} \in \text{K}$. Ta cần chứng minh $\displaystyle a_{i} =b_{i} =c_{i} =0,\forall i$. Xét đẳng thức sau đây:

$$
\begin{equation*}
a_{1} \alpha _{1} +...+a_{r} \alpha _{r} +b_{1} \beta _{1} +...+b_{s} \beta _{s} =-( c_{1} \gamma _{1} +...c_{t} \gamma _{t})
\end{equation*}
$$

Vector bên trái thuộc vào $\displaystyle U$ và vector bên phải thuộc vào $\displaystyle W$ vì nó là vector sinh bởi cơ sở của $\displaystyle W$. Như vậy vector trên thuộc vào $\displaystyle U\cap W$. Do đó nó cũng có một biểu diễn tuyến tính qua $\displaystyle (\alpha _{1} ,...,\alpha _{r})$ như sau 
$$
\begin{gather*}
d_{1} \alpha _{1} +...+d_{r} \alpha _{r} =-( c_{1} \gamma _{1} +...c_{t} \gamma _{t})\\
\leftrightarrow c_{1} \gamma _{1} +...c_{t} \gamma _{t} +d_{1} \alpha _{1} +...+d_{r} \alpha _{r} =0
\end{gather*}
$$

Nhưng do hệ $\displaystyle ( \alpha _{1} ,...\alpha _{r} ,\gamma _{1} ,...,\gamma _{t})$ độc lập tuyến tính cho nên $\displaystyle d_{1} =...=d_{r} =c_{1} =...=c_{t} =0$. Như vậy thay ngược lại ở trên ta có 
$$
\begin{equation*}
a_{1} \alpha _{1} +...+a_{r} \alpha _{r} +b_{1} \beta _{1} +...+b_{s} \beta _{s} =0
\end{equation*}
$$

Và một lần nữa do $\displaystyle ( \alpha _{1} ,...,\alpha _{r} ,\beta _{1} ,...,\beta _{s})$ là một hệ độc lập tuyến tính cho nên $\displaystyle a_{1} =...=a_{r} =b_{1} =...=b_{s} =0$. Vậy ta có điều phải chứng minh. Từ những nhận xét trên ta suy ra $\displaystyle \{\alpha _{1} ,...,\alpha _{r} ,\beta _{1} ,...,\beta _{s} ,\gamma _{1} ,...,\gamma _{t}\}$ là cơ sở của $\displaystyle U+W$.


Từ định nghĩa về tổng trực tiếp ta cũng suy ra ngay 
$$
\begin{equation*}
\dim( U\oplus W) =\dim( U) +\dim( W)
\end{equation*}
$$

#### Định nghĩa 12. Phần bù tuyến tính

Nếu $\displaystyle V=U\oplus W$ thì $\displaystyle W$ được gọi là một phần bù tuyến tính của $\displaystyle U$ trong $\displaystyle V$ và $\displaystyle \dim W=\dim V-\dim U$ được gọi là đối chiều của $\displaystyle U$ trong $\displaystyle V$. Giả sử $\displaystyle V=U\oplus W$. Khi đó mỗi vector trong $\displaystyle v$ có thể được biểu diễn duy nhất dưới $\displaystyle v=u+w$.


Định nghĩa một ánh xạ 
$$
\begin{gather*}
pr_{U} :V\rightarrow U\\
pr_{U}( v) =u
\end{gather*}
$$
Nó được gọi là phép chiếu từ $\displaystyle V$ lên $\displaystyle U$ theo phương $\displaystyle W$. Phép chiếu có các tính chất sau: 

$$
\begin{gather*}
pr_{U}( v+v') =pr_{U}( v) +pr_{U}( v') ,\forall v,v'\in V\\
pr_{U}( av) =apr_{U}( v) ,\forall v\in V
\end{gather*}
$$
## Không gian thương - Quotient Spaces

Đầu tiên ta có định nghĩa về quan hệ tương đương. 

Định nghĩa. Một quan hệ tương đương trên một tập hợp $\displaystyle A$ là một mối quan liên hệ $\displaystyle x\sim y$ giữa các phần tử $\displaystyle x,y$ của $\displaystyle A$ thỏa mãn đồng thời các điều kiện sau: 

- Tính phản xạ : $\displaystyle x\sim x$ với mọi $\displaystyle x\in A$
- Tính đối xứng: Nếu $\displaystyle x\sim y$ thì $\displaystyle y\sim x$
- Tính bắc cầu: Nếu $\displaystyle x\sim y$ và $\displaystyle y\sim z$ thì $\displaystyle x\sim z$


## Lattice

## Qui ước
Các kí hiệu: Các vector với các phần tử trong $\displaystyle \mathbb{R}$ được xem như là vector cột và được biểu thị bằng các chữ in thường đậm, ví dụ $\displaystyle \mathbf{x} ,\mathbf{y} ,\mathbf{z}$. Các ma trận được biểu thị bằng các chữ cái in hoa đậm, ví dụ $\displaystyle \mathbf{A} ,\mathbf{S} ,\mathbf{B} ,...$
Chuyển vị của một vector hoặc ma trận được biểu thị bằng $\displaystyle \mathbf{v}^{T}$ hoặc $\displaystyle \mathbf{V}^{T}$ tương ứng. Ngoài ra, chúng ta biểu thị tích trong của hai vector cột $\displaystyle \mathbf{v} ,\mathbf{w} \in \mathbb{R}^{n}$ theo $\displaystyle \langle \mathbf{v} ,\mathbf{w} \rangle =\mathbf{v}^{T}\mathbf{w}$. 
Một số kí hiệu khác: 

- $\displaystyle \mathbb{R}^{n\times m}$: không gian của ma trận $\displaystyle n\times m$ với các mục số thực
- $\displaystyle \| \cdotp \| ,\ \| \cdotp \| _{\infty }$: Chuẩn Euclid và chuẩn tối đa
- $\displaystyle \mathcal{L}$: Một lưới
- $\displaystyle \mathcal{L}(\mathbf{B})$: lưới với các cột của ma trận $\displaystyle \mathbf{B}$ làm cơ sở. 
- $\displaystyle \lambda _{i}(\mathcal{L})$: Số nhỏ nhất sao cho có $\displaystyle i$ vector độc lập tuyến tính trong $\displaystyle \mathcal{L}$ mà mỗi vector đó có chuẩn không vượt quá $\displaystyle \lambda _{i}$.
- $\displaystyle \gamma$ : Hệ số xấp xỉ (gần đúng) trong các bài toán lưới
- $\displaystyle \mathbf{b}_{i}$: một vector cơ sở lưới
- $\displaystyle \mathbf{b}_{i}^{*}$: một vector trong cơ sở trực giao Gram-Schmidt của một lưới. 

## Mở đầu
## Nhắc lại một số định nghĩa

Một lattice ${\displaystyle \mathcal{L} \subset \mathbb{R}^{m}}$ là một không gian vector được sinh bởi các tổ hợp tuyến tính nguyên của các vector độc lập tuyến tính. Tức là 
$$
\begin{equation*}
\mathcal{L} =\left\{\sum _{i=1}^{n} x_{i}\mathbf{b}_{i} \ \middle| x_{i} \in \mathbb{Z}\right\}
\end{equation*}
$$
trong đó $\displaystyle \{\mathbf{b}_{i}\}_{i=1}^{n} \subset \mathbb{R}^{m}$. Đặt $\displaystyle \mathbf{B} \in \mathbb{R}^{m\times n}$ thì $\displaystyle \mathcal{L} =\mathbf{B}\mathbb{Z}^{n}$, đồng nghĩa với việc $\displaystyle \mathcal{L}$ là ảnh của $\displaystyle \mathbb{Z}^{n}$ dưới ánh xạ tuyến tính $\displaystyle \mathbf{B} :\mathbb{R}^{n}\rightarrow \mathbb{R}^{m}$.

Ta có thể định nghĩa lưới theo một cách khác. Cho $\displaystyle m,n,k\in \mathbb{Z}_{ >0}$ với $\displaystyle m\geqslant k$. Một lưới $\displaystyle m$ chiều $\displaystyle \mathcal{L}$ là một nhóm con cộng rời rạc của $\displaystyle \mathbb{R}^{m}$ chứa tất cả các tổ hợp tuyến tính nguyên của $\displaystyle k$ vector độc lập tuyến tính $\displaystyle \{\mathbf{b}_{1} ,\mathbf{b}_{2} ,...,\mathbf{b}_{k}\}$. Đó là $\displaystyle \mathcal{L} =\left\{\mathbf{Bx} \ |\ \mathbf{x} \in \mathbb{Z}^{k}\right\}$ với ma trận $\displaystyle \mathbf{B} =(\mathbf{b}_{1} ,...,\mathbf{b}_{k}) \in \mathbb{R}^{m\times k}$. Ta gọi $\displaystyle \mathbf{B}$ là cơ sở của $\displaystyle \mathcal{L}$ và $\displaystyle k$ là rank của lưới. Sau này ta chỉ quan tâm tới các full rank lattice tức là các lattice có hạng bằng với số chiều. 

![image](https://hackmd.io/_uploads/Syl5BRPBxe.png)


Định thức của một lưới $\displaystyle \mathcal{L}$ với cơ sở $\displaystyle \mathbf{B}$ được xác định bởi $\displaystyle \det(\mathcal{L}) =\sqrt{| \det\left(\mathbf{B}^{T}\mathbf{B}\right)| }$. Nếu lattice $\displaystyle \mathcal{L}$ là full rank thì $\displaystyle \det(\mathcal{L}) =| \det(\mathbf{B})|$. 

Lưu ý rằng cơ sở của một lưới không là duy nhất, hay nói đúng hơn với mỗi ma trận đơn nhất $\displaystyle \mathbf{U} \in \mathbb{Z}^{n\times n}$ thì $\displaystyle \mathbf{BU}$ cũng là cơ sở cho cùng một lưới. Vì ta có tính chất sau: Với hai cơ sở $\displaystyle \mathbf{B}$ và $\displaystyle \mathbf{B} '$ cho lưới $\displaystyle \mathcal{L}$ thì $\displaystyle \mathcal{L}(\mathbf{B}) =\mathcal{L}(\mathbf{B} ')$ cho nên suy ra $\displaystyle \det(\mathbf{B}) =\det(\mathbf{B} ')$. 

Một ma trận đơn nhất $\displaystyle \mathbf{U}$ là một ma trận thỏa mãn $\displaystyle \det(\mathbf{U}) =1$. Như vậy nếu ta lấy $\displaystyle \mathbf{B} '=\mathbf{BU}$ thì sẽ thỏa mãn định thức hai ma trận trên là như nhau.

Tính chất trên tuy đơn giản nhưng rất quan trọng đối với việc triển khai các hệ mật, vì một số cơ sở dễ xử lí hơn những cơ sở khác. 

Mỗi lưới $\displaystyle \mathcal{L}$ có một lưới đối ngẫu (dual lattice), kí hiệu $\displaystyle \mathcal{L}^{*} =\left\{\mathbf{w} \in \mathbb{R}^{m} \ \middle| \ \langle \mathbf{w} ,\mathbf{x} \rangle \in \mathbb{Z} ,\ \forall \mathbf{x} \in \mathcal{L}\right\}$.

## Các bài toán khó

**Bài toán tìm vector ngắn nhất - SVP** : Cho một cơ sở tùy ý $\displaystyle \mathbf{B}$ của một lưới $\displaystyle \mathcal{L}$ có số chiều $\displaystyle m$, hãy tìm một $\displaystyle x\in \mathcal{L}$ khác không với $\displaystyle \| x\| \leqslant \gamma ( m) \lambda _{1}(\mathcal{L})$

Trong đó $\displaystyle \lambda _{1}(\mathcal{L})$ là độ dài cực tiểu thứ nhất của lưới $\displaystyle \mathcal{L}$ (first successive minimum). Mà theo định lí thứ nhất của Minkowski thì với một full rank lattice $\displaystyle \mathcal{L}$ với rank là $\displaystyle n$ thì 
$$
\begin{equation*}
\lambda _{1}(\mathcal{L}) \leqslant \sqrt{n} \mid \det(\mathcal{L}) \mid ^{1/n}
\end{equation*}
$$
Hiểu một cách trực quan: $\displaystyle \lambda _{i}(\mathcal{L})$ là bán kính của một quả cầu có tâm tại gốc tọa độ sao cho trong quả cầu đó tồn tại $\displaystyle i$ vector độc lập tuyến tính. 

Biến thể của bài SVP là bài uSVP là tìm vector ngắn nhất và duy nhất.


![image](https://hackmd.io/_uploads/SJ0DtCDBxg.png)

**Bài toán vector gần nhất - CVP**: Cho một cơ sở tùy ý $\displaystyle \mathbf{B}$ của một lưới $\displaystyle \mathcal{L} =\mathcal{L}(\mathbf{B})$ và một vector đích $\displaystyle \mathbf{t}$ (không nhất thiết thuộc vào $\displaystyle \mathcal{L}$). Tìm một vector $\displaystyle \mathbf{v}$ thuộc lưới sao cho $\displaystyle \| \mathbf{v} -\mathbf{t} \| =\min_{\mathbf{w} \in \mathcal{L}} \| \mathbf{w} -\mathbf{t} \|$. 

![image](https://hackmd.io/_uploads/r1QQ9RDHgl.png)


## Các thuật toán rút gọn lưới


Các thuật toán rút gọn lưới nhằm mục đích lấy một cơ sở đưa ra của một lưới và biến đổi nó thành một cơ sở khác cho cùng lưới nhưng với các vector ngắn hơn và trực giao hơn. Bằng cách này, một vector lưới ngắn có thể được khôi phục. Các thuật toán thường không được thiết kế để tìm chính xác, mà là để trích xuất một vector ngắn trong một số yếu tố gần đúng, nói cách khác là để giải một số bài toán lưới khó gần đúng. 


## Thuật toán Gram-Schmidt

Hai vector $\displaystyle \mathbf{u} ,\mathbf{v}$ được gọi là trực giao nếu như tích trong của chúng bằng 0 tức là $\displaystyle \langle \mathbf{u} ,\mathbf{v} \rangle =0$. Một hệ các vector $\displaystyle \mathbf{S} =(\mathbf{v}_{1} ,...,\mathbf{v}_{n})$ được gọi là một hệ trực giao nếu như chúng đôi một trực giao. Tương tự, một hệ trực giao các vector đơn vị được gọi là một hệ trực chuẩn. 

Ta có thể chứng minh rằng mọi hệ trực chuẩn đều độc lập tuyến tính. 

**Định lí:** Cho $\displaystyle \mathbf{S} =(\mathbf{v}_{1} ,...,\mathbf{v}_{n})$ là một hệ các vector độc lập tuyến tính của không gian Euclid $\displaystyle V$. Khi đó ta có thể tìm được một hệ trực chuẩn $\displaystyle \mathbf{S} '=(\mathbf{u}_{1} ,...,\mathbf{u}_{n})$ sao cho 
$$
\begin{equation*}
span\{\mathbf{v}_{1} ,..,\mathbf{v}_{k}\} =span\{\mathbf{u}_{1} ,...,\mathbf{u}_{k}\} ,\forall k=1,...,n
\end{equation*}
$$
Để xây dựng một hệ trực chuẩn thì trước hết ta sẽ xây dựng một hệ trực giao rồi lấy từng vector chia cho chuẩn của chính nó. 

![image](https://hackmd.io/_uploads/HyBAd-OBgl.png)


```python
from sage.all import *

def gram_schmidt(vectors):
    orthogonal_vectors = []
    for v in vectors:
        for u in orthogonal_vectors:
            v -= (v * u) / (u * u) * u
        orthogonal_vectors.append(v)
    return orthogonal_vectors
v1 = vector([4, 1, 3, -1])
v2 = vector([2, 1, -3, 4])
v3 = vector([1, 0, -2, 7])
v4 = vector([6, 2, 9, -5])

v = [v1,v2,v3,v4]
output = gram_schmidt(v)
print(output)
```

## Thuật toán LLL

Thuật toán rút gọn lưới đầu tiên là LLL. Mục tiêu của thuật toán LLL là tìm ra một cơ sở $\displaystyle \mathbf{b}_{i}$ của lưới sao cho các vector Gram-Schmidt $\displaystyle \mathbf{b}_{i}^{*}$ không quá giảm về kích thước. Cụ thể, với $\displaystyle \delta \in ( 1/4,1)$ ta gọi một cơ sở $\displaystyle \mathbf{B} =\{\mathbf{b}_{1} ,...,\mathbf{b}_{n}\}$ là một cơ sở rút gọn $\displaystyle \delta -LLL$ nếu như

1. $\displaystyle  | \mu _{i,j} | \leqslant \frac{1}{2}$ với mọi $\displaystyle 1\leqslant j< i$.
2. $\displaystyle \left( \delta -\mu _{i+1,i}^{2}\right) \| \mathbf{b}_{i}^{*} \| ^{2} \leqslant \| \mathbf{b}_{i+1}^{*} \| ^{2} ,\forall 1\leqslant i\leqslant n-1$.

![image](https://hackmd.io/_uploads/BJDypWuHle.png)

Mọi người có thể xem implement của key-moon tại đây https://github.com/key-moon/pylll/blob/main/pylll/lll.py

**Cài đặt flatter** Tham khảo tại link sau https://github.com/keeganryan/flatter. 

Để cài thì đầu tiên cần clone repo về terminal của mình 
`git clone https://github.com/keeganryan/flatter`.

Tool được build bằng cmake nên cần cài thêm như sau

![image](https://hackmd.io/_uploads/Hykz4G_rxl.png)

```bash
sudo apt update
sudo apt install build-essential cmake
```

Tiếp theo tạo một thư mục build và chạy cmake

```bash
mkdir build
cd build
cmake ..
```
Mình gặp một cái lỗi như này 
![image](https://hackmd.io/_uploads/B1uSNfuBxe.png)

Lỗi này là do ta chưa cài Eigen, một dependency cần có để build `flatter`.

Tải nốt bằng lệnh sau:
```bash
sudo apt install libeigen3-dev
```

Rồi sau đó chạy lại toàn bộ quá trình một lần nữa

```bash
cd ~/flatter/build
cmake ..
make -j$(nproc)
```
Mọi người thấy thông báo như này hiện ra thì coi như oke

```bash
-- Found FPLLL: /usr/include (found suitable version "5.4.1", minimum required is "5.1.0")
-- Configuring done
-- Generating done
-- Build files have been written to: /home/duc112006/flatter/build
```
Cuối cùng là sao chép file thực thi vào `/usr/local/bin` để chạy trong VSCode
```bash
duc112006@LAPTOP-VB45ARKK:~/flatter/build$ sudo cp bin/flatter /usr/local/bin/flatter
duc112006@LAPTOP-VB45ARKK:~/flatter/build$ which flatter
/usr/local/bin/flatter
duc112006@LAPTOP-VB45ARKK:~/flatter/build$
```
Test:
```python
from sage.all import *
from Crypto.Util.number import *
def flatter(M):
    import re
    from subprocess import check_output
    # compile https://github.com/keeganryan/flatter and put it in $PATH
    z = "[[" + "]\n[".join(" ".join(map(str, row)) for row in M) + "]]"
    ret = check_output(["flatter"], input=z.encode())
    return matrix(M.nrows(), M.ncols(), list(map(int, re.findall(b"-?\\d+", ret))))
M = [[-2, 2], [-2, 1]]
M = Matrix(ZZ, M) 
M = M.transpose()
M = flatter(M)
print(M)
M = [[-2, 2], [-2, 1]]
M = Matrix(ZZ, M) 
m = M.transpose()
print(m.LLL())
```
**Lưu ý:** Do thuật toán LLL thực hiện rút gọn theo cột của ma trận nên trước khi rút gọn cần phải dùng cú pháp `M.transpose()` để chuyển vị ma trận hoặc nếu ta đã sắp xếp đúng theo định dạng thì không cần phải chuyển vị nữa. 

**Một số định lí và tính chất**

Mục đích ban đầu của thuật toán LLL là phân tích các đa thức trong $\displaystyle \mathbb{Q}[ x]$, điều này thực hiện trong thời gian đa thức. Tuy nhiên trên đường đi, nó khôi phục một vector lưới có độ dài tối đa $\displaystyle \left(\frac{2}{\sqrt{3}}\right)^{m}$ lần so với vector ngắn nhất trong một số lưới $\displaystyle \mathcal{L}$, tức là nó có thể giải được $\displaystyle SVP_{\left( 2/\sqrt{3}\right)^{m}}$ trong thời gian $\displaystyle O\left( n^{6}\log_{3} B\right)$ trong đó $\displaystyle B$ là độ dài của vector cơ sở đầu vào dài nhất.

Cụ thể ta có các định lí sau đây

**Định lí 1.** Cho $\displaystyle \mathbf{B} =\{\mathbf{b}_{1} ,...,\mathbf{b}_{n}\}$ là một cơ sở lattice và $\displaystyle \mathbf{B}^{*} =\left\{\mathbf{b}_{1}^{*} ,...,\mathbf{b}_{n}^{*}\right\}$ là cơ sở sau khi trực giao hóa Gram Schmidt. Khi đó $\displaystyle \lambda _{1}(\mathcal{L}(\mathbf{B})) \geqslant \min_{i\in \{1,...,n\}} \| \mathbf{b}_{i}^{*} \|$.

Chứng minh. 

Xét $\displaystyle \mathbf{x} =( x_{1} ,...,x_{n}) \in \mathbb{Z}^{n}$ là vector nhỏ nhất khác 0 và vì $\displaystyle \mathbf{x}$ khác vector 0 cho nên tồn tại một chỉ số $\displaystyle j$ lớn nhất sao cho $\displaystyle x_{j} \neq 0$. Khi đó $\displaystyle x_{i} =0,\forall i >j$. Bây giờ xét điểm nguyên $\displaystyle \mathbf{xB}$ thì ta 
$$
\begin{gather*}
 | \langle \mathbf{xB} ,\mathbf{b}_{j}^{*} \rangle  | =\mid \langle \sum _{i=1}^{n} x_{i}\mathbf{b}_{i} ,\mathbf{b}_{j}^{*} \rangle  | \\
=\mid \sum _{i=1}^{n} x_{i} \langle \mathbf{b}_{i} ,\mathbf{b}_{j}^{*} \rangle  | \geqslant |x_{j} |\langle \mathbf{b}_{j} ,\mathbf{b}_{j}^{*} \rangle = | x_{j} | \| \mathbf{b}_{j}^{*} \| ^{2}
\end{gather*}
$$
Mà lại có 
$$
\begin{gather*}
 | \langle \mathbf{xB} ,\mathbf{b}_{j}^{*} \rangle  | \leqslant \| \mathbf{xB} \| \cdotp \| \mathbf{b}_{j}^{*} \| \Longrightarrow  | x_{j} | \cdotp \| \mathbf{b}_{j}^{*} \| ^{2} \leqslant \| \mathbf{xB} \| \cdotp \| \mathbf{b}_{j}^{*} \| \\
\Longrightarrow  | x_{j} | \cdotp \| \mathbf{b}_{j}^{*} \| \leqslant \| \mathbf{xB} \| \\
\Longrightarrow \min_{i\in \{1,...,n\}} \| \mathbf{b}_{i}^{*} \| \leqslant \| \mathbf{xB} \| 
\end{gather*}
$$


**Định lí 2.** Cho $\displaystyle \mathbf{B} =\{\mathbf{b}_{1} ,...,\mathbf{b}_{n}\}$ là một cơ sở rút gọn $\displaystyle \delta -LLL$ rút gọn. Khi đó $\displaystyle \| \mathbf{b}_{1} \| \leqslant \left(\frac{2}{\sqrt{4\delta -1}}\right)^{n-1} \lambda _{1}$.


Định lí này có ý nghĩa rằng: vector đầu tiên sau khi rút gọn LLL chưa chắc là vector ngắn nhất nhưng nó là một vector gần với vector ngắn nhất của mạng.

Từ điều kiện rút gọn lattice ta có 
$$
\begin{equation*}
\left( \delta -\mu _{i+1,i}^{2}\right) \| \mathbf{b}_{i}^{*} \| ^{2} \leqslant \| \mathbf{b}_{i+1}^{*} \| ^{2}
\end{equation*}
$$
Mà ta có $\displaystyle \mu _{i+1,i} \leqslant \frac{1}{2}$ kéo theo $\displaystyle \left(\frac{4\delta -1}{4}\right) \| \mathbf{b}_{i}^{*} \| ^{2} \leqslant \mathbf{\| b}_{i+1}^{*} \| ^{2}$

Cho nên 
$$
\begin{gather*}
\| \mathbf{b}_{i}^{*} \| ^{2} \leqslant \mathbf{\| b}_{i+1}^{*} \| ^{2}\left(\frac{4}{4\delta -1}\right)\\
\Longrightarrow \| \mathbf{b}_{1}^{*} \| \leqslant \| \mathbf{b}_{i}^{*} \| \left(\frac{2}{\sqrt{4\delta -1}}\right)^{i-1}\\
\Longrightarrow \| \mathbf{b}_{1}^{*} \| \leqslant \| \mathbf{b}_{n}^{*} \| \left(\frac{2}{\sqrt{4\delta -1}}\right)^{n-1}
\end{gather*}
$$

Ngoài ra ta còn có một khái niệm khác gọi là heuristic. Heuristic là các giả định dùng để ước lượng số lượng vector mà lattice có trong một miền nhất định. Hai phương pháp heuristic thường được sử dụng là Gaussian Heuristic và Geometric Series Assumption GSA. 
Mọi người có thể xem qua bài viết sau: [LLL on the Average](https://link.springer.com/chapter/10.1007/11792086_18). Tác giả có đưa ra một nhận xét như sau:
**Giả thuyết:** Với mỗi lưới ngẫu nhiên $\mathcal{L}$ có rank là $n$ và cho $b_1,...,b_n$ là một cơ sở rút gọn LLL của nó. Thì khi đó 
$$
\displaystyle \| b_{i} \| \leqslant \sqrt{i}( 1.02)^{n}\det( L)^{1/n}
$$


Gaussian Heuristic là một ước lượng của $\lambda_1(\mathcal{L})$: Mật đố của các điểm là $1/\det(\mathcal{L})$ , vì vậy trong một quả cầu có bán kính là $r$, chúng ta mong đợi sẽ có $v_n \times r^n/\det(\mathcal{L})$  các điểm lưới, trong đó $v_n$ là thể tính của quả cầu đơn vị $n$ chiều. Cụ thể, điều này đưa ra một ước lượng cho $\lambda_1$ thông qua $v_n\lambda_{1}^{n}/\det(\mathcal{L}) \approx 1$. Vì thể tích của quả cầu đơn vị được tính bởi 

$$
\displaystyle v_{n} \approx \frac{1}{\sqrt{2n\pi }}\left(\frac{2\pi e}{n}\right)^{n/2}
$$
GH đưa giả ra định:
$$ 
\displaystyle \lambda _{1} \approx \det(\mathcal{L})^{1/n}\sqrt{\frac{n}{2\pi e}}
$$

## Bài toán CVP 

Như đã trình bày ở trên thì thuật toán LLL giúp ta giải bài toán SVP và apprSVP. Bài toán tiếp theo mà ta tìm hiểu sẽ là bài toán CVP và apprCVP tức là bài toán tìm vector gần nhất với vector cho trước. Cụ thể với lưới $\displaystyle \mathcal{L}$ và một target vector $\displaystyle t$, ta sẽ tìm $\displaystyle v\in \mathcal{L}$ sao cho $\displaystyle \| v-t\|$ là nhỏ nhất. 

### Thuật toán Babai

Đầu tiên để sinh ra một cơ sở thuận tiện cho tính toán thì ta cần làm 2 việc đó là rút gọn LLL cho cơ sở và chuyển cơ sở thành cơ sở trực giao với thuật toán gram schmidt. Chẳng hạn với cơ sở trực giao $\displaystyle \mathbf{B} =\{\mathbf{b}_{1} ,...,\mathbf{b}_{n}\}$ thì độ dài của mỗi vector trong $\displaystyle \mathcal{L}(\mathbf{B})$ được tính bởi 

$$
\begin{equation*}
\| a_{1}\mathbf{b}_{1} +...+a_{n}\mathbf{b}_{n} \| ^{2} =a_{1}^{2} \| \mathbf{b}_{1} \| ^{2} +...+a_{n}^{2} \| \mathbf{b}_{n} \| ^{2}
\end{equation*}
$$

Ta xét một siêu phẳng sinh bởi $\displaystyle n-1$ vectors đầu tiên của lưới và đặt $\displaystyle t'=t-c_{n} b_{n}$ trong đó $\displaystyle c_{n}$ là số nguyên được chọn sao cho siêu phẳng được tịnh tiến bởi $\displaystyle c_{n}\mathbf{b}_{n}$ gần $\displaystyle t$ nhất có thể. $\displaystyle c_{n}$ sẽ được tính bởi $\displaystyle c_{n} =\left\lfloor \frac{\langle \mathbf{b} ,\mathbf{b}_{n}^{*} \rangle }{\langle \mathbf{b}_{n}^{*} ,\mathbf{b}_{n}^{*} \rangle }\right\rfloor$. Tiếp tục làm tương tự cho tới khi thu được tổng $\displaystyle c_{i}\mathbf{b}_{i}$ và cũng chính là giá trị mà ta cần tìm. 

**Định nghĩa siêu phẳng:** Tập $X$ là siêu phẳng trong $\mathbb{R}^n$ nếu $X$ là không gian affine $n-1$ chiều. 

Chi tiêt mọi người có thể xem ở đây https://ecampusontario.pressbooks.pub/daisotuyentinh/chapter/hyperplanes-and-half-spaces/



![image](https://hackmd.io/_uploads/ByrORMcrxx.png)


Implement: 
```python
from sage.all import *
from sage.modules.free_module_integer import IntegerLattice
def flatter(M):
    import re
    from subprocess import check_output
    # compile https://github.com/keeganryan/flatter and put it in $PATH
    z = "[[" + "]\n[".join(" ".join(map(str, row)) for row in M) + "]]"
    ret = check_output(["flatter"], input=z.encode())
    return matrix(M.nrows(), M.ncols(), list(map(int, re.findall(b"-?\\d+", ret))))

def Babai_CVP(mat,target):
    M = flatter(mat)
    G = M.gram_schmidt()[0]
    diff = target 
    for i in reversed(range(G.nrows())):
        diff -= M[i] * ((diff*G[i]) / (G[i]*G[i])).round()
    return target - diff 
```

### Kannan's Embedding

Một cách khác để xử lí CVP đó là nhúng vector cần tính vào trong ma trận cơ sở của lưới và chuyển từ bài CVP thành SVP. 

Xét $\displaystyle \mathbf{B} =\{\mathbf{b}_{1} ,...,\mathbf{b}_{n}\}$ là cơ sở của lưới và $\displaystyle \mathbf{t} =( t_{1} ,...,t_{n})$ là target vector. Nghiệm của CVP lúc này sẽ có dạng $\displaystyle c_{1}\mathbf{b}_{1} +...+c_{n}\mathbf{b}_{n}$. Như vậy 
$$
\begin{gather*}
\mathbf{t} \approx \sum _{i=1}^{n} c_{i}\mathbf{b}_{i}\\
\Longrightarrow \mathbf{t} =\sum _{i=1}^{n} c_{i}\mathbf{b}_{i} +e\\
\Longrightarrow \mathbf{t} =\mathbf{xB} +e\ 
\end{gather*}
$$
trong đó ta có thể coi $\displaystyle e$ là sai số nhỏ. Xét một lưới $\displaystyle ( n+1) \times ( n+1)$ với các cơ sở như sau:
$$
\begin{equation*}
\mathbf{B} '=\begin{bmatrix}
\mathbf{B} & 0\\
\mathbf{t} & q
\end{bmatrix}
\end{equation*}
$$

Viết đầy đủ ma trận ra như sau:
$$
\begin{equation*}
\mathbf{B} '=\begin{bmatrix}
b_{11} & b_{12} & \cdots  & b_{1n} & 0\\
b_{21} & b_{22} & \cdots  & b_{2n} & 0\\
\vdots  & \vdots  & \ddots  & \vdots  & \vdots \\
b_{n1} & b_{n2} & \cdots  & b_{nn} & 0\\
t_{1} & t_{2} & \cdots  & t_{n} & q
\end{bmatrix}
\end{equation*}
$$


Như vậy lưới này sẽ có một vector nhỏ $\displaystyle ( e,q) =( e_{1} ,e_{2} ,...,e_{n} ,q)$ sinh bởi tổ hợp tuyến tính $\displaystyle ( -c_{1} ,...,-c_{n} ,1)$. 


Ví dụ: 

Giả sử ta có một ma trận như sau:	
$$
\begin{equation*}
B=\begin{pmatrix}
35 & 72 & -100\\
-10 & 0 & -25\\
-20 & -279 & 678
\end{pmatrix}
\end{equation*}
$$
là một lattice trong $\displaystyle \mathbb{R}^{3}$. Vector mục tiêu của ta là $\displaystyle w=( 100,100,100)$. Ta chọn trọng số $\displaystyle q=1$. Xây dựng ma trận mới và làm theo thuật toán ở trên:
$$
\begin{equation*}
B'=\begin{pmatrix}
35 & 72 & -100 & 0\\
-10 & 0 & -25 & 0\\
-20 & -279 & 678 & 0\\
100 & 100 & 100 & 1
\end{pmatrix}
\end{equation*}
$$

```python
M = Matrix(ZZ, [[35,72,-100,0],[-10,0,-25,0],[-20,-279,678,0],[100,100,100,1]])
target = vector(ZZ,[100,100,100])
M = flatter(M)
print(M)
for row in M:
    if row[-1] == 1:
        vec = target - vector(row[:-1])
        print(f"solution là {vec}")
```


## Bài toán ACD
Cho các tham số $\gamma,\eta,\rho$ và $p$ là một số nguyên lẻ có độ lớn là $\eta$-bit. Như vậy ta sẽ có 
$$
2^{\eta-1}<p <2^{\eta}
$$
$p$ không nhất thiết phải là số nguyên tố và ta sẽ xem xét kĩ hơn trong các biến thể khác của bài toán. Ta xét một tập hợp các mẫu thử như sau:

$$
\displaystyle \mathcal{D}_{\gamma ,\rho }( p) =\left\{pq+r\ |\ q\leftarrow \mathbb{Z} \ \cap \ \left[ 0,2^{\gamma } /p\right) ,\ r\ \leftarrow \mathbb{Z} \cap \left( -2^{\rho } ,2^{\rho }\right)\right\}
$$
Trên thực tế ta có giá trị của $\displaystyle \rho$ nhỏ hơn $\displaystyle \eta$ rất nhiều cho nên các mẫu thử từ $\displaystyle \mathcal{D}_{\gamma ,\rho }( p)$ sẽ gồm các số $\displaystyle x_{i} < 2^{\gamma }$ với xác suất lớn. Hơn nữa với $\displaystyle t$ đủ lớn và $\displaystyle x_{1} ,...,x_{t}$ là các mẫu thử từ $\displaystyle \mathcal{D}_{\gamma ,\rho }( p)$ thì ta kì vọng rằng sẽ có ít nhất một giá trị $\displaystyle x_{i}$ sao cho
$$
\begin{equation*} 
2^{\gamma -1} < x_{i} < 2^{\gamma }
\end{equation*}
$$
Lúc này bài toán ACD được phát biểu như sau: Cho một số hữu hạn các giá trị được làm nhiễu $x_i$ từ $\mathcal{D}_{\gamma ,\rho }( p)$, hãy tính toán lại giá trị của $p$. 

Một biến thể của bài là bài PACD - partial approximate common divisor problem: Tương tự bài ACD nhưng ta được biết được một mẫu "sạch" không bị làm nhiễu là $x_0 = pq_0$
Ngoài ra ta còn có các decisional versions của bài nhưng trong phạm của bài viết này mình sẽ không đề cập đến (nếu có mình sẽ viết lại trong thư mục Theoretical Cryptography)

Ngoài ra còn một phiên bản khác là CRT-ACD mọi người có thể xem tại [đây](https://nutmic2019.imj-prg.fr/confpapers/CRT-GCD.pdf)

Tiếp theo là các cách attacks cho bài toán trên

### Simultaneous Diophantine approximation - SDA
Attack này được dùng trong trường hợp giá trị làm nhiễu quá lớn để có thể vét cạn và ta có nhiều mẫu bị nhiễu. Tức là các giá trị $r_i$ lớn và ta được biết nhiều giá trị $x_i$. 
Ý tưởng chính của attack này đó là từ phương trình $x_i = pq_i + r_i$  với $1 \leq i \leq t$ thì ta có thể viết lại dưới dạng: 
$$
\frac{x_i}{x_0} \approx \frac{q_i}{q_0}
$$
với mỗi $1 \leq i \leq t$. Ta có thể xem $\displaystyle \frac{q_i}{q_0}$ như một xấp xỉ Diophante của $\displaystyle \frac{x_i}{x_0}$. Như vậy nếu như ta xác định được giá trị của $\displaystyle \frac{q_i}{q_0}$ thì ta có thể giải được bài toán ACD bằng cách tính $r_0 \equiv x_0 (\bmod q_0)$ và có $(x_0-r_0)/q_0=p$. Thực tế ta không cần giá trị của mẫu $x_0 = pq_0$ để giải bài toán trên. 
Ta sẽ xây dựng một lattice $\mathbb{B}$ có rank là $t+1$ như sau: 
$$
\displaystyle \mathbb{B} =\begin{pmatrix} 2^{\rho +1} & x_{1} & x_{2} & \dotsc & x_{t}\\ & -x_{0} & -x_{0} & & \\ & & -x_{0} & & \\ & & & \ddots & \\ & & & & -x_{0} \end{pmatrix}
$$
Nó sẽ chứa một vector $\displaystyle \mathbf{v}$ là tổ hợp tuyến tính của $\displaystyle ( q_{0} ,q_{1} ,...,q_{t})$ như sau:
$$
\begin{gather*}
\mathbf{v} =( q_{0} ,q_{1} ,...,q_{t})\mathbb{B}\\
=\left( 2^{\rho +1} q_{0} ,q_{0} x_{1} -q_{1} x_{0} ,...,q_{0} x_{t} -q_{t} x_{0}\right)\\
=\left( q_{0} 2^{\rho +1} ,q_{0} r_{1} -q_{1} r_{0} ,...,q_{0} r_{t} -q_{t} r_{0}\right)
\end{gather*}
$$

Vì ta có : với cặp $\displaystyle x_{i} =pq_{i} +r_{i} ,\ x_{j} =pq_{j} +r_{j}$ thì 

$$
\begin{gather*}
q_{i} =( x_{i} -r_{i}) /p\\
\Longrightarrow q_{i} x_{j} =( x_{i} -r_{i}) x_{j} /p\\
q_{j} =( x_{j} -r_{j}) /p\\
\Longrightarrow q_{j} x_{i} =( x_{j} -r_{j}) x_{i} /p\\
\Longrightarrow q_{i} x_{j} -q_{j} x_{i} =\frac{x_{i} x_{j} -r_{i} x_{j} -x_{i} x_{j} +x_{i} r_{j}}{p} =\frac{x_{i} r_{j} -r_{i} x_{j}}{p}
\end{gather*}
$$
Mặt khác 
$$
\begin{gather*}
q_{i} r_{j} =( x_{i} -r_{i}) r_{j} /p\\
q_{j} r_{i} =( x_{j} -r_{j}) r_{i} /p\\
\Longrightarrow q_{i} r_{j} -q_{j} r_{i} =( x_{i} r_{j} -x_{j} r_{i}) /p
\end{gather*}
$$
Vì $\displaystyle q_{i} \approx 2^{\gamma -\eta }$ cho nên chuẩn euclid (norm) của $\displaystyle \mathbf{v}$ sẽ xấp xỉ $\displaystyle \sqrt{t+1} \times 2^{\gamma -\eta +\rho +1}$

Bây giờ đối với ma trận $\displaystyle \mathbb{B}$ của ta thì theo Gaussian Heuristic ở trên, nếu như 
$$
\begin{equation*}
\sqrt{t+1} \times 2^{\gamma -\eta +\rho +1} < \sqrt{\frac{t+1}{2\pi e}}\det( L)^{1/( t+1)}
\end{equation*}
$$
thì ta có thể kì vọng vector $\displaystyle \mathbf{v}$ sẽ là vector ngắn nhất sinh ra bởi lưới. Như vậy ta sẽ chạy thuật toán LLL cho lưới trên và lấy phần tử $\displaystyle \mathbf{w}$ đầu tiên của vector kết quả chia cho $\displaystyle 2^{\rho +1}$. Đây chính là giá trị có thể có của $\displaystyle q_{0}$. Sau đó ta sẽ tính $\displaystyle r_{0} \equiv x_{0}(\bmod q_{0})$ và kiểm tra giá trị của $\displaystyle p=( x_{0} -r_{0}) /q_{0}$ bằng cách tính thử xem $\displaystyle x_{i}\bmod p$ có "nhỏ" hay không. 
Implement:
```python
from sage.all import *
def flatter(M):
    from subprocess import check_output
    from re import findall
    z = "[[" + "]\n[".join(" ".join(map(str, row)) for row in M) + "]]"
    ret = check_output(["flatter"], input=z.encode())
    return matrix(M.nrows(), M.ncols(), map(int, findall(b"-?\\d+", ret)))
def symmetric_mod(x, m):
    return int((x + m + m // 2) % m) - int(m // 2)
def SDA(x, rho):
    assert len(x) >= 2
    R = 2 ** (rho + 1)
    B = matrix(ZZ, len(x), len(x))
    B[0, 0] = R
    for i in range(1, len(x)):
        B[0, i] = x[i]
        B[i, i] = -x[0]
    B_ = flatter(B)   
    for v in B_:
        if v[0] != 0 and v[0] % R == 0:
            q0 = v[0] // R
            r0 = symmetric_mod(x[0], q0)
            p = abs((x[0] - r0) // q0)
            r = [symmetric_mod(xi, p) for xi in x]
            if all(-R < ri < R for ri in r):
                return int(p), r
```

(Nếu k có flatter thì mọi người có thể dùng `LLL` của sage =)) mà flatter lâu lâu cx hay lỏ,mn nên thử cả hai và nên cập nhật phiên bản mới của flatter trước khi chạy)

### Orthogonal based approach (OL)

### Multivariate polynomial approach (MP)

## Hidden Number Problem - HNP
Có hai phiên bản khác nhau của HNP, ở đây mình sẽ trình bày lại phiên bản quen thuộc hơn. Phiên bản còn lại mọi người có thể xem ở [đây](https://link.springer.com/chapter/10.1007/3-540-68697-5_11)


**Hidden Number Problem**. Cho $\displaystyle p$ là một số nguyên tố và $\displaystyle \alpha \in [ 1,p-1]$ là một số nguyên bí mật mà ta cần tìm với điều kiện rằng ta được biết $\displaystyle m$ cặp giá trị $\displaystyle \{( t_{i} ,a_{i})\}_{i=1}^{m}$ thỏa mãn 
$$
\begin{equation*} \beta _{i} -t_{i} \alpha +a_{i} =0\bmod p \end{equation*}
$$
trong đó các giá trị $\displaystyle \beta _{i}$ được ẩn đi và ta chỉ biết rằng $\displaystyle |\beta _{i} |< B$ với $\displaystyle B< p$ nào đó.
Có hai hướng tiếp cận đó là dựa vào bài toán CVP hoặc SVP.

Đối với thiết lập CVP, ta sẽ xét attice được xây dựng dựa trên ma trận sau:
$$
\begin{equation*}
\mathbf{B} =\begin{bmatrix}
p &  &  &  & \\
 & p &  &  & \\
 &  & \ddots  &  & \\
 &  &  & p & \\
t_{1} & t_{2} & \dotsc  & t_{m} & 1/p
\end{bmatrix}
\end{equation*}
$$

Ta viết lại phương trình HNP dưới dạng $\displaystyle \beta _{i} +a_{i} =t_{1} \alpha +k_{i} p$ với mỗi số nguyên $\displaystyle k_{i}$. Như vậy ta có một vector $\displaystyle ( \beta _{1} +a_{1} ,...,\beta _{m} +a_{m} ,\alpha /p)$ được sinh ra bởi tổ hợp tổ tuyến $\displaystyle \mathbf{x} =( k_{1} ,...,k_{m} ,\alpha )$. Đặt $\displaystyle \mathbf{t} =( a_{1} ,...,a_{m} ,0)$ và $\displaystyle \mathbf{u} =( \beta _{1} ,...,\beta _{m} ,\alpha /p)$ thì ta có $\displaystyle \mathbf{xB} -\mathbf{t} =\mathbf{u}$ trong đó độ dài của $\displaystyle \mathbf{u}$ (norm) bị chặn trên bởi $\displaystyle \sqrt{m+1} B$ trong khi định thức của $\displaystyle \mathbf{B}$ là $\displaystyle p^{m-1}$. Như vậy ta sẽ chuyển sang bài toán CVP với target vector là $\displaystyle \mathbf{t}$.  Để khôi phục lại $\displaystyle \alpha$ ta sẽ thử nhân phần tử cuối của vector với $\displaystyle p$. 

Còn đối với SVP, thì ta sẽ xét lattice sinh bởi ma trận sau đây:
$$
\begin{equation*}
\mathbf{B} =\begin{bmatrix}
p &  &  &  &  & \\
 & p &  &  &  & \\
 &  & \ddots  &  &  & \\
 &  &  & p &  & \\
t_{1} & t_{2} & \dotsc  & t_{m} & B/p & \\
a_{1} & a_{2} & \dotsc  & a_{m} &  & B
\end{bmatrix}
\end{equation*}
$$

Lattice này sẽ chứa một vector ngắn là 
$$
\begin{equation*}
\mathbf{u} '=( \beta _{1} ,...,\beta _{m} ,\alpha B/p,-B)
\end{equation*}
$$

sinh bởi tổ hợp tuyến tính $\displaystyle ( k_{1} ,...,k_{m} ,\alpha ,-1)$. Ta có $\displaystyle \| \mathbf{u} '\| < \sqrt{m+2} B$ và dựa vào các giả định ở trên về cơ sở rút gọn LLL thì ta có thể kì vọng rằng sẽ tìm được vector $\displaystyle \mathbf{u} '$ trong số các cơ sở của ma trận mới. Lưu ý thêm rằng, lattice này cũng chứa một vector ngắn là $\displaystyle ( 0,...,0,B,0)$, sinh bởi $\displaystyle ( -t_{1} ,...,-t_{m} ,p,0)$ cho nên $\displaystyle \mathbf{u} '$ có thể rơi vào vector ngắn thứ hai của cơ sở (hoặc nếu không thì ta có thể thử hết =))?)
```python
def hnp(p, T, A, B, lattice_reduction=None, verbose=False):
    r"""
    Returns the solution of the given hidden number problem instance. i.e. finds
    `\alpha \in [1, p - 1]` satisfying

    .. MATH::

        \beta_i - t_i \alpha + a_i \equiv 0 \pmod p

    where the `t_i` and `a_i` are given by ``T`` and ``A``, and the `\beta_i`
    are bounded above by ``B``.

    The implementation follows the algorithm as described in section 2.5 of [1].

    INPUT:

    - ``p`` -- The modulus `p` as described above.

    - ``T`` -- A list of integers representing the `t_i`.

    - ``A`` -- A list of integers representing the `a_i`.

    - ``B`` -- The upper bound on the `\beta_i` as described above.

    OUTPUT:

    The integer `\alpha` which is a solution to the HNP instance. If no solution
    could be found, None is returned.

    REFERENCES:

    [1] Martin R. Albrecht and Nadia Heninger. *On Bounded Distance Decoding with Predicate:
    Breaking the “Lattice Barrier” for the Hidden Number Problem.*
    In Lecture Notes in Computer Science, p. 528--558. Springer, 2021.
    https://link.springer.com/chapter/10.1007/978-3-030-77870-5_19
    """

    verbose = (lambda *a: print('[hnp]', *a)) if verbose else lambda *_: None

    if len(T) != len(A):
        raise ValueError(f'Expected number of t_i to equal number of a_i, but got {len(T)} and {len(A)}.')

    m = len(T)
    M = p * Matrix.identity(QQ, m)
    M = M.stack(vector(T))
    M = M.stack(vector(A))
    M = M.augment(vector([0] * m + [B / p] + [0]))
    M = M.augment(vector([0] * (m + 1) + [B]))
    M = M.dense_matrix()

    verbose('Lattice dimensions:', M.dimensions())
    lattice_reduction_timer = cputime()
    if lattice_reduction:
        M = lattice_reduction(M)
    else:
        M = M.LLL()
    verbose(f'Lattice reduction took {cputime(lattice_reduction_timer):.3f}s')

    for row in M:
        if row[-1] == -B:
            alpha = (row[-2] * p / B) % p
            if all((beta - t * alpha + a) % p == 0 for beta, t, a in zip(row[:m], T, A)):
                return alpha
        if row[-1] == B:
            alpha = (-row[-2] * p / B) % p
            if all((beta - t * alpha + a) % p == 0 for beta, t, a in zip(-row[:m], T, A)):
                return alpha

    return None

```

### Extended Hidden Number Problem - EHNP
EHNP là một biến thể mở rộng của HNP. Cụ thể bài toán được phát biểu như sau:
**Extended Hidden Number Problem**. Cho $p$ là một số nguyên tố và $x \in [1,p-1]$ là một số nguyên bí mật thỏa mãn:
$$
\displaystyle x=\overline{x} +\sum _{j=1}^{m} 2^{\pi _{j}} x_{j}
$$
trong đó ta biết giá trị của $\displaystyle \overline{x}$ và $\displaystyle \pi _{j}$, và các số nguyên $\displaystyle x_{j}$ thỏa mãn $\displaystyle 0\leqslant x_{j} < 2^{v_{j}}$ (ta không được biết $\displaystyle x_{j}$) với $\displaystyle v_{j}$ cho trước. Bây giờ giả sử ta có $\displaystyle d$ phương trình dưới dạng 
$$
\begin{equation*}
\alpha _{i}\sum _{j=1}^{m} 2^{\pi _{j}} x_{j} +\sum _{j=1}^{l_{i}} \rho _{i,j} k_{i,j} =\beta _{i} -\alpha _{i}\overline{x} \ (\bmod p)
\end{equation*}
$$
với $\displaystyle 1\leqslant i\leqslant d$ và $\displaystyle \alpha _{i} \neq 0(\bmod p) ,\rho _{i,j}$ và $\displaystyle \beta _{i}$ được biết giá trị. Hơn nữa các giá trị $\displaystyle k_{i,j}$ bị chặn bởi $\displaystyle 0\leqslant k_{i,j} < 2^{\mu _{i,j}}$ và ta không biết giá trị của các số này. Bài toán của ta sẽ là tìm cách khôi phục lại giá trị $\displaystyle x$ từ các phương trình trên. 
Như vậy, một trường hợp cho bài EHNP sẽ là: 
$$

\begin{equation*}
\left(\overline{x} ,p,\{\pi _{j} ,v_{j}\}_{j=1}^{m} ,\ \left\{\alpha _{i} ,\{\rho _{i,j} ,\mu _{i,j}\}_{j=1}^{l_{i}} ,\beta _{i}\right\}_{i=1}^{d}\right)
\end{equation*}

$$
Mọi người để ý rằng ta chỉ biết khoảng chặn của các giá trị bị ẩn, nói đơn giản chính là độ lớn về bit của các số này. 




## CTF Challenges

Một số bài CTF có ứng dụng Lattice trong lời giải.


## Tài liệu tham khảo
**[1]** Abstract Algebra: Theory and Applications ,Thomas W. Judson, Stephen F. Austin, State University, August 11, 2012 
**[2]** [Predicting Lattice Reduction, Nicolas Gama and Phong Q.Nguyen](https://www.iacr.org/archive/eurocrypt2008/49650031/49650031.pdf)
**[3]** [NGHIÊN CỨU MỘT SỐ HỆ MẬT LATTICE TRONG HỌ MÃ HÓA ĐỒNG CẤU ĐẦY ĐỦ, Khuất Thanh Sơn, Nguyễn Trường Thắng, Lê Phê Đô, Bùi Trọng A Đam](http://vap.ac.vn/Portals/0/TuyenTap/2021/12/22/1ecec417207345d595e011cb434f7fe8/70_FAIR2021_paper_86.pdf?fbclid=IwZXh0bgNhZW0CMTAAAR2d04r_wPXW1k73WUNgvopc-q4OIlhh7EIkq6K5kwQOlZAM8tkRaTY7ups_aem_UiulJSBIYNoAPE_-a0z24A)
**[4]** Giáo trình đại số tuyến tính - Ngô Việt Trung, Bộ sách cao học, Viện toán học.
**[5]** [Determinants and Volumes](https://textbooks.math.gatech.edu/ila/determinants-volumes.html)        
**[6]** https://github.com/Giapppp/Lattice-Based-Cryptography
**[7]** A Gentle Tutorial for Lattice-Based Cryptanalysis, https://eprint.iacr.org/2023/032.pdf
**[8]** A Course in Computational Algebraic Number Theory, Henri Cohen, Springer
**[9]** https://magicfrank00.github.io/writeups/posts/lll-to-solve-linear-equations/
**[10]** https://ur4ndom.dev/static/files/latticetraining/practical_lattice_reductions.pdf
**[11]** [Algorithms for the Approximate Common Divisor Problem](https://eprint.iacr.org/2016/215.pdf)
