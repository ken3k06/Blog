## Giới thiệu 
Xem doc và tải thư viện tại đây: https://flintlib.org/doc/index.html hoặc đọc phiên bản PDF của nó: https://flintlib.org/doc/flint.pdf

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

Ngoài ra thì còn có thư viện OpenSSL build bằng C compiler:  https://wiki.openssl.org/index.php/Compilation_and_Installation
Phiên bản mới nhất của OpenSSL hiện tại là 3.6 và đã được cài đặt sẵn các chuẩn mã hóa hậu lượng tử. Tải tại đây: https://openssl-library.org/source/

Check phiên bản:
```c
#include <stdio.h>
#include <openssl/crypto.h>

int main(void) {
    printf("OpenSSL runtime version: %s\n", OpenSSL_version(OPENSSL_VERSION));
    return 0;
}
// OpenSSL runtime version: OpenSSL 3.6.0 1 Oct 2025
```

	
