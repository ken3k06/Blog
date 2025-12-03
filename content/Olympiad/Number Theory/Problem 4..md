**Đề bài.** Cho $\displaystyle p$ là số nguyên tố và $\displaystyle k$ là một số nguyên dương. Tập $\displaystyle S$ gồm các số nguyên dương $\displaystyle a$ thỏa mãn $\displaystyle 1\leqslant a\leqslant p-1$ và đồng thời tồn tại $\displaystyle x$ nguyên dương sao cho $\displaystyle a\equiv x^{k}(\bmod p)$. Giả sử rằng $\displaystyle 3\leqslant |S|\leqslant p-2$. Chứng minh rằng các phần tử của $\displaystyle S$ không thể sắp xếp thành một cấp số cộng được.
*Lời giải.*
Ta sử dụng lại 1 kết quả quen thuộc : Tổng các thặng dư bậc cao theo modulo $\displaystyle p$ chia hết cho $\displaystyle p$. Thật vậy, xét $\displaystyle a$ là một thặng dư bậc $\displaystyle n$ của $\displaystyle m=p^{k}$ thì điều kiện cần và đủ sẽ là 

$$
\begin{equation*}
a^{\frac{\varphi ( m)}{\gcd( n,\varphi ( m))}} \equiv 1(\bmod m)
\end{equation*}
$$

Do đó, nếu gọi $\displaystyle g$ là căn nguyên thủy của $\displaystyle m$ thì tồn tại một chỉ số $\displaystyle i_{a}$ sao cho 
$$
\begin{equation*}
a\equiv g^{i_{a}}(\bmod m)
\end{equation*}
$$
và từ nhận xét ở trên ta cần có $\displaystyle d=( n,\varphi ( m)) |i_{a}$. Vậy tập các số $\displaystyle i_{a}$ thỏa mãn sẽ là $\displaystyle \{d,2d,...,Md\}$ trong đó $\displaystyle M=\frac{\varphi ( m)}{d}$. Tiếp đến ta sẽ xét tổng 
$$
\begin{equation*}
1+g^{d} +g^{2d} +...+g^{\varphi ( m) -d}
\end{equation*}
$$
Đặt $\displaystyle x=g^{d}$ thì tổng sẽ đưa về 
$$
\begin{equation*}
1+x^{2} +...+x^{\frac{\varphi ( m)}{d} -1} =\frac{x^{\frac{\varphi ( m)}{d}} -1}{x-1} =\frac{g^{\varphi ( m)} -1}{g^{d} -1} \equiv 0(\bmod p)
\end{equation*}
$$
Suy ra ta có điều phải chứng minh. Bây giờ, quay ngược lại bài toán ban đầu của ta, thì lúc này ta gọi tập $\displaystyle S=\{a,a+k,...,a+( d-1) k\}$ với $\displaystyle k$ là công bội và theo kết quả ở trên thì 
$$
\begin{gather*}
\sum _{s\in S} s=\sum _{i=0}^{d-1}( a+ik) =da+\frac{d( d-1)}{2} k\equiv 0(\bmod p)\\
\sum _{s\in S} s^{2} =\sum _{i=0}^{d-1}( a+ik)^{2} =da^{2} +d( d-1) ak+\frac{d( d-1)( 2d-1)}{6} k^{2} \equiv 0(\bmod p)
\end{gather*}
$$

suy ra 
$$
\begin{equation*}
a+\frac{d-1}{2} k=a^{2} +( d-1) ak+\frac{( d-1)( 2d-1)}{6} k^{2} =0
\end{equation*}
$$
thay $\displaystyle a=-\frac{d-1}{2} k$ trở lại thì ta có 
$$
\begin{gather*}
k^{2}\left(\frac{( d-1)^{2}}{4} -\frac{( d-1)^{2}}{2} +\frac{( d-1)( 2d-1)}{6}\right) =0\\
\Longrightarrow \frac{d-1}{4} -\frac{d-1}{2} +\frac{2d-1}{6} =0\\
\Longrightarrow d=-1
\end{gather*}
$$
là điều mâu thuẫn. Vậy không tồn tại tập $\displaystyle S$ thỏa mãn yêu cầu bài toán.
