# Sign a POST using HMAC SHA256

## Python

```python
import base64
import hmac
import hashlib
keyBase64 = 'GzmVoVZJQ+O4SsnRzV3//g=='
keyBytes = base64.standard_b64decode(keyBase64)
# if using hexa format :
# keyHexa = '1b3995a1564943e3b84ac9d1cd5dfffe'
# keyBytes = bytes.fromhex(keyHexa)
print('binary key:', keyBytes) # b'\x1b9\x95\xa1VIC\xe3\xb8J\xc9\xd1\xcd]\xff\xfe'
print('key length:', len(keyBytes)) # 16
bodyString = '{"id":1,"name":"Gizmo","price":1.99}'
contentType = 'application/json'
contentLength = str(len(bodyString)) # 36
xRequestId = 'f058ebd6-02f7-4d3f-942e-904344e8cde5'
toSign = bodyString + contentType + contentLength + xRequestId
# {"Id":1,"Name":"Gizmo","Price":1.99}application/json36f058ebd6-02f7-4d3f-942e-904344e8cde5
print('content to sign:', toSign)
toSignBytes = bytearray(toSign,'utf8')
signatureBytes = hmac.new(keyBytes, toSignBytes, hashlib.sha256).digest()
signatureBase64 = str(base64.standard_b64encode(signatureBytes))
print('base64 signature:', signatureBase64) # b'dD7B2f0/4pyGlR7+MIVL7jcyuCqcyyOeLLzdPwv3m1E='
```

## Nodejs

```javascript
const crypto = require('crypto');
const keyBase64 = 'GzmVoVZJQ+O4SsnRzV3//g==';
const keyBytes = Buffer.from(keyBase64, 'base64');
// if using hexa format :
// const keyHexa = '1b3995a1564943e3b84ac9d1cd5dfffe';
// const keyBytes = Buffer.from(keyHexa, 'hex');
console.log('binary key:', keyBytes); // <Buffer 1b 39 95 a1 56 49 43 e3 b8 4a c9 d1 cd 5d ff fe>
console.log('key length:', keyBytes.length); // 16
const body = {id:1,name:"Gizmo",price:1.99};
const bodyString = JSON.stringify(body);
console.log('string body:', bodyString); // {"id":1,"name":"Gizmo","price":1.99}
const contentType = 'application/json';
const xRequestId = 'f058ebd6-02f7-4d3f-942e-904344e8cde5';
const toSign = bodyString + contentType + bodyString.length + xRequestId;
// {"id":1,"name":"Gizmo","price":1.99}application/json36f058ebd6-02f7-4d3f-942e-904344e8cde5
console.log('content to sign:', toSign);
const hmac = crypto.createHmac('sha256', keyBytes);
const signatureBase64 = hmac.update(toSign, 'utf8').digest('base64');
console.log('base64 signature:', signatureBase64); // dD7B2f0/4pyGlR7+MIVL7jcyuCqcyyOeLLzdPwv3m1E=
```

## Ruby

```ruby
require 'openssl'
require 'base64'
keyBase64 = 'GzmVoVZJQ+O4SsnRzV3//g=='
keyBytes = Base64.decode64(keyBase64)
# if using hexa format :
# keyHexa = '1b3995a1564943e3b84ac9d1cd5dfffe'
# keyBytes = keyHexa.scan(/../).map{|h| h.hex.chr}.join() # ruby n'a pas de conversion native hexa
puts 'key length: %d' % keyBytes.length # 16
bodyString = '{"id":1,"name":"Gizmo","price":1.99}'
contentType = 'application/json'
xRequestId = 'f058ebd6-02f7-4d3f-942e-904344e8cde5'
toSign = bodyString + contentType + bodyString.length.to_s() + xRequestId
# {"Id":1,"Name":"Gizmo","Price":1.99}application/json36f058ebd6-02f7-4d3f-942e-904344e8cde5
puts 'Content to sign: %s' % toSign
signatureBytes = OpenSSL::HMAC.digest("SHA256", keyBytes, toSign)
signatureBase64 = Base64.encode64(signatureBytes)
puts 'base64 signature: %s' % signatureBase64 # b'dD7B2f0/4pyGlR7+MIVL7jcyuCqcyyOeLLzdPwv3m1E='
```

## PHP CLI

```php
<?php
$keyBase64 = 'GzmVoVZJQ+O4SsnRzV3//g==';
$keyBytes = base64_decode($keyBase64);
# if using hexa format :
# $keyHexa = '1b3995a1564943e3b84ac9d1cd5dfffe';
# $keyBytes = hex2bin($keyHexa);
echo 'key length: ', strlen($keyBytes), "\n"; # 16
$bodyString = '{"id":1,"name":"Gizmo","price":1.99}';
$contentType = 'application/json';
$xRequestId = 'f058ebd6-02f7-4d3f-942e-904344e8cde5';
$toSign = $bodyString . $contentType . strlen($bodyString) . $xRequestId;
# {"Id":1,"Name":"Gizmo","Price":1.99}application/json36f058ebd6-02f7-4d3f-942e-904344e8cde5
echo 'Content to sign: ', $toSign, "\n";
$signatureBytes = hash_hmac('sha256', $toSign, $keyBytes, true);
$signatureBase64 = base64_encode($signatureBytes);
echo 'base64 signature: ', $signatureBase64, "\n"; # dD7B2f0/4pyGlR7+MIVL7jcyuCqcyyOeLLzdPwv3m1E=
```

## C#

```csharp
using System;
using System.Text;
using System.Security.Cryptography;
class Program {
static void Main(string[] args) {
try {
  var keyBase64 = "GzmVoVZJQ+O4SsnRzV3//g==";
  var keyBytes = Convert.FromBase64String(keyBase64);
  // if using hexa format :
  // var keyHexa = "1b3995a1564943e3b84ac9d1cd5dfffe";
  // var keyBytes = Convert.FromHexString(keyHexa); // Uniquement à partir de .NET5                                       
  Console.WriteLine("key length: " + keyBytes.Length); // 16
  var bodyString = "{\"id\":1,\"name\":\"Gizmo\",\"price\":1.99}";
  var contentType = "application/json";
  var xRequestId = "f058ebd6-02f7-4d3f-942e-904344e8cde5";
  var toSign = bodyString + contentType + bodyString.Length + xRequestId;
  // {"id":1,"name":"Gizmo","price":1.99}application/json36f058ebd6-02f7-4d3f-942e-904344e8cde5
  Console.WriteLine("content to sign: " + toSign);
  var toSignBytes = Encoding.ASCII.GetBytes(toSign);
  var hmac = new HMACSHA256(keyBytes);
  var signatureBase64 = Convert.ToBase64String(hmac.ComputeHash(toSignBytes));
  Console.WriteLine("base64 signature: " + signatureBase64); // dD7B2f0/4pyGlR7+MIVL7jcyuCqcyyOeLLzdPwv3m1E=
}
catch(Exception e) { Console.WriteLine(e); }
}
}
```

## Java 8

```java
import java.nio.charset.*;
import java.util.Base64;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
class Sign {
public static void main(String[] args) {
try {
  String keyBase64 = "GzmVoVZJQ+O4SsnRzV3//g==";
  byte[] keyBytes = Base64.getDecoder().decode(keyBase64);
  // Note : Java has no native hexa conversion
  System.out.println("key length: " + keyBytes.length); // 16
  String bodyString = "{\"id\":1,\"name\":\"Gizmo\",\"price\":1.99}";
  String contentType = "application/json";
  String xRequestId = "f058ebd6-02f7-4d3f-942e-904344e8cde5";
  String toSign = bodyString + contentType + bodyString.length() + xRequestId;
  // {"id":1,"name":"Gizmo","price":1.99}application/json36f058ebd6-02f7-4d3f-942e-904344e8cde5
  System.out.println("content to sign: " + toSign);
  byte[] toSignBytes = toSign.getBytes(StandardCharsets.US_ASCII);
  Mac hmac = Mac.getInstance("HmacSHA256");
  hmac.init(new SecretKeySpec(keyBytes,"HmacSHA256"));
  byte[] signatureBytes = hmac.doFinal(toSignBytes);
  String signatureBase64 = Base64.getEncoder().encodeToString(signatureBytes);
  System.out.println("base64 signature: " + signatureBase64); // dD7B2f0/4pyGlR7+MIVL7jcyuCqcyyOeLLzdPwv3m1E=
}
catch(Exception e) { System.out.println(e); }
}
}
```

## Go

```go
package main
import (
  "fmt"
  "encoding/base64"
  // "encoding/hex"
  "crypto/hmac"
  "crypto/sha256"
)
func main() {
  keyBase64 := "GzmVoVZJQ+O4SsnRzV3//g=="
  keyBytes, _ := base64.StdEncoding.DecodeString(keyBase64)
  // if using hexa format :
  // keyHexa := "1b3995a1564943e3b84ac9d1cd5dfffe"
  // keyBytes, _ := hex.DecodeString(keyHexa)
  fmt.Println("binary key:", keyBytes)
  fmt.Println("key length:", len(keyBytes)) // 16
  bodyString := "{\"id\":1,\"name\":\"Gizmo\",\"price\":1.99}"
  contentType := "application/json"
  xRequestId := "f058ebd6-02f7-4d3f-942e-904344e8cde5"
  toSign := fmt.Sprintf("%s%s%d%s", bodyString, contentType, len(bodyString), xRequestId)
  // {"id":1,"name":"Gizmo","price":1.99}application/json36f058ebd6-02f7-4d3f-942e-904344e8cde5
  fmt.Println("content to sign:", toSign)
  toSignBytes := []byte(toSign)
  hmac := hmac.New(sha256.New, keyBytes)
  hmac.Write(toSignBytes)
  signatureBytes := hmac.Sum(nil)
  signatureBase64 := base64.StdEncoding.EncodeToString(signatureBytes)
  fmt.Println("base64 signature:", signatureBase64) // dD7B2f0/4pyGlR7+MIVL7jcyuCqcyyOeLLzdPwv3m1E=
}
```

## Rust

```rust
// no hmac in rust std lib, using "ring" external one
use ring::hmac;
use base64;
fn main() {
  let body_string = "{\"id\":1,\"name\":\"Gizmo\",\"price\":1.99}";
  let content_type = "application/json";
  let request_id = "f058ebd6-02f7-4d3f-942e-904344e8cde5";
  let to_sign = [body_string, content_type, &body_string.len().to_string(), request_id].concat();
  println!("content to sign: {:?}", to_sign);
  let key_bytes = base64::decode("GzmVoVZJQ+O4SsnRzV3//g==").unwrap();
  let key = hmac::Key::new(hmac::HMAC_SHA256, &key_bytes);
  let tag = hmac::sign(&key, to_sign.as_bytes());
  let signature_bytes = tag.as_ref();
  let signature_base64 = base64::encode(signature_bytes);
  println!("base64 signature: {:?}", signature_base64);
}
```
