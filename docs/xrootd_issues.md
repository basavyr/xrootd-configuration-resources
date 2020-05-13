## xrootd issues 
When trying to build project with cmake:

Plenty of *Undefined symbols for architecture x86_64:* type of errors 


* Determining if the function *setresuid* exists failed
* Determining if the function *sigwaitinfo* exists failed
* Determining if the function *sigwaitinfo* exists in the rt failed
* Determining if the include file shadow.h exists failed
* Determining if the function *getprotobyname_r* exists failed
* Determining if the function *getprotobyname_r* exists in the socket failed
* Determining if the function *gethostbyaddr_r* exists failed
* Determining if the function *gethostbyaddr_r* exists in the socket failed
* Determining if the include file et/com_err.h exists failed
* Determining if the function *uuid_generate_random* exists in the uuid failed
* Determining if the function TLS_method exists failed 
	* cannot link directly with dylib/framework, your binary is not an allowed client of /usr/lib/libcrypto.dylib for architecture x86_64
	* potential issue with linking the crypto lib
* Determining if the TLS_method exist failed
``` CMakeTmp/CheckSymbolExists.c:2:10: fatal error: 'OPENSSL_INCLUDE_DIR-NOTFOUND/openssl/ssl.h' file not found
#include <OPENSSL_INCLUDE_DIR-NOTFOUND/openssl/ssl.h>
         ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
```
	* potential issue with the linking of the ssl directory 
* Determining if the function TLSv1_2_method exists failed
```
ld: cannot link directly with dylib/framework, your binary is not an allowed client of /usr/lib/libcrypto.dylib for architecture x86_64

```
* Determining if the TLSv1_2_method exist failed 
```
CMakeTmp/CheckSymbolExists.c:2:10: fatal error: 'OPENSSL_INCLUDE_DIR-NOTFOUND/openssl/ssl.h' file not found
#include <OPENSSL_INCLUDE_DIR-NOTFOUND/openssl/ssl.h>
         ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
```
* Determining if the function TLSv1_1_method exists failed
```
ld: cannot link directly with dylib/framework, your binary is not an allowed client of /usr/lib/libcrypto.dylib for architecture x86_64
```
* Determining if the TLSv1_1_method exist failed 
```
CMakeTmp/CheckSymbolExists.c:2:10: fatal error: 'OPENSSL_INCLUDE_DIR-NOTFOUND/openssl/ssl.h' file not found
#include <OPENSSL_INCLUDE_DIR-NOTFOUND/openssl/ssl.h>
         ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
1 error generated.
```
* Determining if the function TLSv1_method exists failed
```
ld: cannot link directly with dylib/framework, your binary is not an allowed client of /usr/lib/libcrypto.dylib for architecture x86_64
```
* Determining if the TLSv1_method exist failed
```
CMakeTmp/CheckSymbolExists.c:2:10: fatal error: 'OPENSSL_INCLUDE_DIR-NOTFOUND/openssl/ssl.h' file not found
#include <OPENSSL_INCLUDE_DIR-NOTFOUND/openssl/ssl.h>
         ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
1 error generated.
```
* Determining if the function DH_compute_key_padded exists failed 
```
ld: cannot link directly with dylib/framework, your binary is not an allowed client of /usr/lib/libcrypto.dylib for architecture x86_64

```
* Determining if the DH_compute_key_padded exist failed
```
CMakeTmp/CheckSymbolExists.c:2:10: fatal error: 'OPENSSL_INCLUDE_DIR-NOTFOUND/openssl/dh.h' file not found
#include <OPENSSL_INCLUDE_DIR-NOTFOUND/openssl/dh.h>
         ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
1 error generated.

```

## Potential fixes

1. configure `OPENSSL` directory 
2. configure the crpypto library in openssl

