
**TL;DR:** Một bài viết hơi dài của mình, tổng hợp lại một số thứ về đa thức và các Secret Sharing Schemes dựa trên bài toán nội suy đa thức (Shamir, FROST)

## Các vấn đề trên đa thức

Ta sẽ xem một đa thức $a \in R[x]$ với $R$ là một trường (field) dưới dạng một danh sách hữu hạn các hệ số $(a_0,a_1,...,a_n)$. 
$$
a = a_nx^n +a_{n-1}x^{n-1}+...+a_1x+a_0
$$
trong đó $a_n=lc(a)$ được gọi là hệ số cao nhất và $a_0$ được gọi là hệ số tự do. 




## Tài liệu 

1. [Modern Computer Algebra](https://drive.google.com/file/d/1WSN4q7NyFg6DK6CQRP6uJKtVwV23UnPz/view)
2. [Operations on Polynomials and Series](https://cp-algorithms.com/algebra/polynomial.html)
3. https://doc.sagemath.org/html/en/constructions/polynomials.html
4. 
