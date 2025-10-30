
Để học một ngôn ngữ lập trình mới, theo mình ta cần bắt đầu từ 3 vấn đề cơ bản nhất: Một là biến và kiểu dữ liệu, hai là các câu lệnh điều kiện, rẽ nhánh và ba là quy tắc khai báo và gọi hàm.

Chạy thử code rust trên đây: [Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2024)
## Mở đầu

Chương trình hello world đầu tiên:

```rust
fn main(){
	println!("Hello World");
}
```

Rust có một điểm khá giống với C++ đó chính là điểm bắt đầu của chương trình nằm ở hàm `fn main()` và sẽ có dấu `;` ở cuối mỗi câu lệnh, trừ một vài trường hợp đặc biệt.

Đối với Rust thì ta sẽ sử dụng Cargo làm công cụ quản lí gói. Về công dụng của nó thì mọi người xem tại đây: [https://doc.rust-lang.org/cargo/](https://doc.rust-lang.org/cargo/)

Để build một project mới bằng Cargo thì ta sẽ dùng lệnh Cargo new + [tên project]. Lúc này Cargo sẽ tự động tạo ra các file Cargo.lock, Cargo.toml và hai thư mục src, target. Về chức năng của từng cái thì tạm thời mình sẽ bỏ qua và cũng chưa cần thiết để đào sâu lắm.

Chương trình chính của ta sẽ nằm ở thư mục src chứa file [main.rs](http://main.rs)

Để chạy file thì ta sẽ gõ `Cargo run` . Hoặc tải extension `rust-analyzer` trong VS-Code. Ngoài ra có thể tải thêm CodeLLDB để debug code Rust

Cargo còn giúp ta quản lí các thư viện ngoài hay các dependencies từ [https://crates.io/](https://crates.io/)

Ví dụ ta muốn tải thư viện `rand` để làm việc với các hàm sinh số ngẫu nhiên thì ta thêm dòng này vào trong file Cargo.toml và gõ `Cargo build`

```rust
[dependencies]
rand = "0.8.5"
```

Cargo sẽ tự động tải các gói cần thiết về và ta có thể sử dụng được thư viện này.

## Biến và kiểu dữ liệu

Kiểu dữ liệu trong Rust khá đặc biệt, được chia làm 2 loại là Mutable và Immutable.

Để khởi tạo một biến trong Rust, ta sẽ dùng từ khóa `let` , mặc định khi ta tạo một biến mới thì biến đó sẽ được định nghĩa là Immutable tức là không thể thay đổi. Điều này có nghĩa là sau khi khởi tạo biến, ta không thể thay đổi giá trị của nó nữa.

Ví dụ mình có đoạn chương trình sau đây:

```rust
fn main(){
	let x = 5; 
	println!("x = {}" , x); 
	x +=1;
}
```

Thì sẽ gặp ngay lỗi:

```rust
(base) ➜  rustt rustc main.rs
warning: value assigned to `x` is never read
 --> main.rs:4:5
  |
4 |     x += 1;
  |     ^
  |
  = help: maybe it is overwritten before being read?
  = note: `#[warn(unused_assignments)]` on by default

error[E0384]: cannot assign twice to immutable variable `x`
 --> main.rs:4:5
  |
2 |     let x = 5;
  |         - first assignment to `x`
3 |     println!("x = {}", x);
4 |     x += 1;
  |     ^^^^^^ cannot assign twice to immutable variable
  |
help: consider making this binding mutable
  |
2 |     let mut x = 5;
  |         +++

error: aborting due to 1 previous error; 1 warning emitted

For more information about this error, try `rustc --explain E0384`.
(base) ➜  rustt

```

Đọc log thì mọi người để ý lỗi ở đây là `cannot assign twice to immutable variable` và cách xử lí đơn giản là ta thêm từ khóa `mut` ở trước biến `x` khi khai báo.

Rust đảm bảo rằng nếu ta khai báo một giá trị là immutable thì nó sẽ thực sự không thay đổi =)) điều này giúp tránh việc có một đoạn code nào đó làm thay đổi giá trị của biến mà ta không mong muốn.

Ngoài ra còn có một khái niệm đó là Shadowing, tức là ta khai báo hai biến cùng một tên và khác kiểu giá trị, như vậy biến được khai báo lần thứ hai sẽ làm lu mờ đi biến thứ nhất.

```rust
fn main(){
	let x = 5; 
	let x = 6; 
	println!("x = {}" , x); 
	x +=1;
}
```

```rust
warning: unused variable: `x`
 --> main.rs:2:9
  |
2 |     let x = 5;
  |         ^ help: if this is intentional, prefix it with an underscore: `_x`
  |
  = note: `#[warn(unused_variables)]` on by default

warning: 1 warning emitted

(base) ➜  rustt ./main
x = 6
(base) ➜  rustt
```

Về phần kiểu dữ liệu thì thông thường Rust có thể đoán được kiểu dữ liệu của biến. Nó sẽ trông như thế này:
![[Pasted image 20251030205516.png]]
Và lưu ý một điều là các biến trong Rust một khi được khai báo trong scope thì nó sẽ chỉ tồn tại trong scope đó mà thôi. Scope ở đây là cặp ngoặc nhọn `{}`. Khi ra khỏi scope thì chúng sẽ bị xóa đi để giải phóng bộ nhớ.

Ngoài khai báo biến thì ta có thể khai báo constants hay còn gọi là hằng số.
Khi khai báo thì bắt buộc phải có khóa const và kiểu dữ liệu

Quy ước đặt tên của Rust cho các hằng số là sử dụng tất cả chữ hoa và dấu gạch dưới giữa các từ.

```rust
fn main()
{
	const MAX_SCORE : u32 = 100_000; 
	println!("Max score: {}" , MAX_SCORE);  
}
```

Các kiểu dữ liệu bao gồm:
Đầu tiên là scalar types.
Scalar type là kiểu dữ liệu đại diện cho một giá trị duy nhất. Trong rust thì ta có integers, floating-point numbers (số dấu chấm động), Booleans và characters, tương tự như các ngôn ngữ lập trình khác.
Và lưu ý một điều là các biến trong Rust một khi được khai báo trong scope thì nó sẽ chỉ tồn tại trong scope đó mà thôi. Scope ở đây là cặp ngoặc nhọn `{}`. Khi ra khỏi scope thì chúng sẽ bị xóa đi để giải phóng bộ nhớ.

Ngoài khai báo biến thì ta có thể khai báo constants hay còn gọi là hằng số.

Khi khai báo thì bắt buộc phải có khóa const và kiểu dữ liệu

Quy ước đặt tên của Rust cho các hằng số là sử dụng tất cả chữ hoa và dấu gạch dưới giữa các từ.

```rust
fn main()
{
	const MAX_SCORE : u32 = 100_000; 
	println!("Max score: {}" , MAX_SCORE);  
}
```

Các kiểu dữ liệu bao gồm:

Đầu tiên là scalar types.

Scalar type là kiểu dữ liệu đại diện cho một giá trị duy nhất. Trong rust thì ta có integers, floating-point numbers (số dấu chấm động), Booleans và characters, tương tự như các ngôn ngữ lập trình khác.

### Integer Types

![[Pasted image 20251030205553.png]]

![[Pasted image 20251030205614.png]]

Trong Rust thì một byte đơn lẻ sẽ là

```rust
let b: u8 = b'a'; 
println!("{}",b);
```

Còn đối với một chuỗi byte thì dùng `b"abc"(&[u8;3])` Ví dụ như này:

```rust
    let b = b"abc"; 
    for byte in b{
        println!("{}", byte)
    }
```

### Floating-Point Types

Floating thì có 2 kiểu là `f32` và `f64` lần lượt là 32 và 64 bit kích thước:

```rust
fn main(){
	let x = 2.0; // f64 
	let y: f32 = 3.0; //f32
}
```

Các phép toán cơ bản trong Rust:

```rust
fn main(){
	let x = 5;
	let y = 5; 
	let sum = x + y; 
	let diff = x - y ;
	let product = x*y; 
	let remainder = 43 % 5; 
}
```

Đối với phép chia thì nếu cả hai số là `i32` thì sẽ chia lấy phần nguyên còn nếu số thực thì chia như bình thường, kết quả trả về cũng là số thực

```rust
let quo = 56.7 /32.1 ; // 1.7663551
let trunc = -5/3; // -1
```

### The Boolean Type

Boolean type thì có 2 giá trị là `true` hoặc `false`.

Nó chỉ nhận 2 giá trị duy nhất là `true` hoặc `false`.

Khác với python ở chỗ này. Như trong python thì ta có `15` hay `{0},[0]` đều được tính là `true` khi ta ép kiểu bool cho nó.

### The Character Type

Char được khai báo như sau:

```rust
fn main(){
	let c = 'z'; 
	let z: charr = 'Z'; 
	let cat = '😻';
}
```

Lưu ý rằng ở đây ta dùng dấu nháy đơn chứ không phải dấu nháy kép như string. Hơn nữa `char` trong rust có kích thước là 4 byte (unicode scalar value) nên nó lưu được mọi kí tự unicode chứ không chỉ ASCII.

Và chỉ được lưu một kí tự duy nhất. Tức là ta không được lưu kiểu

```rust
let c = 'AB'
```

### Compound Types

Compound types là kiểu dữ liệu có thể nhóm nhiều giá trị thuộc cùng một kiểu dữ liệu lại với nhau. Trong rust có hai kiểu dữ liệu cơ bản thuộc loại này đó là tuple và arrays

Tuple thì có thể gộp nhiều kiểu dữ liệu vào một, chẳng hạn như:

```rust
let tup: (i32, f64, u8) = (500, 6.4, 1);
```

Kích thước của tuple là cố định và không thay đổi sau khi khai báo.

```rust
let (x, y, z) = tup;   // destructuring
println!("{}", y);     // 6.4

println!("{}", tup.0); // 500
println!("{}", tup.1); // 6.4
```

Tuple có thể rỗng:

```rust
let unit = (); 
```

`()` được gọi là unit type (giống với void trong C++)

Tiếp theo là array. Cú pháp khai báo sẽ là `tên biến: [kiểu dữ liệu; kích thước]`

```rust
let arr: [i32; 4] = [1,2,3,4]; 
```

Tương tự như python thì chỉ số của mảng cũng bắt đầu bằng 0.

Ngoài ra ta cũng có thể khởi tạo nhanh một mảng rỗng như sau:

```rust
let zeros = [0;5]; // [0,0,0,0,0]
```

Bây giờ ta sẽ đào sâu hơn về array.

Cú pháp khai báo thì có 2 cách, 1 là ta gắn kiểu và độ dài rõ ràng như trên, 2 là để cho rust tự suy luận kiểu dữ liệu

```rust
let arr = [1,2,3,4]; 
let arr : [i32;3] = [20,30,40];
```

Hoặc dùng const như sau:

```rust
const N: usize = 4;
let arr = [1;N]; 
```

Trong đó `usize` là kiểu số nguyên dùng làm chỉ số mảng

Mảng lồng nhau: Tạo ma trận hai chiều

```rust
let matrix = [
[1,2,3],[4,5,6],];
println!("{}", matrix[1][2]); //6
```

Lấy độ dài của mảng bằng

```rust
println!("{}", arr.len()); 
```

Kiểm tra có rỗng không:

```rust
if arr.is_empty(){...}
```

Truy cập vào phần tử đầu vào cuối:

```rust
println!("{:?}", arr.first()); // Some(1)
println!("{:?}", arr.last());  // Some(4)
```

Dùng cú pháp `.iter_mut()` để cho phép thay đổi giá trị khi duyệt

```rust
let mut arr = [1,2,3]; 
for x in arr.iter_mut(){
	*x *= 2; 
}
println!("{:?}", arr); // 
```

Dùng map, giống list comprehension bên python:

```rust
let doubled = arr.map(|x| x * 2);
println!("{:?}", doubled); //
```

Kiểm tra có tồn tại giá trị cụ thể hay không:

```rust
if arr.contains(&3) {
    println!("Found 3!");
}
```

Lấy giá trị ở vị trí cụ thể:

```rust
println!("{:?}", arr.get(10)); //None
```

Nếu vượt quá giới hạn thì trả về `Option<&T>` thay vì thông báo panic.

Ta có thể dùng slicing để lấy mảng con:

```rust
let slc = &arr[..2]; // phan tu [0..2)
```

Là lấy 2 phần tử đầu tiên.

Code test:

```rust
fn main() {
    let mut arr = [1,2,3];
    for x in arr.iter_mut(){
        *x *= 2;
    }
    println!("{:?}", arr); 
    println!("{}", arr.len());
    println!("{}", arr.is_empty()); 
    println!("{:?}", arr.first());
    println!("{:?}", arr.last()); 
    let doubled = arr.map(|x| x * 2);
    println!("{:?}", doubled); // [4,8,12]
    if arr.contains(&3) {
    println!("Found 3!");
} else{
    println!("Đéo có đâu");}
    println!("{:?}", arr.get(1));
    let slc = &arr[..2];
    println!("{:?}", slc);
}
```

### Vec Type

## **References và Borrowing**

Đây là một cặp khái niệm mình thấy cực hay trong Rust, giúp cú pháp của Rust trở nên chặt chẽ hơn nhiều.

[What is Ownership?](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html)

### Stack & Heap

Nhiều ngôn ngữ lập trình không yêu cầu ta phải hiểu rõ về stack và heap quá rõ ràng. Tuy nhiên đối với một ngôn ngữ lập trình hệ thống như Rust thì việc hiểu rõ hai khái niệm này khá quan trọng vì một giá trị nằm trên stack hay heap sẽ ảnh hưởng đến cách nó hoạt động và tương tác với các thành phần khác trong chương trình.

Đầu tiên, cả stack và heap đều là những vùng nhớ có sẵn giúp lưu trữ giá trị khi thực thi chương trình. (chúng sẽ được lưu trữ trong RAM)

- Stack hoạt động theo cơ chế LIFO, các giá trị lưu trên stack đều có kích thước cố định. Bộ nhớ stack được dùng để lưu trữ các biến cục bộ trong hàm, tham số truyền vào. Việc truy cập vào bộ nhớ này rất nhanh và được thực thi khi chương trình được biên dịch.
- Còn bộ nhớ Heap được dùng để lưu trữ vùng nhớ cho những biến con trở được cấp phát động. Nó là một vùng nhớ mà các giá trị được lưu trên đó không xác định kích thước (dùng để lưu những phần tử có kích thước thay đổi). Trên heap, một lượng bộ nhớ sẽ được cấp phát cùng với đó là trả về 1 con trỏ lưu địa chỉ của vị trí vừa được cấp phát. Con trỏ chứa địa chỉ ô nhớ với kích thước cố định và được lưu ở stack

![[Pasted image 20251030205709.png]]


### Ownership

Ownership là một khái niệm hoàn toàn mới trong Rust, có chức năng đảm bảo tính an toàn, tối ưu cho bộ nhớ mà không cần đến garbage collector như trong Python hoặc một số ngôn ngữ khác như C/C++ yêu cầu người dùng phải tự giải phóng bộ nhớ bằng tay.

Ownership được định nghĩa là một bộ các quy tắc chỉ định cách quản lý bộ nhớ trong Rust và nếu bất kì quy tắc nào bị vi phạm thì chương trình sẽ không được biên dịch.

Các quy tắc như sau:

- Mỗi giá trị trong Rust có một biến được gọi là chủ sở hữu (ownership) của nó
- Chỉ có thể có một chủ sở hữu tại một thời điểm
- Khi chủ sở hữu đi ra khỏi phạm vi, bộ nhớ lưu giá trị đó sẽ được giải phóng

Quy tắc đầu tiên:

```rust
fn main(){
	let s = String::from("hello");
}
```

`"hello"` nằm trong heap và `s` là biến duy nhất sở hữu nó.

Quy tắc thứ hai:

```rust
fn main(){
	let s1 = String::from("Hello"); 
	let s2 = s1; 
	println!("{}",s1); 
}
```

Khi `s1` được gán cho `s2` thì Rust chuyển quyền sở hữu dữ liệu cho `s2` chứ không copy dữ liệu heap. Như vậy `s1` sẽ bị vô hiệu ngay lập tức sau khi ta gọi `s2`. Nếu ta chuyển thành `println!("{}", s2);` thì chương trình chạy lại bình thường.

Nhưng hãy xem xét kĩ hơn, ta hãy cùng xem các giá trị lưu trữ trên biến `s1`:

![[Pasted image 20251030205721.png]]

Biến `s1` lưu trữ 3 thông tin trên stack:

- con trỏ ptr trỏ đến nội dung của chuỗi trên heap
- len lưu độ dài của chuỗi (tính bằng bytes)
- capacity lưu kích thước bộ nhớ đang được cấp phát cho chuỗi (tính bằng bytes)


![[Pasted image 20251030205736.png]]
Khi ta gán `let s2 = s1;` thì trình biên dịch sẽ hiểu là ta đang copy nông thay vì copy sâu. Do đó chỉ phần con trỏ, len và capacity được copy thay vì giữ liệu trên heap và từ đó tiết kiệm được 1 lượng bộ nhớ trên heap.

![[Pasted image 20251030205749.png]]

Nếu như cấp phát như thế này thì khi ra khỏi scope , rust sẽ tự động gọi hàm `drop()` và giải phóng bộ nhớ Heap 2 lần và gây ra  "double free error"

Quy tắc thứ ba:

```rust
fn main(){
	{let s = String::from("Hello");}
	println!("{:?}",s);
}
```

Gặp ngay lỗi:

```rust
help: the binding `s` is available in a different scope in the same function

```

Khi ra khỏi scope thì vùng nhớ heap sẽ được giải phóng ngay

Lưu ý là trong Rust chỉ có một số kiểu dữ liệu đặc biệt được cấp phát trên heap còn đa số dữ liệu sẽ nằm trên stack

Stack: Mọi giá trị có kích thước cố định, nhỏ, xác định tại compile time đều nằm trực tiếp trên stack

```rust
let x: i32 = 10; 
let b: bool = true; 
let c: char = 'A'; 
let tup = (1,2.0,false); 
```

Heap: sẽ dùng cho những dữ liệu có kích thước quá lớn để lưu trực tiếp trên stack hoặc ta không biết được trước kích thước của nó.

Như trên thì biến kiểu `String` sẽ được cấp phát trên Heap, ta có thể thay đổi nội dung, độ dài tùy ý của nó.

Với str literal thì ta không làm được như vậy:

```rust
fn main() {
   let mut a = "conglt";
   println!("{}", a);
}
```

```rust
   Compiling playground v0.0.1 (/playground)
warning: variable does not need to be mutable
 --> src/main.rs:2:8
  |
2 |    let mut a = "conglt";
  |        ----^
  |        |
  |        help: remove this `mut`
  |
  = note: `#[warn(unused_mut)]` on by default
```

## Control Flow

Tương tự các ngôn ngữ lập trình khác thì Rust cũng có 3 câu lệnh điều khiển luồng cơ bản là `if, while, for`.

### If

Lệnh điều kiện if cho phép ta rẽ nhánh dựa trên các điều kiện. Syntax cơ bản:

```rust
fn main() {
    let number = 3;

    if number < 5 {
        println!("condition was true");
    } else {
        println!("condition was false");
    }
}
```

Nếu có nhiều trường hợp hơn thì thêm `else if` vào

```rust
fn main() {
    let number = 6;

    if number % 4 == 0 {
        println!("number is divisible by 4");
    } else if number % 3 == 0 {
        println!("number is divisible by 3");
    } else if number % 2 == 0 {
        println!("number is divisible by 2");
    } else {
        println!("number is not divisible by 4, 3, or 2");
    }
}
```

### while, loop, for

Rust có 3 vòng lặp đó là `while, loop, for` . Ví dụ như sau:

**Vòng lặp loop:**

```rust
fn main(){
    let mut count = 0; 
    loop {
        count +=1; 
        if count == 5{
            break;
        }
        println!("count: {}", count);
    }
}
```

Loop có thể lặp vô hạn nếu ta không thêm `break;` ở trong:

```rust
fn main() {
    loop {
        println!("again!");
    }
}
```

Có thể interrupt bằng ctrl+c

Loop cũng có thể trả về giá trị nếu ta thêm giá trị trả về vào ngay sau câu lệnh break

```rust
fn main(){
    let _res = loop {
        break 10 * 2; 
    };
    println!("{}", _res)
}

```

Thêm nữa là nếu như ta xài nhiều vòng loop lồng nhau thì có thể gán nhãn cho chúng để lệnh `break` và `continue` biết đang trỏ tới vòng loop nào:

Ví dụ:

```rust
fn main() {
    let mut count = 0;
    'counting_up: loop {
        println!("count = {count}");
        let mut remaining = 10;

        loop {
            println!("remaining = {remaining}");
            if remaining == 9 {
                break;
            }
            if count == 2 {
                break 'counting_up;
            }
            remaining -= 1;
        }

        count += 1;
    }
    println!("End count = {count}");
}
```

Kết quả:

```rust
count = 0
remaining = 10
remaining = 9
count = 1
remaining = 10
remaining = 9
count = 2
remaining = 10
End count = 2
```

**Vòng lặp while:**

Lặp khi điều kiện còn đúng:

```rust
let mut n = 3;
while n > 0 {
    println!("{}!", n);
    n -= 1;
}
println!("Hết giờ!"); 
```

**Vòng lặp for:**

Duyệt qua một range hoặc iterator:

```rust
for i in 1..5 { // 1, 2, 3, 4
    println!("i = {}", i);
}

let arr = [10, 20, 30];
for val in arr.iter() {
    println!("Giá trị: {}", val);
}
```

Ngoài ra ta còn có:
### match

Ví dụ:

```rust
let number = 2;

match number {
    1 => println!("Một"),
    2 | 3 => println!("Hai hoặc ba"), // nhiều trường hợp
    4..=6 => println!("Từ 4 đến 6"), // range
    _ => println!("Khác"),           // mặc định
}

```

## Functions

Hàm là một nhóm các đoạn code thực hiện một công việc nào đó và có thể được gọi để sử dụng ở nhiều nơi khác nhau. Trong một chương trình Rust có thể viết bao nhiêu hàm cũng được.

Ta đã biết: Hàm `main()` là điểm khởi đầu của mọi chương trình rust.

Rust cũng có quy tắc đặt tên hàm riêng tương tự như quy tắc đặt tên cho hằng số. Quy tắc đặt tên hàm trong rust sẽ là viết thường và cách nhau bằng dấu gạch dưới `_` (snake case).

Cú pháp đơn giản như sau:

```rust
fn ten_ham(tham_so1: kieu, tham_so2: kieu) -> kieutrave {
	// than ham 
}
```

Nếu muốn return về giá trị thì ta không thêm dấu chấm phẩy ở dòng cuối cùng của hàm, nếu không thì trình biên dịch sẽ hiểu đây là hàm thực thi chứ không trả về giá trị.

```rust
fn main() {
    fn tinh_tong(a:i32, b:i32)->i32{
        a+b
    }
    let a:i32 = 5; 
    let b:i32 = 7;
    let tong:i32= tinh_tong(a,b);
    println!("{}", tong); 
}
```

Hàm không trả về dữ liệu (hàm thực thi):

```rust
fn xinchao(){
    println!("Xin chao"); 
}

fn main() {
    xinchao(); 
}
```

Hoặc thêm return vào như sau:

```rust

fn kiem_tra(x: i32) -> i32 {
    if x < 0 {
        return 0;
    }
    x * 2
}
fn main() {
    let x = -7; 
    let test = kiem_tra(x); 
    println!("test = {}", test); 
}
```

## Thực hành

[https://cryptohack.org/challenges/general/](https://cryptohack.org/challenges/general/)

### ASCII

Có 2 cách để làm, một là dùng `arr` , hai là dùng `vec`.

```rust
    // bai 1
    let a: [u8;23] = [99, 114, 121, 112, 116, 111, 123, 65, 83, 67, 73, 73, 95, 112, 114, 49, 110, 116, 52, 98, 108, 51, 125];
    let s:String = a.iter().map(|&c| c as char).collect(); 
    let mut vec: Vec<char> = Vec::new(); 

    println!("{}", s); 
    for chr in a.iter(){
        let c = chr.clone(); 
        let chr = c as char;  
        println!("{}",chr); 
        vec.push(chr); 
    }
    let flag: String = vec.iter().collect(); 
    println!("{:?}", flag); 
```

Trong Python thì có cú pháp `''.join` còn ở đây thì có vẻ ta sẽ sử dụng `collect();`.

 [Storing Lists of Values with Vectors](https://doc.rust-lang.org/book/ch08-01-vectors.html#storing-lists-of-values-with-vectors)

Cái hay của vector đó là ta có thể khai báo nó trực tiếp mà không cần biết trước độ dài. Muốn thêm phần tử vào thì ta dùng `vec.push(element)`.

**Một số lưu ý:**

Có một số cách chính để duyệt qua Array.
Một là ta dùng `&a` là con trỏ để tham chiếu tới array `a`. Hai là dùng `a.iter()` và ba là `a.into_iter()`. Mỗi phương thức sẽ có ý nghĩa khác nhau.


```rust
fn main(){
    let a: [u8;3] = [99, 114, 121];
    for v in &a{
        println!("{}",v);
    }
    
    for v in a.iter(){
        println!("{}",v); 
    }
    for v in a.into_iter(){
        println!("{}", v);
    }
    
}

```

![[Pasted image 20251030210003.png]]

[StackOverflow - What is the difference between iter and into iter](https://stackoverflow.com/questions/34733811/what-is-the-difference-between-iter-and-into-iter)

Chuyển string thành bytes như sau:

```rust
fn main(){
    let s:String = "flag{fake_flag}".to_string();
    let byte = s.as_bytes();
    println!("{:?}", byte);
}
```

### Hex

Có một số thư viện mà ta cần nắm rõ: 

- [Base64](https://docs.rs/base64/latest/base64/)
- [Hex](https://docs.rs/hex/0.4.3/hex/)

### Bytes and Big Integers

- [Num BigInt](https://docs.rs/num-bigint/latest/num_bigint/)
- [Num Traits](https://docs.rs/num-traits/latest/num_traits/)



## Resources 
1. https://cheats.rs/
2. https://doc.rust-lang.org/book/
3. https://crates.io/
Ngoài ra có thể tham khảo phiên bản dịch tiếng Việt của anh Đào Hải Nam: [![](https://s0.wp.com/i/favicon.ico?m=1713425267i)namdhDịch tài liệu Rust (Rust book)](https://daohainam.com/2023/03/07/dich-tai-lieu-rust-rust-book/)​
