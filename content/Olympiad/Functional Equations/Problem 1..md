**Đề bài** Chosố nguyên dương $\displaystyle n$. Tìm tất cả các hàm $\displaystyle f:\mathbb{R}^{+}\rightarrow \mathbb{R}^{+}$ thỏa mãn 
$$
\begin{equation*}
f\left( xf( y) +f( x)^{n}\right) =yf( x) +f( x)^{n}
\end{equation*}
$$
*Lời giải.*
Ta có $\displaystyle f$ là hàm đơn ánh. Thật vậy, xét $\displaystyle a,b >0$ sao cho $\displaystyle f( a) =f( b)$ thì ta có 
$$
\begin{equation*}
f\left( xf( a) +f( x)^{n}\right) =f\left( xf( b) +f( x)^{n}\right) =af( x) +f( x)^{n} =bf( x) +f( x)^{n}
\end{equation*}
$$
Suy ra $\displaystyle a=b$ và $\displaystyle f$ đơn ánh. 

Ngoài ra ta cũng có $\displaystyle f$ không bị chặn vì $\displaystyle yf( x) +f( x)^{n}\rightarrow \infty$ với $\displaystyle x$ cố định và $\displaystyle y\rightarrow \infty$. 

Đặt $\displaystyle A=\{x >0:f( x) =x\}$. Xét $\displaystyle \alpha =f( 1) +f( 1)^{n} \in A$. Thay $\displaystyle P( \alpha ,\alpha )$ thì được 
$$
\begin{equation*}
f\left( \alpha ^{2} +\alpha ^{n}\right) =\alpha ^{2} +\alpha ^{n}
\end{equation*}
$$
Vậy cứ hễ $\displaystyle \alpha \in A$ thì ta có $\displaystyle \alpha ^{2} +\alpha ^{n} \in A$. Xét $\displaystyle P( x,x)$ ta cũng có 
$$
\begin{equation*}
f\left( xf( x) +f( x)^{n}\right) =xf( x) +f( x)^{n}
\end{equation*}
$$

Suy ra $\displaystyle xf( x) +f( x)^{n} \in A$. Ta sẽ thử một vài phép thế liên quan đến tập $\displaystyle A$ để xem thử co tính chất gì đặc biệt không (tạm thời đây là cách duy nhất để ta khai thác phương trình hàm). Xét $\displaystyle P( \alpha ,y)$ ta có 
$$
\begin{gather*}
f\left( \alpha f( y) +\alpha ^{n}\right) =y\alpha +\alpha ^{n}\\
\Longrightarrow f\left( \alpha f\left( \alpha f( y) +\alpha ^{n}\right)\right) +\alpha ^{n}) =\alpha \left( \alpha f( y) +\alpha ^{n}\right) +\alpha ^{n}\\
\Longrightarrow f\left( y\alpha ^{2} +\alpha ^{n+1} +\alpha ^{n}\right) =\alpha ^{2} f( y) +\alpha ^{n+1} +\alpha ^{n}\\
\Longrightarrow f\left( y\alpha ^{2} +C\right) =\alpha ^{2} f( y) +C
\end{gather*}
$$
Ta có được hai đẳng thức $\displaystyle f\left( \alpha f( x) +\alpha ^{n}\right) =x\alpha +\alpha ^{n}$ và $\displaystyle f\left( \alpha ^{2} x+C\right) =\alpha ^{2} f( x) +C,\forall x >0,\forall \alpha \in A$. Ta muốn tạo đối xứng để triệt tiêu bớt các hằng số và đưa về dạng đơn giản hơn. Để có được điều đó ta xét phép thế $\displaystyle P\left( x,\alpha f( y) +\alpha ^{n}\right)$ thì được 
$$
\begin{gather*}
f\left( x\left( y\alpha +\alpha ^{n}\right) +f( x)^{n}\right) =\left( \alpha f( y) +\alpha ^{n}\right) f( x) +f( x)^{n} =\alpha f( x) f( y) +\alpha ^{n} f( x) +f( x)^{n}\\
\Longrightarrow f\left( xy\alpha +\alpha ^{n} x+f( x)^{n}\right) =\alpha f( x) f( y) +\alpha ^{n} f( x) +f( x)^{n}
\end{gather*}
$$
Ta phân tích như sau : Đầu tiên ta thử hoán đổi vai trò của $\displaystyle x,y$ xem sao 
$$
\begin{gather*}
f\left( xy\alpha +\alpha ^{n} y+f( y)^{n}\right) =\alpha f( x) f( y) +\alpha ^{n} f( y) +f( y)^{n}\\
\Longrightarrow f\left( xy\alpha +\alpha ^{n} y+f( y)^{n}\right) -f\left( xy\alpha +\alpha ^{n} x+f( x)^{n}\right) =\alpha ^{n}( f( y) -f( x)) +f( y)^{n} -f( x)^{n}
\end{gather*}
$$
Vậy cách này không hiệu quả lắm, ta cũng không thể thế $\displaystyle y=\frac{y}{\alpha x}$ để triệt tiêu đi được. Và về phải còn chứa thêm đại lượng $\displaystyle f( y)^{n} ,f( x)^{n}$. Vấn đề chính trong bài này đó là làm sao làm mất đi $\displaystyle f( x)^{n}$ để thuận tiện cho biến đổi. Cho nên ta cần phải thử một phép thế khác. Ta quan sát thấy rằng : nếu cho cả $\displaystyle x,y$ di động thì rất khó kiểm soát. Thay vào đó ta sẽ cố định $\displaystyle x$ và thay $\displaystyle y$ bởi một giá trị nào đó để hoán đổi với $\displaystyle \alpha$. Nếu làm được như vậy thì ta có thể triệt tiêu hoàn toàn đi $\displaystyle f( x)^{n}$. Ở đây ta xét $\displaystyle y=\beta \in A$ thì sẽ có 
$$
\begin{equation*}
f\left( x\alpha \beta +\alpha ^{n} \beta +\beta ^{n}\right) =\beta \alpha f( x) +\alpha ^{n} \beta +\beta ^{n}
\end{equation*}
$$
Hoán đổi vị trí $\displaystyle \alpha ,\beta$ ta có 
$$
\begin{gather*}
f\left( x\alpha \beta +\beta ^{n} \alpha +\alpha ^{n}\right) =\alpha \beta f( x) +\beta ^{n} \alpha +\alpha ^{n}\\
\Longrightarrow f\left( x\alpha \beta +\beta ^{n} \alpha +\alpha ^{n}\right) -f\left( x\alpha \beta +\alpha ^{n} \beta +\beta ^{n}\right) =\beta ^{n} \alpha +\alpha ^{n} -\alpha ^{n} \beta -\beta ^{n}
\end{gather*}
$$
Xét $\displaystyle x\rightarrow \frac{x-\beta ^{n} \alpha -\alpha ^{n}}{\alpha \beta }$ và cần thêm điều kiện 
$$
\begin{gather*}
\alpha ^{n} +\beta ^{n} \alpha \neq \alpha ^{n} \beta +\beta ^{n}\\
\leftrightarrow \alpha ^{n}( 1-\beta ) \neq \beta ^{n}( 1-\alpha )\\
\leftrightarrow \frac{\alpha ^{n}}{1-\alpha } \neq \frac{\beta ^{n}}{1-\beta }
\end{gather*}
$$
Tồn tại hai số $\displaystyle \alpha ,\beta$ như vậy vì tập $\displaystyle A$ không bị chặn trên. Ta đưa được về đẳng thức 
$$
\begin{equation*}
f( x+\Delta ) =f( x) +\Delta ,\forall x >0,\Delta  >0,\Delta =\beta ^{n} \alpha +\alpha ^{n} -\alpha ^{n} \beta -\beta ^{n}
\end{equation*}
$$
Ta chọn được $\displaystyle \alpha ,\beta$ như vậy thỏa mãn đẳng thức trên. Bây giờ quay trở lại bài toán ban đầu 
$$
\begin{equation*}
f\left( xf( y) +f( x)^{n}\right) =yf( x) +f( x)^{n} ,\forall x,y >0
\end{equation*}
$$
Cho $\displaystyle y$ đủ lớn và xét $\displaystyle y\rightarrow y+\Delta$
$$
\begin{equation*}
f\left( x( f( y) +\Delta ) +f( x)^{n}\right) =f\left( xf( y) +x\Delta +f( x)^{n}\right) =yf( x) +\Delta f( x) +f( x)^{n}
\end{equation*}
$$
Cho $\displaystyle x=1$ ta được 
$$
\begin{gather*}
f\left( f( y) +\Delta +f( 1)^{n}\right) =yf( 1) +\Delta f( 1) +f( x)^{n}\\
=f\left( f( y) +f( 1)^{n}\right) +\Delta =yf( 1) +f( x)^{n} +\Delta \\
\Longrightarrow f( 1) =1
\end{gather*}
$$
Xét $\displaystyle P( 1,y)$ được 
$$
\begin{equation*}
f( f( y) +1) =y+1,\forall y >0
\end{equation*}
$$
Suy ra $\displaystyle f$ toàn ánh trên $\displaystyle ( 1;+\infty )$. Ngoài ra từ đẳng thức trên tiếp tục thay $\displaystyle y\rightarrow f( y) +1$ ta có được 
$$
\begin{equation*}
f( y+2) =f( y) +2,\forall y >0
\end{equation*}
$$
Vấn đề chính của ta bây giờ vẫn là $\displaystyle f( x)^{n}$ vì ta vẫn chưa biết cách để khử đại lượng này một cách hợp lí. Lặp lại liên tục 2 đẳng thức ở trên ta có 
$$
\begin{gather*}
f( f( y+2) +1) =f( f( y) +3) =y+3\\
\rightarrow f( f( f( y) +3) +1) =f( y+4) =f( y) +4
\end{gather*}
$$
Vậy quy nạp suy ra $\displaystyle f( f( y) +2n+1) =y+2n+1$ và $\displaystyle f( y+2n) =f( y) +2n,\forall y >0,n\in \mathbb{Z}_{\geqslant 0}$. Ngoài ra ta cũng chứng minh được $\displaystyle f( n) =n,\forall n\in \mathbb{Z}_{ >0}$. Từ đây ta xét $\displaystyle P( 2,y)$ thì được 
$$
\begin{equation*}
f\left( 2f( y) +2^{n}\right) =2y+2^{n} =f( 2f( y)) +2^{n}
\end{equation*}
$$
Do $\displaystyle f\left( y+2^{n}\right) =y+2^{n}$ do $\displaystyle 2^{n}$ chẵn như ta nhận xét ở trên. Điều này dẫn tới $\displaystyle f( 2f( y)) =2y,\forall y >0$ và $\displaystyle f$ là toàn ánh. Tương tự ta có $\displaystyle P( 4,y)$ thì được 
$$
\begin{gather*}
f\left( 4f( y) +4^{n}\right) =4y+4^{n} =f( 4f( y)) +4^{n}\\
\Longrightarrow f( 4f( y)) =4y
\end{gather*}
$$
Mặt khác từ $\displaystyle f( 2f( y)) =2y$ ta thay $\displaystyle y\rightarrow 2f( y)$ thì được 
$$
\begin{gather*}
f( 2f( 2f( y))) =f( 4y) =4f( y)\\
\Longrightarrow f( f( 4f( y)) =4f( y)
\end{gather*}
$$
Mà $\displaystyle f( y)$ toàn ánh nên $\displaystyle 4f( y)$ cũng toàn ánh dẫn tới $\displaystyle f( f( y)) =y,\forall y >0$. Từ đây ta suy ra được đẳng thức 
$$
\begin{equation*}
f( f( f( y)) +1) =f( y+1) =f( y) +1,\forall y >0
\end{equation*}
$$
Xét $\displaystyle P\left(\frac{1}{f( y)} ,y\right)$ ta được 

$$
\begin{gather*}
f\left( 1+f\left(\frac{1}{f( y)}\right)^{n}\right) =yf\left(\frac{1}{f( y)}\right) +f\left(\frac{1}{f( y)}\right)^{n}\\
\Longrightarrow f\left( 1+f\left(\frac{1}{y}\right)^{n}\right) =f( y) f\left(\frac{1}{y}\right) +f\left(\frac{1}{y}\right)^{n}\\
\Longrightarrow f\left( 1+f( y)^{n}\right) =f( y) f\left(\frac{1}{y}\right) +f( y)^{n} =f\left( f( y)^{n}\right) +1
\end{gather*}
$$
Bây giờ xét $\displaystyle P\left( x,\frac{1}{f( x)}\right)$ ta lại có 
$$
\begin{gather*}
f\left( xf\left(\frac{1}{f( x)}\right) +f( x)^{n}\right) =1+f( x)^{n} =f\left( f\left( f( x)^{n}\right) +1\right)\\
\Longrightarrow f( x)^{n} +xf\left(\frac{1}{f( x)}\right) =f\left( f( x)^{n}\right) +1
\end{gather*}
$$
Từ đây thu được $\displaystyle f( y) f\left(\frac{1}{y}\right) =yf\left(\frac{1}{f( y)}\right) ,\forall y >0$. Nếu các phép thế đơn biến $\displaystyle y$ không hiệu quả thì ta thử kết hợp cả $\displaystyle x,y$ lại xem sao, tận dụng những đẳng thức ta vừa thu được. Ta xét $\displaystyle P( x,1)$ thì được 
$$
\begin{equation*}
f\left( x+f( x)^{n}\right) =f( x) +f( x)^{n} ,\forall x >0
\end{equation*}
$$
Bây giờ cho $\displaystyle P( x,f( y))$ đưa về 
$$
\begin{equation*}
f\left( xy+f( x)^{n}\right) =f( x) f( y) +f( x)^{n}
\end{equation*}
$$
Thay $\displaystyle y\rightarrow y+1$ được
$$
\begin{equation*}
f\left( xy+x+f( x)^{n}\right) =f( x) f( y) +f( x) +f( x)^{n}
\end{equation*}
$$
Thay $\displaystyle x\rightarrow \frac{1}{y}$ được 
$$
\begin{equation*}
f\left(\frac{1}{y} +f\left(\frac{1}{y}\right)^{n} +1\right) =f\left(\frac{1}{y} +f\left(\frac{1}{y}\right)^{n}\right) +1=f( y) f\left(\frac{1}{y}\right) +f\left(\frac{1}{y}\right) +f\left(\frac{1}{y}\right)^{n}
\end{equation*}
$$
Mà 
$$
\begin{equation*}
f\left(\frac{1}{y} +f\left(\frac{1}{y}\right)^{n}\right) =f\left(\frac{1}{y}\right) +f\left(\frac{1}{y}\right)^{n}
\end{equation*}
$$
từ đẳng thức $\displaystyle f\left( x+f( x)^{n}\right) =f( x) +f( x)^{n}$ ta thế ở trên. Cho nên $\displaystyle 1=f( y) f\left(\frac{1}{y}\right)$. Quay trở lại ta có 
$$
\begin{equation*}
f( y) f\left(\frac{1}{y}\right) =yf\left(\frac{1}{f( y)}\right) =1
\end{equation*}
$$
Mà ta lại có
$$
\begin{gather*}
f( x)^{n} +xf\left(\frac{1}{f( x)}\right) =f\left( f( x)^{n}\right) +1\\
\Longrightarrow f\left( f( x)^{n}\right) =f( x)^{n} ,\forall x >0
\end{gather*}
$$
Vì $\displaystyle f$ toàn ánh nên $\displaystyle f( x)^{n}$ cũng toàn ánh và từ đây ta có được $\displaystyle f( x) =x,\forall x >0$ và bài toán hoàn tất. 