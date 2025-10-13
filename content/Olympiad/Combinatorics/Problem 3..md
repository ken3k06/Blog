**Đề bài.** Sắp xếp 9 học sinh đứng cách đều nhau trên một vòng tròn tại vị trí 9 đỉnh của một đa giác đều. Chứng minh rằng tồn tại hai tam giác có đỉnh là các đỉnh của đa giác đều và bằng nhau ( các đỉnh của hai tam giác có thể trùng nhau nhưng hai tam giác là phân biệt ) mà tất cả các học sinh đứng ở các đỉnh của hai tam giác đó là cùng giới. 

Giả thiết rằng mỗi em học sinh trong 9 em học sinh này chỉ thuộc một trong 2 giới là nam và nữ.(no LGBT bro)

*Lời giải.*
Gọi 9 đỉnh của đa giác đều đó lần lượt là $\displaystyle h_{1} ,h_{2} ,...,h_{9}$. Thì theo nguyên lí Dirichlet sẽ có ít nhất là $\displaystyle \left\lfloor \frac{9}{2}\right\rfloor +1=5$ đỉnh mà tại đó các học sinh có cùng một giới tính. Giả sử 5 đỉnh đó lần lượt là $\displaystyle h_{1} ,h_{2} ,h_{3} ,h_{4} ,h_{5}$. Bây giờ ta cần chứng minh rằng trong mọi trường hợp các vị trí của 5 đỉnh trên thì ta luôn có thể chọn ra 2 tam giác bằng nhau. 

9 điểm cách đều nhau đứng trên 1 vòng tròn và ta chọn ra 5 đỉnh bất kì. Nếu như ta chọn 5 đỉnh $\displaystyle h_{1} ,h_{2} ,h_{3} ,h_{4} ,h_{5}$ mà độ dài các cung tạo ra bởi 2 đỉnh liền kề trong 5 đỉnh này phân biệt nhau thì ta có điều vô lí vì lúc này tổng số đo 5 cung sẽ lớn hơn $\displaystyle 1+2+3+4 >9$. Do đó phải có ít nhất 2 cung kề nhau tạo bởi 5 đỉnh này có độ dài bằng nhau. 

Thế thì bài toán chuyển về cấu hình đơn giản hơn : Gọi $\displaystyle H_{12}$ là độ dài cung tạo bởi $\displaystyle h_{1}$ và $\displaystyle h_{2}$. Tương tự như vậy ta gọi $\displaystyle H_{i( i+1)}$ là độ dài cung tạo bởi hai đỉnh $\displaystyle h_{i} ,h_{i+1}$ với giả sử rằng $\displaystyle h_{1} ,h_{2} ,h_{3} ,h_{4} ,h_{5}$ được xếp theo thứ tự như vậy trên đường tròn và không có hai đỉnh nào trùng nhau. Có ít nhất hai cung có độ dài bằng nhau nên ta xét lần lượt các trường hợp cho độ dài của 2 cung đó

*Trường hợp 1*. Có hai cung có độ dài là 3 thì 3 cung còn lại có độ dài sẽ là 1. 

Giả sử $\displaystyle H_{12} =H_{23} =H_{34} =1$ và $\displaystyle H_{45} =H_{51} =3$ thì ta chọn hai tam giác $\displaystyle h_{1} h_{2} h_{5}$ và $\displaystyle h_{3} h_{4} h_{5}$ thì hai tam giác này bằng nhau và bài toán hoàn tất.

*Trường hợp 2.* Có 2 cung có độ dài là 2. Thì tổng độ dài 3 cung còn lại sẽ là 5.

Bây giờ xét $\displaystyle H_{12} =H_{23} =2$. Còn trong 3 cung còn lại vì tổng là 5 nên sẽ có ít nhất 2 cung có độ dài bằng nhau nữa. Do nếu tất cả đều phân biệt thì sẽ có tổng độ dài là $\displaystyle 1+2+3 >5$. 

Nếu như là trường hợp $\displaystyle ( 2,2,1)$ thì luôn có 3 cung độ dài là 2 xếp kề nhau và sẽ tạo thành 2 tam giác mà ta mong muốn

Nếu như là trường hợp $\displaystyle ( 3,1,1)$ thì bằng cách vẽ trực tiếp ra ta sẽ có được luôn tồn tại 2 tam giác bằng nhau. 

Thật vậy, ta xét nếu như thứ tự các cung là $\displaystyle 2-2-1-1-3$ thì sẽ tạo thành hình thang cân tại $\displaystyle h_{1} h_{2} h_{4} h_{5}$.

Còn nếu như thứ tự các cung là $\displaystyle 2-2-1-3-1$ thì ta có ngay điều phải chứng minh vì tạo thành hình thang cân tại $\displaystyle h_{1} h_{3} h_{4} h_{5}$.

*Trường hợp 3.* Có 2 cung có độ dài là 1. Nếu như có 2 cung có độ dài là 1 thì tổng số đo các cung còn lại sẽ là 7.

Nếu nhu có 3 cung có độ dài là 1 thì có điều phải chứng minh vì 3 cung này phải được tạo thành từ ít nhất 4 đỉnh thì ta có ngay được 1 hình thang cân từ ít nhất 4 đỉnh.

Nếu như có 2 cung độ dài 1 và 1 cung độ dài là 2 thì 2 cung còn lại chỉ có thể rơi vào 2,3 hoặc 3,2 do đó quy lại về trường hợp ở trên

Nếu như có 2 cung độ dài 1 và 1 cung độ dài 3 thì cũng tương tự như vừa rồi

Nếu như có 2 cung độ dài 1 và 1 cung độ dài là 4 thì 2 cung còn lại có tổng là 3 và lại rơi vào trường hợp có 3 cung có độ dài là 1. 

Vậy ta đã xét qua tất cả các trường hợp có thể có.

Suy ra bài toán hoàn tất và ta có điều phải chứng minh.

[[Olympiad/Combinatorics/Problem 4.|Problem 4.]]
