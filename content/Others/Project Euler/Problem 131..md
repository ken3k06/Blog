![[Pasted image 20250922201032.png]]

Tóm tắt đề bài: Xét một số nguyên tố $\displaystyle p$ sao cho tồn tại số nguyên dương $\displaystyle n$ thỏa mãn $\displaystyle n^{3} +n^{2} p$ là một số lập phương đúng. Ví dụ ta có $\displaystyle p=19$ thì tồn tại $\displaystyle n=8$ thỏa mãn $\displaystyle 8^{3} +8^{2} \times 19=12^{3}$. Ta cần đếm xem có bao nhiêu số nguyên tố $\displaystyle p\leqslant 1000000$ thỏa mãn tính chất trên. 

Giải thuật:Viết lại phương trình nghiệm nguyên dưới dạng 

$$
\begin{equation*}
k^{3} =n^{2}( n+p)
\end{equation*}
$$

Nếu như $\displaystyle \gcd( n,p) =p$ thì đặt $\displaystyle n=n_{1} p^{\alpha }$ trong đó $\displaystyle \gcd( n_{1} ,p) =1$ còn $\displaystyle \alpha =v_{p}( n)$. Như vậy vì $\displaystyle k^{3} \vdots n^{2} \vdots p$ cho nên ta cũng có $\displaystyle k=k_{1} p^{\beta }$ với định nghĩa các giá trị tương tự với $\displaystyle n$. Khi đó ta viết lại phương trình nghiệm nguyên ban đầu dưới dạng 

$$
\begin{equation*}
k_{1}^{3} p^{3\beta } =n_{1}^{2} p^{2\alpha }\left( n_{1} p^{\alpha } +p\right)
\end{equation*}
$$

Nếu $\displaystyle \beta  >\alpha$ thì khi đó $\displaystyle 3\beta  >2\alpha +1$ cho nên ta có điều vô lí. Tiếp tục ta có nếu như $\displaystyle \alpha  >\beta \geqslant 1$. Từ định giá p-adic ta lại có $\displaystyle 3\beta =2\alpha +1$ và khi ta hạ các lũy thừa của $\displaystyle p$ xuống ta sẽ được một phương trình mới là 

$$
\begin{equation*}
k_{1}^{3} =n_{1}^{3} p^{\alpha -1} +n_{1}^{2}
\end{equation*}
$$

Ta có $\displaystyle 3\beta =2\alpha +1$ cho nên $\displaystyle \alpha \equiv 1\bmod 3$ cho nên $\displaystyle \alpha -1=3t$ và 

$$
\begin{equation*}
k_{1}^{3} =n_{1}^{3} p^{3t} +n_{1}^{2} =\left( n_{1} p^{t}\right)^{3} +n_{1}^{2}
\end{equation*}
$$

Nhưng mặt khác ta có $\displaystyle k^{3} \vdots n^{2}$ cho nên giữa $\displaystyle k_{1}$ và $\displaystyle n_{1}$ tồn tại một ước nguyên tố $\displaystyle q$ khác $\displaystyle p$. Ta có thể xét trường hợp $\displaystyle k,n$ là lũy thừa của $\displaystyle p$ và trường hợp này dẫn tới vô lí. Khi đó xét ước nguyên tố $\displaystyle q$ đó và ta sẽ kiểm tra $\displaystyle \alpha =\min( v_{q}( k) ,v_{q}( n))$. Thực chất ta không cần quan tâm tới số mũ của $\displaystyle p$ miễn là $\displaystyle \alpha -1 >0$ là được. 


Ta viết lại phương trình dưới dạng $\displaystyle n^{3} +n^{2} p=k^{3}$. Khi đó rõ ràng $\displaystyle ( k,n) \neq 1$. Ta xét một ước nguyên tố $\displaystyle q^{\alpha } \| \gcd( k,n)$ trong đó $\displaystyle q^{\alpha } =\min\{v_{q}( k) ,v_{q}( n)\}$. Đầu tiên ta giả sử $\displaystyle v_{q}( n) =\alpha$ còn $\displaystyle v_{q}( k) =\beta$ và $\displaystyle \beta  >\alpha$. Khi đó viết lại phương trình trên dưới dạng 

$$
\begin{equation*}
n_{1}^{3} q^{3\alpha } +n_{1}^{2} q^{2\alpha } p=k_{1}^{3} q^{3\beta }
\end{equation*} 
$$

Do $\displaystyle \beta  >\alpha$ cho nên $\displaystyle 3\beta  >2\alpha$ dẫn tới 

$$
\begin{equation*}
n_{1}^{3} q^{\alpha } +n_{1}^{2} p=k_{1}^{3} q^{3\beta -2\alpha }
\end{equation*}
$$

Suy ra $\displaystyle p=q$ vì $\displaystyle \gcd( n_{1} ,q) =1$. 
Tiếp tục xét $\displaystyle v_{q}( k) =\alpha$ và ngược lại $\displaystyle v_{q}( n) =\beta  >\alpha$. Ta cũng viết lại phương trình dưới dạng 

$$
\begin{equation*}
n_{1}^{3} q^{3\beta } +n_{1}^{2} q^{2\beta } p=k_{1}^{3} q^{3\alpha }
\end{equation*}
$$

Nếu như $\displaystyle 3\alpha  >2\beta$ thì ta có 

$$
\begin{equation*}
n_{1}^{3} q^{\beta } +n_{1}^{2} p=k_{1}^{3} q^{3\alpha -2\beta }
\end{equation*}
$$

Suy ra $\displaystyle p=q$. Tiếp tục nếu như $\displaystyle 2\beta  >3\alpha$ thì ta có 

$$
\begin{equation*}
n_{1}^{3} q^{3\beta -3\alpha } +n_{1}^{2} q^{2\beta -3\alpha } p=k_{1}^{3}
\end{equation*}
$$

Nhưng $\displaystyle ( k_{1} ,q) =1$ cho nên ta có điều vô lí. 
Như vậy trường hợp này ta loại. 

Tiếp theo ta xét $\displaystyle \gcd( n,p) =1$ thì khi đó $\displaystyle n^{2}$ và $\displaystyle n+p$ đều là các số lập phương đúng. Suy ra $\displaystyle n$ cũng là số lập phương đúng vì $\displaystyle n^{2}$ là số lập phương đúng. Điều này dẫn tới $\displaystyle p=a^{3} -b^{3}$ là hiệu của hai số lập phương đúng. Nhưng $\displaystyle p$ là số nguyên tố cho nên $\displaystyle a-b=1$ và đưa về $\displaystyle p=( a+1)^{3} -a^{3} =3a^{2} +3a+1$. Như vậy ta chỉ cần check xem các số có dạng $\displaystyle 3a^{2} +3a+1\leqslant 1000000$ có phải là số nguyên tố không. Giải bất đẳng thức ta được $\displaystyle a\leqslant 577$. Như vậy số không lớn lắm và ta có thể bruteforce trực tiếp. 

```python
import sympy
import math 

def project_euler_131(limit):
  valid_p=[]
  for i in range(577):
    cube=3*i**2+3*i+1
    if cube>limit:
      break
    elif sympy.isprime(cube):
      valid_p.append(cube)
  return len(valid_p)
limit=10**6
project_euler_131(limit)
```