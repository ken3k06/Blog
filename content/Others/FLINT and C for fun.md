## Giới thiệu 
Xem doc và tải thư viện tại đây: https://flintlib.org/doc/index.html hoặc đọc phiên bản PDF: https://flintlib.org/doc/flint.pdf

Check version hiện tại:
```c
#include <flint/flint.h>
#include <flint/arb.h>
int main(){
    flint_printf("Computed with FLINT-%s\n", flint_version);
    return 0;
}
// Computed with FLINT-3.5.0-dev
```
Để compile chương trình thì thêm flag `-lflint -lmpfr -lgmp` vào:
```bash
gcc test.c -lflint -lmpfr -lgmp -o test && ./test
```


## Challenges to work with 
