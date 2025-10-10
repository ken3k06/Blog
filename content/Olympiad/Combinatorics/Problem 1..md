
**Đề bài.** Cho tập $\displaystyle S=\{1,2,...,3n\}$, phân hoạch tập $\displaystyle S=A\cup B\cup C$ sao cho $\displaystyle A,B,C$ đôi một rời nhau và $\displaystyle |A|=|B|=|C|=n$. Chứng minh rằng tồn tại 3 phần tử $\displaystyle a\in A,b\in B,c\in C$ thỏa mãn số này bằng tổng của hai số còn lại. 

*Lời giải.*

Yêu cầu bài toán tương đương với việc chứng minh rằng, tồn tại 3 số $\displaystyle a\in A,b\in B,c\in C$ để cho $\displaystyle ( a+b-c)( a+c-b)( b+c-a) =0$. Giả sử phản chứng, ta luôn có $\displaystyle ( a+b-c)( a+c-b)( b+c-a) \neq 0$ với mọi $\displaystyle a\in A,b\in B,c\in C$. Ta sẽ chứng minh điều giả sử ở trên là vô lí.

Bây giờ xét $\displaystyle S=\{1,...,n\} \cup \{n+1,...,2n\} \cup \{2n+1,...,3n\}$. Không mất tính tổng quát, ta giả sử $\displaystyle 1\in A$, và gọi $\displaystyle k\in S$ là số sao cho $\displaystyle 1,2,...,k-1\in A$ nhưng $\displaystyle k\notin A$. Ta xét $\displaystyle k\in B$. Với $\displaystyle k >2$ thì $\displaystyle k-1\geqslant 2$ cho nên $\displaystyle 2\in A$. Còn nếu $\displaystyle k=2$ thì $\displaystyle 2\in B$. Suy ra trong mọi trường hợp ta có $\displaystyle 2\notin C$. Vai trò của $\displaystyle B,C$ như nhau nên ta có thể giả sử $\displaystyle k\in B$ và suy ra $\displaystyle 2\notin C$. 

Tiếp tục, ta sẽ khảo sát các số thuộc $\displaystyle C$ và từ đó xác định cấu trúc của tập $\displaystyle C$ xem có gì đặc biệt hay không. Cụ thể xét $\displaystyle x\in C$. Ta có $\displaystyle 1\in A$, vậy thì các số $\displaystyle x-1,x+1$ sẽ thuộc về những tập hợp nào. Nếu $\displaystyle x-1\in B$ thì ta có ngay điều vô lí. Do đó $\displaystyle x-1\in A$ hoặc $\displaystyle x-1\in C$. Tương tự với $\displaystyle x+1$ thì $\displaystyle x+1\notin B$ kéo theo $\displaystyle x+1\in A$ hoặc $\displaystyle x+1\in C$. 

Ta xét $\displaystyle x-1\in C$ trước. Bây giờ nếu như $\displaystyle x-1\in C$ thì do $\displaystyle 2\notin C$ cho nên $\displaystyle x-1\neq 1,\forall x\in C$. Tiếp theo ta xét:

+ Nếu $\displaystyle k=2$ và $\displaystyle 2\in B$ thì $\displaystyle 2+x-1=x+1$. Nếu như $\displaystyle x+1\in A$ thì vô lí. Dẫn tới $\displaystyle x+1\in B$ hoặc $\displaystyle x+1\in C$. Nhưng ta có $\displaystyle x+1\notin B$ như nhận xét ở trên cho nên $\displaystyle x+1\in C$. Vậy $\displaystyle x-1\in C$ thì kéo theo $\displaystyle x+1\in C$. 

Tiếp tục, $\displaystyle x+1\in C$ thì với $\displaystyle 1\in A$ ta có $\displaystyle x+2\in B$ dẫn tới vô lí cho nên $\displaystyle x+2\in A$ hoặc $\displaystyle x+2\in C$. Nếu như $\displaystyle x+2\in A$ thì chọn $\displaystyle 2\in B,x+2\in A$ và $\displaystyle x\in C$ có ngay điều vô lí. Vậy $\displaystyle x+2\in C$. 

Với $\displaystyle x+2\in C$. Tiếp tục xét $\displaystyle x+3\in B$ thì có điều vô lí nên $\displaystyle x+3\in A$ hoặc $\displaystyle x+3\in C$ như nhận xét ở trên. Nếu $\displaystyle x+3\in A$ thì chọn $\displaystyle x+3\in A,2\in B,x+1\in C$ ta cũng có điều vô lí. Vậy $\displaystyle x+3\in C$. Cứ tiếp tục như vậy, ta làm tương tự với $\displaystyle x+3\in C$ thì $\displaystyle x+4\in A$ hoặc $\displaystyle x+4\in C$. Nếu $\displaystyle x+4\in A$ thì chọn $\displaystyle x+2\in C,2\in B$ cũng cho ta điều vô lí. Suy ra $\displaystyle x+4\in C$. Ta có dãy $\displaystyle \{x-1,x,x+1,x+2,x+3,....,x+k\} \subseteq C$ và $\displaystyle x+k\in C$ dẫn tới $\displaystyle x+k+1\in C$ nhưng tập $\displaystyle C$ là hữu hạn cho nên nhận xét trên là vô lí. 

+ Nếu như $\displaystyle 2\in A$. Lúc này $\displaystyle x-1\in C$ và ta có những nhận xét như sau : Xét $\displaystyle \{x-1,x\} \in C$ và $\displaystyle \{1,2,...,k-1\} \in A$. 

Lúc này ta có $\displaystyle k\in B$ và xét $\displaystyle x-2\notin B$ vì nếu như $\displaystyle x-2\in B$ thì chọn $\displaystyle ( a,b,c) =( 2,x-2,x)$ ta có được điều vô lí. Vậy $\displaystyle x-2\in C$ hoặc $\displaystyle x-2\in A$. Bây giờ xét nếu như $\displaystyle x-k\in A$ thì vô lí do đó $\displaystyle x-k\in C$ hoặc $\displaystyle x-k\in B$. Nếu như $\displaystyle x-k\in B$ thì có $\displaystyle x-k+k-1=x-1\in C$ và $\displaystyle k-1\in A$ là điều vô lí. Vậy $\displaystyle x-k\in C$. Ta có $\displaystyle \{x-k,x-1,x\} \in C$. Tiếp theo xét $\displaystyle x-k-1\in B$ thì cũng chọn ra được $\displaystyle 1\in A$ mà $\displaystyle x-k-1+1=x-k\in C$ là điều vô lí. Do đó $\displaystyle x-k-1\in A$. Nhưng nếu như vậy thì ta có $\displaystyle x-k-1+k=x-1\in C$ mâu thuẫn. Vậy $\displaystyle x-k-1\in C$. Tương tự như trên, ta sẽ lấy $\displaystyle x-k-2,x-k-3,...$ đều thuộc $\displaystyle C$ nhưng các phần tử thuộc $\displaystyle C$ bị chặn dưới. Cho nên có điều mâu thuẫn. 

Từ hai trường hợp nhỏ trên ta kết luận rằng, với mỗi $\displaystyle x\in C$ thì kéo theo $\displaystyle x-1\in A$. 

Bây giờ gọi $\displaystyle \{c_{1} ,c_{2} ,...,c_{n}\}$ là các số thuộc tập $\displaystyle C$ thì $\displaystyle \{c_{1} -1,c_{2} -1,...,c_{n} -1\} \in A$. Vì các số $\displaystyle c_{i}$ là phân biệt cho nên $\displaystyle c_{i} -1\neq c_{j} -1,\forall i\neq j$. Do $\displaystyle |A|\geqslant n$ mà $\displaystyle |A|=n$ cho nên các số trên cũng chính là các số thuộc tập $\displaystyle A$. Do $\displaystyle 1\in A$ nên tồn tại $\displaystyle i$ để $\displaystyle c_{i} -1=1$ hay $\displaystyle 2\in C$ nhưng mâu thuẫn với nhận xét ở trên rằng $\displaystyle 2\notin C$. Vậy ta có điều phải chứng minh. 

[[Olympiad/Combinatorics/Problem 2.|Problem 2.]]
