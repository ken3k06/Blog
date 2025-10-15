
## Lớp và đối tượng

- Một lớp bao gồm các thành phần dữ liệu (thuộc tính) và các phương thức (hàm thành phần)
- Lớp trong C++ thực chất là một kiểu dữ liệu do người sử dụng định nghĩa
- Trong C++, dừng từ khóa class để chỉ điểm bắt đầu của một lớp sẽ được cài đặt

Ví dụ:

```cpp
class Student{// bao gom
// thuoc tinh 
// ham thanh phan 
};
```

Lớp là một mô tả trừu tượng của nhóm các đối tượng cùng bản chất, ngược lại mỗi một đối tượng là một thể hiện cụ thể cho những mô tả trừu tượng đó. Ví dụ xe ô tô thì có ô tô hãng audi, mercedes, vin phét.

Cú pháp khai báo như sau:
```cpp
class TenLop{
	private: 
	//
	protected:
	//
	public:
	//
}
```
Private là thành phần riêng, protected là thành phần riêng trong từng đối tượng, có thể truy cập từ lớp kế thừa hoặc các class con. 
Public là khai báo thành phần công cộng.
Private chỉ có thể được truy xuất từ các hàm thành phần nằm trong lớp đó. 


Các thuộc tính được khai báo như khai báo biến trong C.
Các phương thức được khai báo giống như khai báo hàm trong C. Có hai cách định nghĩa thi hành của một phương thức
- Định nghĩa thi hành trong lớp
- Định nghĩa thi hành ngoài lớp

Nói chung khi làm việc với các lớp thì ta cần xác định 3 thứ

- Xác định các thuộc tính (giống như một struct)
- Xác định các phương thức (hình vi) (những gì mà đối tượng có thể làm)
- Xác định các quyền truy xuất

Ví dụ:

```cpp
#include <iostream>
#include <bits/stdc++.h>
using namespace std; 
class Point{
    private:
    int x;
    int y; 
    public:
    void init(int ox, int oy)
    {
        x = ox;y=oy;
    };
    void move(int dx, int dy)
    {
        x+=dx; y+=dy;
    }
    void display(){
        cout << "Toa do thanh phan la\\n";
        cout << x  << " " << y << "\\n";
    }
};
int main(){
    Point p;
    p.init(5,6);
    p.move(2,4);
    p.display();
    return 0;
}
```

Tiếp theo ta có khái niệm về hàm khởi tạo. Hàm khởi tạo, hay constructor trong C++ là một hàm được tự động gọi khi ta tạo một đối tượng của lớp đó.
Mục đích của hàm khởi tạo là để khởi tạo các giá trị mặc định ban đầu cho các thành viên của lớp.
Một constructor thì mặc định sẽ có tên trùng với tên của class
Default constructor là hàm khởi tạo mặc định, tức là nếu ta gọi đối tượng mà không truyền dữ liệu vào thì nó sẽ mặc định lấy giá trị của đối tượng là giá trị mặc định của hàm khởi tạo.
Có thể overload cả default constructor và constructor.

Bây giờ ta nói về con trỏ trong OOP. Ví dụ khi lập trình OOP với python ta quen với cú pháp gọi `__init__()` khi tạo object.

Trong C++ cũng cho ta một con trỏ gọi là con trỏ this. Các biến thành viên sẽ được gọi trong Private còn constructor sẽ đưa vào trong Public.

Nếu ta không định nghĩa constructor mặc định nhưng lại có các constructor khác, trình biên dịch sẽ báo lỗi không tìm thấy constructor mặc định nếu ta không cung cấp tham số khi tạo thể hiện.
Trong thực tế khi thiết kế các class thì ta nên cung cấp cả hai loại constructor. 


Ví dụ:

```cpp
#include <iostream>
using namespace std;

class Student {
private:
    string name;   
    int age;       

public:
    // constructor (giống __init__)
    Student(string name, int age) {
        this->name = name;
        this->age = age;
    }

    void showInfo() {
        cout << "Name: " << name << ", Age: " << age << endl;
    }
};

int main() {
    Student s("Duc", 20);  // constructor tự động chạy
    s.showInfo();
}
```

**Ví dụ:**

![[Pasted image 20251015162618.png]]

```cpp
#include <iostream>
#include <bits/stdc++.h>
using namespace std;


int gcd (int a, int b) {
    return b ? gcd (b, a % b) : a;
};
// toan tu 3 ngoi: dieu kien ? bieu thuc neu dung : bieu thuc neu sai

class PhanSo{
    private:
    int tu;
    int mau;


    public:

    PhanSo(int t = 0 ,int m = 1){
        this -> tu = t;
        this -> mau = (m == 0) ? 1 : m;
        rutGon();
    }
    // can 1 ham nhap phan so vao, constructor tao gia tri mac dinh la 0/1
    // ta muon tu nhap de tao mot phan so moi
    void Nhap(){
        cout << "Nhập tử số: "; cin >> tu;
        cout << "Nhập mẫu số: "; cin >> mau; 
        if (mau == 0) {mau =1;}
        rutGon();
    }
    void Xuat(){
        if (mau == 1){ cout << tu;}
        else{
        cout << tu << "/" << mau; }
        }
    void rutGon(){
        int g  = gcd(abs(tu),abs(mau));
        tu /= g;
        mau /= g;
        if (mau < 0){
            tu = -tu ;
            mau = -mau;
        }
    }
    PhanSo Cong(const PhanSo& b){
        int x = this -> tu ;
        int y = this -> mau ;
        int num = x*b.mau + y*b.tu;
        int den = y * b.mau;
        return PhanSo(num, den);
    }
    PhanSo Tru(const PhanSo& b){
        int x = this -> tu;
        int y = this -> mau;
        int num = x*b.mau - y*b.tu;
        int den = y*b.mau;
        return PhanSo(num, den);
    }
    PhanSo Chia(const PhanSo &b){
        int x = this -> tu;
        int y = this -> mau;
        int num = x*b.mau;
        int den = y*b.tu;
        return PhanSo(num,den);
    }
    PhanSo Nhan(const PhanSo &b){
        int x =  this->tu;
        int y = this->mau;
        int num = x*b.tu;
        int den = y*b.mau;
        return PhanSo(num, den);
    }
    
};


int main()
{
    ios_base::sync_with_stdio(0);
    PhanSo a,b ; 
    cout << "Nhập phân số a: \n"; a.Nhap();
    cout << "Nhập phân số b: \n"; b.Nhap();
    cout << "Tổng là: "; a.Cong(b).Xuat(); cout <<endl;


    return 0;

}
```
## Static member

Khi một thuộc tính (biến) hoặc một phương thức (hàm) được khai báo với từ khóa `static` thì nó sẽ thuộc về lớp chứ không thuộc về từng đối tượng. Tức là giá trị của nó vẫn sẽ được giữ nguyên khi các đối tượng khác được tạo ra
```cpp
#include <iostream>
#include <bits/stdc++.h>
using namespace std;

class Counter{
    private:
    static int count;
    public:
    Counter(){
        count++; // mỗi lần tạo một object mới thì hàm counter được khởi tạo => count tăng
    }
    static void ShowCount(){
        cout << "Đã tạo " << count << " đối tượng"<< endl;
    }
};


int Counter::count = 0;

int main(){
    Counter a;
    Counter b; 
    Counter c;
    Counter::ShowCount();

    ios_base::sync_with_stdio(0);
    return 0;
}
```
