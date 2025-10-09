**Bài 2.** Với mỗi số nguyên dương $\displaystyle c$, kí hiệu $\displaystyle p( c)$ là ước nguyên tố lớn nhất của $\displaystyle c$. Xét dãy số nguyên dương $\displaystyle ( a_{n})$ xác định bởi $\displaystyle a_{1}  >1,a_{n+1} =a_{n} +p( a_{n}) ,\forall n\geqslant 1$. Chứng minh rằng tồn tại ít nhất một số chính phương thuộc dãy. 
*Lời giải.*
Ý tưởng để giải quyết bài toán này là gì? Ta hãy cùng liệt kê một số cách tiếp cận khả thi: Trước hết yêu cầu của bài toán là chứng minh tồn tại ít nhất một số chính phương thuộc dãy. Điều này có nghĩa là sao? Ta có hai hướng để tiếp cận bài toán. Hướng đi đầu tiên là tìm một dạng cụ thể cho $\displaystyle a_{n}$. Nhưng điều này thực sự rất khó vì ta không xác định được rõ cấu trúc của $\displaystyle p( a_{n})$, chưa kể, các số nguyên tố có thể thay phiên nhau thay đổi tùy ý nên không thể đi theo hướng như thế này được. 
Hướng tấn công thứ hai mà ta có thể xây dựng đó chính là sử dụng liên tục rời rạc. Giống như bài toán chứng minh có vô số số Square-free. Tức là một số $\displaystyle a_{n}$ sẽ được tách làm 2 phần, phần đầu tiên là $\displaystyle p( a_{n})$ và phần còn lại sẽ là $\displaystyle \frac{a_{n}}{p( a_{n})}$. Cái ta cần làm là khảo sát lượng $\displaystyle \frac{a_{n}}{p( a_{n})}$ để xem có gì đặc biệt hay không. Ta cần có $\displaystyle p( a_{n}) =\frac{a_{n}}{p( a_{n})}$. Nhưng điều này liệu có xảy ra không, và nếu xảy ra thì cần điều kiện gì. Giả sử một số $\displaystyle a_{n}$ có dạng $\displaystyle a_{n} =p\frac{a_{n}}{p}$ chẳng hạn. Thì trong $\displaystyle \frac{a_{n}}{p}$ có gì đặc biệt không. Đó là những câu hỏi mà ta cần phải hỏi khi làm bài này. 


Ta đặt $\displaystyle a_{n} =r^{\alpha }\prod _{i=1}^{l} q_{i}^{\beta _{i}}$ trong đó $\displaystyle r=p( a_{n})$. Bây giờ xét 
$$
\begin{equation*}
a_{n+1} =a_{n} +p( a_{n}) =r+r^{\alpha }\prod _{i=1}^{l} q_{i}^{\beta _{i}} =r\left( 1+r^{\alpha -1}\prod _{i=1}^{l} q_{i}^{\beta _{i}}\right)
\end{equation*}
$$
và trong đó $\displaystyle a_{n+1} =p( a_{n+1})\frac{a_{n+1}}{p( a_{n+1})}$và từ phân tích ở trên ta suy ra $\displaystyle p( a_{n+1}) =\max\left\{r,p\left( 1+r^{\alpha -1}\prod _{i=1}^{l} q_{i}^{\beta _{i}}\right)\right\}$

Nếu như $\displaystyle \alpha  >1$ thì $\displaystyle 1+r^{\alpha -1}\prod _{i=1}^{l} q_{i}^{\beta _{i}}$ nguyên tố cùng nhau với tất cả các số nguyên tố $\displaystyle r,q_{i}$ cho nên nó có một ước nguyên tố lớn hơn $\displaystyle r$ và suy ra được $\displaystyle p( a_{n+1})  >p( a_{n})$. Ngược lại nếu như $\displaystyle \alpha =1$ thì ta có $\displaystyle 1+\prod _{i=1}^{l} q_{i}^{\beta _{i}}$ nguyên tố cùng nhau với tất cả các số nguyên tố $\displaystyle q_{i}$ cho nên nó cũng có một ước nguyên tố khác với các số $\displaystyle q_{i}$. Điều này dẫn tới $\displaystyle p( a_{n+1}) \geqslant p( a_{n})$. Từ đây suy ra $\displaystyle p( a_{n+1}) \geqslant p( a_{n})$ và dãy $\displaystyle \{p( a_{n})\}$ không giảm. Suy ra 
$$
\begin{gather*}
p( a_{n+1})\frac{a_{n+1}}{p( a_{n+1})} =p( a_{n})\left(\frac{a_{n}}{p( a_{n})} +1\right)\\
\leftrightarrow \frac{p( a_{n+1})}{p( a_{n})} =\frac{\frac{a_{n}}{p( a_{n})} +1}{\frac{a_{n+1}}{p( a_{n+1})}} \geqslant 1\\
\leftrightarrow \frac{a_{n}}{p( a_{n})} +1\geqslant \frac{a_{n+1}}{p( a_{n+1})}
\end{gather*}
$$

Nếu như có một chỉ số $\displaystyle n$ để $\displaystyle p( a_{n})  >\frac{a_{n}}{p( a_{n})}$ thì số $\displaystyle a_{n}$ có dạng $\displaystyle pk$ với $\displaystyle k=\frac{a_{n}}{p( a_{n})}$. Ta xét 
$$
\begin{equation*}
a_{n+1} =a_{n} +p( a_{n}) =pk+p=p( k+1)
\end{equation*}
$$
trong đó $\displaystyle k+1< p$ và nguyên tố cùng nhau với $\displaystyle p$ nên nó không thể có ước nguyên tố nào lớn hơn $\displaystyle p$. Ta tiếp tục quá trình trên thì tạo ra được dãy 
$$
\begin{equation*}
p( k+1) ,p( k+2) ,...,p^{2}
\end{equation*}
$$
và do đó tồn tại một số chính phương.

Nếu như ngược lại như trên thì ta có với mọi $\displaystyle n$ đẳng thức sau sẽ xảy ra : $\displaystyle p( a_{n}) \leqslant \frac{a_{n}}{p( a_{n})}$

Giả sử $\displaystyle \{p( a_{n})\}$ bị chặn thì do $\displaystyle p( a_{n})$ là dãy không giảm nên nó sẽ hằng từ 1 lúc nào đó trở đi. Từ đây suy ra ta có 
$$
\begin{equation*}
\frac{a_{n}}{p( a_{n})} +1=\frac{a_{n+1}}{p( a_{n+1})}
\end{equation*}
$$

kể từ 1 lúc nào đó. Và tiếp tục cộng dồn để tạo ra một số nguyên tố mới là $\displaystyle \frac{a_{n+M}}{p( a_{n+M})} =\frac{a_{n}}{p( a_{n})} +M >p( a_{n+M}) =p( a_{n})$ là điều vô lí. Vậy $\displaystyle \{p( a_{n})\}$ có thể lớn tùy ý và do đó $\displaystyle \left\{\frac{a_{n}}{p( a_{n})}\right\}$ cũng vậy. Từ đánh giá $\displaystyle \frac{a_{n}}{p( a_{n})} +1\geqslant \frac{a_{n+1}}{p( a_{n+1})}$ ta suy ra dãy $\displaystyle \frac{a_{n}}{p( a_{n})}$ có thể nhận giá trị tùy ý đủ lớn. Thật vậy, xét $\displaystyle n$ là chỉ số đầu tiên để $\displaystyle \frac{a_{n}}{p( a_{n})} \geqslant q$ trong đó $\displaystyle q$ là một số nguyên tố thì 
$$
\begin{equation*}
1\leqslant q-\frac{a_{n-1}}{p( a_{n-1})} \leqslant \frac{a_{n}}{p( a_{n})} -\frac{a_{n-1}}{p( a_{n-1})} \leqslant 1
\end{equation*}
$$
vì $\displaystyle \frac{a_{n-1}}{p( a_{n-1})} \leqslant q-1$ do đó dầu bằng xảy ra và $\displaystyle \frac{a_{n}}{p( a_{n})} =q$. Vậy $\displaystyle a_{n} =pq$ trong đó $\displaystyle p< q$ và lặp lại quá trình như trên ta cũng có được dãy 
$$
\begin{equation*}
pq,( p+1) q,...,q^{2}
\end{equation*}
$$và dãy lại sinh ra một số chính phương mới. Suy ra ta có điều phải chứng minh. 