JWT signature check 
===================

Simple examples of JWT signature checks in different languages using only standard libraries where possible to show how it works, using RSA-SHA256.

Note that JWT dedicated libraries exists, but here we want to show quick samples not requiring external dependencies.

This is not production grade : no error management. Indentation is removed.

We consider that JWT is in a text file, and public key from a certificate file.

Reminder
--------

JWT is composed of 3 base64url parts separated by a dot '.'
- header as JSON, ex: `{"alg":"RS56","typ":"JWT"}`
- content as JSON
- signature, ex: 256 Bytes when sign key is 2048 bits (256 Bytes), so 340 Bytes base64 (base64url does not require '=' padding)

JWT is often found in the Authorization HTTP header, as a Bearer token, remember to remove the `Bearer` prefix : `Authorization: Bearer <JWT>`

Signed data is the JWT without the signature : base64 header + '.' + base64 content

Algo with 'HS' are symmetric HMAC, should not be used unless key is only for one to one dedicated JWT.

'RS' and 'JS' algos are asymmetric RSA, 'JS' (JSS padding instead of PKCS7 one) is more secure but less common.

Nodejs
------

```javascript
const fs = require('fs')
const crypto = require('crypto')
const jwt = fs.readFileSync('jwt.txt', {encoding:'ascii'})
const parts = jwt.split('.')
const tocheck = parts[0]+'.'+parts[1]
const sign = Buffer.from(parts[2], 'base64')

const pem = fs.readFileSync('cert.pem',{encoding:'ascii'})
const cert = new crypto.X509Certificate(pem)
const verif = crypto.verify('RSA-SHA256', tocheck, cert.publicKey, sign)
console.log(verif)
```

NB: yes, I do not put ';' at end of javascript lines, feels more readable

Ruby
----

```ruby
require 'openssl'
require 'base64'
jwt = File.read 'jwt.txt'
parts = jwt.split('.')
tocheck = parts[0]+'.'+parts[1]
sign = Base64.urlsafe_decode64(parts[2])

cert = OpenSSL::X509::Certificate.new File.read 'cert.pem'
verif = cert.public_key.verify(OpenSSL::Digest::SHA256.new, sign, tocheck)
puts verif
```

Python
------

Python standard library has no way to check RSA signatures, needs external libraries as pyopenssl or pca/cryptography (both relying above openssl lib)

Python base64url requires proper '=' padding

```python
import base64
jwt = open("jwt.txt","r").read()
parts = jwt.split('.')
tocheck = (parts[0]+'.'+parts[1]).encode()
sign64 = parts[2].ljust(len(sign64)+(len(sign64)%4),'=')
sign = base64.urlsafe_b64decode(sign64)
```

```python
# https://www.pyopenssl.org/en/20.0.1/api/crypto.html
# pip install openssl
from  OpenSSL import crypto
pem = open("cert.pem","rb").read()
cert = crypto.load_certificate(crypto.FILETYPE_PEM, pem)
verif = crypto.verify(cert, sign, tocheck, 'sha256')
print(verif, 'None means OK, else exception is raised')
```

```python
# pip install cryptography
from cryptography.hazmat.backends import default_backend
from cryptography.hazmat.primitives import hashes
from cryptography.hazmat.primitives.asymmetric import padding
from cryptography.hazmat.primitives.serialization import load_pem_public_key
pem = open("pubkey.pem","rb").read()
pubkey = load_pem_public_key(pem, backend=default_backend())
verif = pubkey.verify(sign, tocheck, padding.PKCS1v15(), hashes.SHA256())
print(verif, 'None means OK, else exception is raised')
```

Java
----

Using Java 8

```java
import java.io.FileInputStream;
import java.nio.file.*;
import java.nio.charset.*;
import java.util.Base64;
import java.security.*;
import java.security.cert.*;
class Test {
public static void main(String[] args) {
try {

String jwt = new String(Files.readAllBytes(Paths.get("jwt.txt")));
String[] parts = jwt.split("\\.");
byte[] tocheck = (parts[0]+"."+parts[1]).getBytes(StandardCharsets.UTF_8);
byte[] sign = Base64.getUrlDecoder().decode(parts[2]);

FileInputStream fis = new FileInputStream("cert.pem");
PublicKey pubKey = CertificateFactory.getInstance("X.509").generateCertificate(fis).getPublicKey();
fis.close();
Signature s = Signature.getInstance("SHA256withRSA");
s.initVerify(pubKey);
s.update(tocheck);
System.out.println(s.verify(sign));

}
catch(java.io.IOException | CertificateException | SignatureException | InvalidKeyException | NoSuchAlgorithmException e) {
System.out.println(e);
}
}
}
```

C#
----

Using C# 5 on dotnet fmk 8, there is no base64url, so convert to base64 format

```csharp
using System;
using System.Text;
using System.IO;
using System.Security.Cryptography;
using System.Security.Cryptography.X509Certificates;
class Program {
static void Main(string[] args) {
try {

var jwt = File.ReadAllText("jwt.txt");
var parts = jwt.Split('.');
var tocheck = Encoding.ASCII.GetBytes(parts[0]+"."+parts[1]);
var sign64 = parts[2].Replace("_","/").Replace("-","+").PadRight(sign64.Length+(sign64.Length%4),'=');
var sign = Convert.FromBase64String(sign64);

var cert = new X509Certificate2("cert.pem");
var pubkey = cert.GetRSAPublicKey();
var verif = pubkey.VerifyData(tocheck, sign, HashAlgorithmName.SHA256, RSASignaturePadding.Pkcs1);
Console.WriteLine(verif);

}
catch(Exception e) {
Console.WriteLine(e);
}
}
}
```

Go
--

```go
package main
import ( "fmt" ; "os" ;  "strings" ; "encoding/base64" ; "encoding/pem" ; "crypto/x509" )
func main() {

bjwt, _ := os.ReadFile("jwt.txt")
jwt := string(bjwt)
parts := strings.Split(jwt, ".")
tocheck := []byte(parts[0]+"."+parts[1])
sign, _ := base64.URLEncoding.DecodeString(parts[2])

pem_cert, _ := os.ReadFile("cert.pem")
block, _ := pem.Decode(pem_cert)
cert, _ := x509.ParseCertificate(block.Bytes)
err := cert.CheckSignature(x509.SHA256WithRSA, tocheck, sign)
fmt.Println(err)

}
```
