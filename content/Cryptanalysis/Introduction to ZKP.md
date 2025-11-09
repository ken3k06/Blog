## Mở đầu
Chứng minh không lộ thông tin hay thuật ngữ tiếng anh của nó là Zero-Knowledge Proof được phát minh bởi [Goldwasser, Micali và Rackoff](https://people.csail.mit.edu/silvio/Selected%20Scientific%20Papers/Proof%20Systems/The_Knowledge_Complexity_Of_Interactive_Proof_Systems.pdf) vào năm 1981 (viết tắt là GMR). Khái niệm "chứng minh không lộ thông tin" ban đầu xuất phát từ việc nghiên cứu các sơ đồ xưng danh, về sau đã được mở rộng cho nhiều loại bài toán khác nhau. 

Giả sử $P$ và $V$ cùng tham gia một trò chơi với các quân bài. $P$ đưa ra hai quân bài úp và nói cho $V$ biết đó là "át" và "2". $P$ sau đó yêu cầu $V$ chọn quân "át". 
Trước khi chọn quân "át", $V$ muốn kiểm tra chắc chắn rằng hai quân bài đó đích thực là "át" và "2". $V$ yêu cầu $P$ chứng minh điều này. Nếu $P$ lật hai quân bài đó lên coi như là một cách chứng minh, thì trò chơi kết thúc, vì $V$ đã nhìn thấy chúng và dĩ nhiên là anh ta có thể chọn ngay ra được quân bài "át".
Có một cách khác để $P$ chứng minh rằng hai quân bài đó là "át" và "2" mà không phải lật hai quân bài đó lên, tức là không làm lộ thông tin về hai quân bài trên tay $P$. Đó là $P$ sẽ đưa 50 quân bài còn lại cho $V$. Nếu như $V$ kiểm tra thấy thiếu một quân bài "át" và một quân bài "2", thì có thể xem hai quân bài trên tay $P$ có đúng như những gì anh ta nói. 

Tóm lại ta có 2 vai trò ở đây.
Vai trò đầu tiên là Prover - Người chứng minh. Người này sẽ biết bí mật cần chứng minh. Người này sẽ cố gắng thuyết phục Verifier rằng họ biết bí mật đó mà không làm tiết lộ bí mật ra bên ngoài. Verifier sẽ cố gắng xác nhận rằng Prover có được bí mật mà không phải chỉ đoán mò hay gian lận. Verifier cũng không được biết gì thêm ngoài sự thật rằng Prover đang nắm giữ bí mật thật. 

![[Pasted image 20251031193305.png]]
Nói chung, chứng minh không để lộ thông tin - ZKP, không có nghĩa là không để lộ thông tin mà là để lộ thông tin ở mức ít nhất về sự vật, sự việc cần chứng minh. 
Người ta đặc biệt quan tâm đến hai hệ thống Sơ đồ ZKP đó là hệ thống chứng minh không lộ thông tin cho tính đẳng cấu của đồ thị 
![[Pasted image 20251031193529.png]]



và hệ thống chứng minh không lộ thông tin cho bài toán thặng dư bậc hai. 

![[Pasted image 20251031193616.png]]




Các bài toán mà ta sẽ tìm kiếm cho chúng những "chứng minh không lộ thông tin" thường là những bài toán quyết định, đó là những bài toán được xác định bởi một tập dữ liệu $\Sigma$ và một tính chất $\Pi$, và nội dung của bài toán là xét xem với mỗi $x \in \Sigma$, $x$ có tính chất $\Pi$ hay không. Một số lớp các bài toán quyết định như vậy đã được xem xét đến khi ta nghiên cứu về độ phức tạp tính toán. Tham gia vào một giao thức chứng minh gồm có hai người: một là người chứng minh $P$ và một là người kiểm thử $V$. Giao thức gồm các câu hỏi - đáp giữa $V$ và $P$, thường là $V$ đưa ra các câu hỏi hay thách đố và $P$ đưa ra các câu trả lời.  Giả sử $P$ biết chắc chắn rằng $x$ có tính chất $\Pi$, $P$ có thể dùng một giao thức chứng minh để thuyết phục $V$ tin rằng $x$ có tính chất $\Pi$ và giao thức chỉ được dùng để thuyết phục $V$ chứ không để lộ thêm bất cứ thông tin nào khác. 

Một số ứng dụng của ZKP đó là bỏ phiếu điện tử và giao dịch tiền điện tử. Trong quá trình giải quyết các bài toán này có sử dụng thuật toán sinh số nguyên tố lớn để thực hiện các bước kiểm chứng thông tin.

## Efficiently Verifiable Proofs
![[Pasted image 20251031194714.png]]
**Định nghĩa.** Cho $L$ là một ngôn ngữ trên bảng chữ $\Sigma$. Ta nói rằng ngôn ngữ $L$ là kiểm chứng được trong thời gian đa thức (Polynomial Time) hay đơn giản là kiểm chứng được nhanh, nếu tồn tại một máy Turing tất định thời gian đa thức $V$ và một tập $C$ nào đó sao cho, đối với mọi từ $w \in \Sigma^{*}$,
$$
w \in L \leftrightarrow  \exists c \in C : V \ accept \ \langle w,c\rangle
$$
và hơn nữa, máy $V$ chấp nhận $\langle w,c \rangle$ trong thời gian đa thức chỉ theo độ dài của từ $w$. Khi ấy, $V$ được gọi là máy kiểm chứng thời gian đa thức đối với ngôn ngữ $L$, mỗi phần tử của tập $C$ được gọi là chứng cứ (certificate), còn chứng cứ $c \in C$ mà theo đó $V$ chấp nhận $\langle w,c \rangle$ được gọi là bằng chứng (proof) để khẳng định $w$ là thành viên của $L$. 
![[Pasted image 20251031195947.png]]

Ở trên là định nghĩa của non-interactive proof tức là chứng minh không tương tác. Prover chỉ gửi một chứng cứ duy nhất cho Verifier và Verifier sẽ dùng nó để kiểm tra. 

Tiếp theo ta có interactive proof. Thì ngược lại với non-interactive proof, ở đây 2 người $V$ và $P$ liên tục tương tác bằng cách gửi thông tin qua lại cho nhau. 



![[Pasted image 20251031200615.png]]

Một interactive proof system là một quá trình tương tác giữa hai người $P$ và $V$ mà trong đó: 
- $P$ nó năng lực tính toán rất mạnh (unbounded)
- $V$ bị giới hạn tính toán đa thức theo độ dài của input 
Khi bắt đầu giao thức, cả $P$ và $V$ đều được cung cấp một thực thể đầu vào $x$. Giao thức diễn ra thông qua việc $V$ đặt câu hỏi và $P$ trả lời. 
Ta nói rằng $\langle P,V \rangle$ là hệ thống xác thực tương tác cho ngôn ngữ $L$ nếu như nó thỏa mãn hai tính chất sau
- Completeness: Với mọi $x \in L$ thì 

$$
\Pr[\langle P,V\rangle(x)=1] = 1-\epsilon
$$
- Soundness: Với mọi $x \notin L$ 

$$
\Pr[\langle P,V\rangle(x)=1]  = \epsilon
$$

Ở một số tài liệu, người ta quy ước như sau:
![[Pasted image 20251031203158.png]]



![[Pasted image 20251031201746.png]]


## Tài liệu
1. https://people.csail.mit.edu/silvio/Selected%20Scientific%20Papers/Proof%20Systems/The_Knowledge_Complexity_Of_Interactive_Proof_Systems.pdf
2. https://rdi.berkeley.edu/zk-learning/ (Tài liệu chính)
3. https://zkplabs.network/blog
4. https://zkhack.dev/whiteboard/
5. https://jbootle.github.io/Misc/fosad2015.pdf
6. https://crypto.stanford.edu/cs355/19sp/lec3.pdf
7. 
