
* [<a href="#">json web token</a>](#json-web-token)
* [<a href="#">格式</a>](#格式)
  * [<a href="#">header</a>](#header)
  * [<a href="#">payload</a>](#payload)
  * [<a href="#">signature</a>](#signature)
  * [<a href="#">header.payload.signature</a>](#headerpayloadsignature)
* [<a href="#">特点</a>](#特点)


# [json web token](#)
json令牌
# [格式](#)
## [header](#)

- ```json
    {
        "alg": "HS256",
        "typ": "JWT"
    }
    ```
  
  - alg表示签名使用的算法，默认是HMAC SHA256（写成 HS256
  - typ属性表示这个令牌（token）的类型（type），JWT 令牌统一写为JWT
- 这个 JSON 对象也要使用 Base64URL 算法转成字符串
## [payload](#)
- Payload 部分也是一个 JSON 对象，用来存放实际需要传递的数据JWT 规定了7个官方字段，供选用，除了官方字段，你还可以在这个部分定义私有字段
  - ```json
    {
      "sub": "1234567890",
      "name": "John Doe",
      "admin": true
    }
    ```
- 这个 JSON 对象也要使用 Base64URL 算法转成字符串
## [signature](#)
- Signature 部分是对前两部分的签名，防止数据篡改。
- 首先，需要指定一个密钥（secret）。这个密钥只有服务器才知道，不能泄露给用户。然后，使用 Header 里面指定的签名算法（默认是 HMAC SHA256），按照下面的公式产生签名。
  - ```html
    HMACSHA256(base64UrlEncode(header) + "." + base64UrlEncode(payload), secret)
    ```
- 算出签名以后，把 Header、Payload、Signature 三个部分拼成一个字符串，每个部分之间用"点"（.）分隔，就可以返回给用户。
## [header.payload.signature](#)
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gR
G9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
```
# [特点](#)
- 无状态的
- 可扩展性
- 支持跨域认证