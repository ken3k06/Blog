## Sage 
[1] https://doc.sagemath.org/html/en/reference/cryptography/sage/crypto/lattice.html
## Trapdoor functions
Về cơ bản các trapdoor functions là các hàm dễ triển khai nhưng khó đảo ngược lại. Các trapdoor functions đóng vai trò nền tảng trong việc xây dựng lược đồ mã hóa. Chẳng hạn trong RSA ta có một trapdoors function là $f_{N,e}(x)=x^e \bmod N$ . 
Mỗi trapdoor functions sẽ được tạo ra kèm theo một số thông tin giúp việc đảo ngược trở nên dễ dàng hơn. Trong trường hợp mã hóa RSA thì thông tin đó sẽ là $d \equiv e^{-1} \bmod \phi(N)$. 


