---
title: JWT简介
toc: true
date: 2019-06-27 21:31:26
category: 后端
tags: 后端
---

JWT是JSON Web Token的缩写，是目前最流行的跨域认证解决方案。

<!--more-->

JWT是一个很长的字符串，中间用点分隔成三个部分。例如：

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjI5NTg5MTA4MDYsImlzcyI6InRlc3QiLCJuYmYiOjE0Nzk0NTczMTZ9.57gqtlk1nNezXSa0VgWBOwu2b2FCDJ6wXizuJF6IY10
```

三个部分依次如下

+ Header（头部）
+ Payload（负载）
+ Signature（签名）

### 1.Header

是一个JSON对象，描述JWT的元数据，通常是这样

```json
{
  "alg":"HS256",
  "typ":"JWT"
}
```

alg表示签名的算法，默认是HMAC SHA256(写成HS256)；

typ表示这个令牌的类型，JWT令牌统一写成JWT.

将上面JSON对象使用Base64URL算法转成字符串，得到这个部分。

### 2.Paload

也是JSON对象，存放实际需要传递的数据，规定了7个官方字段，供选用：

+ iss (issuer)：签发人
+ exp (expiration time)：过期时间
+ sub (subject)：主题
+ aud (audience)：受众
+ nbf (Not Before)：生效时间
+ iat (Issued At)：签发时间
+ jti (JWT ID)：编号

除了官方的还可以定义私有字段，下面就是一个例子

```json
{
  "sub": "1234567890",
  "name": "zhangsan",
  "admin": true
}
```

JWT默认不加密的，不要放秘密信息在这个部分。

这个对象同样用BASE64URL算法转成字符串。

### 3.Signature

这个部分是对前面两部分的签名，防止篡改数据。

首先，需要指定一个密钥，只有服务器知道，不能泄露，然后使用Header里指定的签名算法(默认HMAC SHA256)，按以下公式产生签名：

```
HMACSHA256(
	base64UrlEncode(header)+"."+
	base64UrlEncode(payload),
	secret
)
```

算出签名后，把 Header、Payload、Signature 三个部分拼成一个字符串，每个部分之间用"点"（`.`）分隔，就可以返回给用户。

## JWT 的使用方式

客户端收到服务器返回的 JWT，可以储存在 Cookie 里面，也可以储存在 localStorage。

此后，客户端每次与服务器通信，都要带上这个 JWT。你可以把它放在 Cookie 里面自动发送，但是这样不能跨域，所以更好的做法是放在 HTTP 请求的头信息`Authorization`字段里面。

```
Authorization: Bearer <token>
```

另一种做法是，跨域的时候，JWT 就放在 POST 请求的数据体里面。

## JWT的几个特点

（1）JWT 默认是不加密，但也是可以加密的。生成原始 Token 以后，可以用密钥再加密一次。

（2）JWT 不加密的情况下，不能将秘密数据写入 JWT。

（3）JWT 不仅可以用于认证，也可以用于交换信息。有效使用 JWT，可以降低服务器查询数据库的次数。

（4）JWT 的最大缺点是，由于服务器不保存 session 状态，因此无法在使用过程中废止某个 token，或者更改 token 的权限。也就是说，一旦 JWT 签发了，在到期之前就会始终有效，除非服务器部署额外的逻辑。

（5）JWT 本身包含了认证信息，一旦泄露，任何人都可以获得该令牌的所有权限。为了减少盗用，JWT 的有效期应该设置得比较短。对于一些比较重要的权限，使用时应该再次对用户进行认证。

（6）为了减少盗用，JWT 不应该使用 HTTP 协议明码传输，要使用 HTTPS 协议传输。

## Base64Url算法

Base64 有三个字符`+`、`/`和`=`，在 URL 里面有特殊含义，所以要被替换掉：`=`被省略、`+`替换成`-`，`/`替换成`_` 。这就是 Base64URL 算法。



参考转自：<http://www.ruanyifeng.com/blog/2018/07/json_web_token-tutorial.html>