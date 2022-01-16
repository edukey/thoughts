How to check signature of JWT
=============================

Simple samples of JWT signature checks in different languages using only standard libraries where possible.

Note that JWT dedicated frameworks exists, but here we want to show quick samples not requiring external dependencies.

We consider for the samples that JWT is in a text file, and public key from a certificate file.

Reminder
--------

JWT is 3 base64url parts separated by a dot '.'
- First is header as JSON ex: `{"alg":"RS56","typ":"JWT"}`
- Second is content as JSON
- Third is signature, ex: 256 Bytes when sign key is 2048 bits (256 Bytes), so 340 Bytes base64 (base64url does not require '=' padding)

Signed data is the JWT without the signature : base64 header + '.' + base64 content

Algo with 'HS' are symmetric HMAC, should not be used unless key is only for one to one dedicated JWT.

'RS' and 'JS' algos are asymmetric RSA, 'JS' (JSS padding instead of PKCS7 one) is more secure but less common.

Python
------

Python standard library has no way to check RSA signatures, needs external libraries as pyopenssl or pca/cryptography (both relying above openssl lib)

```python
# pip install openssl
```

```python
# pip install cryptography
```

Java
----

```java

```

C#
----

C# 5 on dotnet fmk 8

```csharp
public static void Main(String args[]) {
}
```


Go
--


```go
package main
import ( "fmt" ; "os" ;  "strings" ; "encoding/base64" ; "encoding/pem" ; "crypto/x509" )
func main() {
  pem_cert, _ := os.ReadFile("local-crt.pem")
  block, _ := pem.Decode(pem_cert)
  cert, _ := x509.ParseCertificate(block.Bytes)
  bjwt, _ := os.ReadFile("jwt.txt")
  jwt := string(bjwt)
  parts := strings.Split(jwt, ".")
  data := []byte(parts[0]+"."+parts[1])
  bsign, _ := base64.URLEncoding.DecodeString(parts[2])
  err := cert.CheckSignature(x509.SHA256WithRSA, data, bsign)
	fmt.Println(err)
}
```

Ruby
----

```ruby
```
