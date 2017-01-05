

# dkimcrypt
`import "gitlab.one.com/go/dkimcrypt"`

* [Overview](#pkg-overview)
* [Index](#pkg-index)
* [Subdirectories](#pkg-subdirectories)

## <a name="pkg-overview">Overview</a>
Package dkimcrypt provides convenient functions for en- or decrypting, as
well as signing and verifying data using a combination of local private key
files and public keys present in DKIM DNS TXT records




## <a name="pkg-index">Index</a>
* [Constants](#pkg-constants)
* [func Decrypt(selector, privkeypath string, in, key, mac []byte) (out []byte, err error)](#Decrypt)
* [func DecryptSingle(selector, privkeypath string, in []byte) (out []byte, err error)](#DecryptSingle)
* [func Encrypt(selector, domain string, in []byte) (out, key, mac []byte, err error)](#Encrypt)
* [func EncryptSingle(selector, domain string, in []byte) (out []byte, err error)](#EncryptSingle)
* [func Sign(message []byte, privkeypath string) (out []byte, err error)](#Sign)
* [func Verify(message, signature []byte, selector, domain string) (err error)](#Verify)


#### <a name="pkg-files">Package files</a>
[crypt_decrypt.go](/src/dkimcrypt/crypt_decrypt.go) [privkey.go](/src/dkimcrypt/privkey.go) [pubkey.go](/src/dkimcrypt/pubkey.go) [sign_verify.go](/src/dkimcrypt/sign_verify.go) 


## <a name="pkg-constants">Constants</a>
``` go
const (
    KeySize = sha256.Size * 8
    MacSize = sha256.Size
)
```
KeySize and MacSize are the sizes in bits of the AES key and the Authentication Code, respectively




## <a name="Decrypt">func</a> [Decrypt](/../blob/master/crypt_decrypt.go?s=3093:3180#L116)
``` go
func Decrypt(selector, privkeypath string, in, key, mac []byte) (out []byte, err error)
```
Decrypt will decrypt the data in 'in' and return it in 'out', given the path to a PEM-encoded
RSA private key file, an RSA-encrypted key, a message authentication code hash,
and a selector, which must be the same used for encryption



## <a name="DecryptSingle">func</a> [DecryptSingle](/../blob/master/crypt_decrypt.go?s=2074:2157#L87)
``` go
func DecryptSingle(selector, privkeypath string, in []byte) (out []byte, err error)
```
DecryptSingle is a wrapper around Decrypt, which will decrypt a byte slice
encrypted by EncryptSingle



## <a name="Encrypt">func</a> [Encrypt](/../blob/master/crypt_decrypt.go?s=3910:3992#L145)
``` go
func Encrypt(selector, domain string, in []byte) (out, key, mac []byte, err error)
```
Encrypt will AES-encrypt the data given in 'in', and return the encrypted
version in 'out', as well as a key, which is RSA-encrypted using the public
key it finds in the DKIM-like TXT record at [selector]._domainkey.[domain],
and a message authentication code hash.  Use the same selector in 'Decrypt'



## <a name="EncryptSingle">func</a> [EncryptSingle](/../blob/master/crypt_decrypt.go?s=2595:2673#L102)
``` go
func EncryptSingle(selector, domain string, in []byte) (out []byte, err error)
```
EncryptSingle is a wrapper around Encrypt, which will encrypt a byte slice
and return a single byte slice representing a key, a verification hash and
the ecrypted data, useful for sending over a network. Decrypt using
DecryptSingle



## <a name="Sign">func</a> [Sign](/../blob/master/sign_verify.go?s=207:276#L3)
``` go
func Sign(message []byte, privkeypath string) (out []byte, err error)
```
Sign will return the signature of the message in 'message' using the private
key in the file at 'privkeypath'.



## <a name="Verify">func</a> [Verify](/../blob/master/sign_verify.go?s=836:911#L31)
``` go
func Verify(message, signature []byte, selector, domain string) (err error)
```
Verify a signature given the signature, the message it signed and the
selector and domain that signed it. If err is nil, then the signature is
good.








- - -
Generated by [godoc2md](http://godoc.org/github.com/davecheney/godoc2md)
