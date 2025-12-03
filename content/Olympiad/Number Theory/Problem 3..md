**Đề bài** Với mỗi số nguyên dương $\displaystyle n$, định nghĩa $\displaystyle V_{n} =\left\lfloor 2^{n}\sqrt{2020}\right\rfloor +\left\lfloor 2^{n}\sqrt{2021}\right\rfloor$. Chứng minh rằng dãy $\displaystyle ( V_{n})_{n\geqslant 1}$ chứa vô hạn số hạng chẵn, cũng như là số hạng lẻ. 
*Lời giải.*
Bản chất của bài này là gì? Vì sao lại có ký hiệu cồng kềnh và phức tạp như thế. Trước hết ta đi đào sâu vào một số vấn đề đã bị bỏ quên như sau : Bất cứ số hữu tỉ nào cũng đều có dạng biểu diễn thập phân hoặc là hữu hạn hoặc là vô hạn tuần hoàn. Một số vô tỉ thì phần biểu diễn thập phân của nó không tuần hoàn hoặc đơn giản hơn là không có bất cứ một quy tắc xác định cụ thể nào hết. Ở trong bài này ta sẽ sử dụng quan sát trên để xử lí.

Bây giờ, gọi biểu diễn dạng nhị phân của hai số $\displaystyle \sqrt{2020}$ và $\displaystyle \sqrt{2021}$ lần lượt là $\displaystyle \overline{...a_{0} ,a_{1} a_{2} ...}$ và $\displaystyle \overline{...b_{0} ,b_{1} b_{2} ...}$. Khi nhân thêm $\displaystyle 2^{n}$ vào $\displaystyle \sqrt{2021} ,\sqrt{2021}$ thì dấu phẩy trong biểu diễn nhị phân sẽ dịch dần sang bên phải nên về mặt bản chất các chữ số vẫn không thay đổi. Để xử lí bài toán ta sẽ giả sử phản chứng.

i/ Nếu như chỉ có hữu hạn số lẻ thì đến một lúc nào đó, các chữ số trong biểu diễn nhị phân của hai số trên sẽ thỏa mãn $\displaystyle a_{i} =b_{i} ,\forall i\geqslant N$ vì khi đó $\displaystyle V_{i}$ sẽ chẵn nên khi lấy phần nguyên ta sẽ được tổng 2 số có đuôi bằng nhau trong biểu diễn nhị phân. 2 số có đuôi bằng nhau thì tổng của chúng cộng lại mới là một số chẵn được. Đại loại ta có biểu diễn 
$$
\begin{equation*}
\overline{...a_{i}}_{2} +\overline{...b_{i}}_{2} =\overline{....( 2a_{i})}_{2} =\overline{....0}_{2}
\end{equation*}
$$

tất cả được lấy trong cơ số 2. 

Do đó hiệu $\displaystyle \sqrt{2020} -\sqrt{2021}$ phải là một số hữu tỉ vì các chữ số kể từ $\displaystyle i\geqslant N$ trong biểu diễn nhị phân của chúng được xác định như nhau nên hiệu của chúng sẽ là một số thập phân với các chữ số đã được xác định, tức bản thân nó chính là một số hữu tỉ. Nhưng đây là điều vô lí từ chuỗi biến đổi như sau 

$$
\begin{gather*}
\sqrt{2020} -\sqrt{2021} \in \mathbb{Q}\\
\leftrightarrow 2020+2021-2\sqrt{2020}\sqrt{2021} \in \mathbb{Q}\\
\leftrightarrow \sqrt{2020.2021} \in \mathbb{Q}\\
\leftrightarrow 2020.2021=x^{2}
\end{gather*}
$$

là sai vì $\displaystyle 2020,2021$ nguyên tố cùng nhau

ii/ Nếu như chỉ có hữu hạn số chẵn, thì dãy sẽ toàn là số lẻ kể từ 1 lúc nào đó. Ta lập luận tương tự như trên thì suy ra chỉ số đuôi của 2 số $\displaystyle \left\lfloor 2^{n}\sqrt{2020}\right\rfloor ,\left\lfloor 2^{n}\sqrt{2021}\right\rfloor$ phải thỏa mãn $\displaystyle a_{i} +b_{i} =1$. Và tương tự thì tổng $\displaystyle \sqrt{2020} +\sqrt{2021}$ cũng hữu tỉ như ta đã nhận xét ở trên. Đây cũng là điều mâu thuẫn. 

Từ 2 trường hợp ta suy ra điều phải chứng minh. 

Bài toán cũng có thể được tổng quát thành cặp $\displaystyle \sqrt{a} \pm \sqrt{b}\not{\in }\mathbb{Q}$.
