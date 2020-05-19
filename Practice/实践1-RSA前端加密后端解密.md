## RSA 是什么
> RSA 是一种非对称加密算法，简单概括，就是加密和解密时使用不同的密钥进行。

## 问题
一般在进行WEB开发过程中，少不了用户登录功能的开发，用户在登录时需要输入用户名（或邮箱等其它唯一标识信息）和密码进行系统登录。如果密码通过明文的方式进行http传输并登录时，密码将能被人查看到。此时多数人会想到MD5编码，通过将密码进行MD5编码成无法解密的密文，则他人就算获取到该密文，也无法解密获取其原始密码。但后台需要获取该原始密码进行校验登录的操作，那么MD5编码不可取。搜索相关如何保证账号密码安全的文章，了解到RSA这种非对称加密算法。

## 方案确定
网上的许多Jsencrypt库进行前端加密，java后台解密的代码，但只适用于公钥和私钥确定的情况。本文为提高安全性，目标是后台动态生成公钥私钥对。
整体方案：后台动态生成RSA的密钥，将公钥发送给前端，并将私钥通过session保存在服务器，让前端进行加密操作后才将密文传给后端，后端使用对应私钥进行解密操作。
前端：TypeScript
后端：Java

## 前端（JavaScript/TypeScript）加密实践
前端进行RSA加密的第三方库采用 node-forge 库，其他如 Jsencrypt 库等暂时没有调试成功。

前端代码：
``` typescript
import * as forge from 'node-forge';

      // publicKey需要先通过http从后台获取，后台可以写一些geKey接口供前端调用

      const pki = forge.pki;

      // 规定格式：publicKey之前需要加'-----BEGIN PUBLIC KEY-----\n'，之后需要加'\n-----END PUBLIC KEY-----'
      const publicK = pki.publicKeyFromPem('-----BEGIN PUBLIC KEY-----\n' + publicKey + '\n-----END PUBLIC KEY-----');

      // forge通过公钥加密后一般会是乱码格式，可进行base64编码操作再进行传输，相应的，后台获取到密文的密码后需要先进行base64解码操作再进行解密
      const passwordCrypto =  forge.util.encode64(publicK.encrypt(password));
      
      // ... 后面就是进行常规的发送登录请求，不同的是，也需要将publicKey作为一个参数传输到后台，后台需要以此找到对应的私钥
```


## 后端（Java）解密实践
网上后端解密的代码很多，但质量无法确保，正好我使用的 Hutool 这个Java的工具库，其中包含了非对称加密的工具，可以直接使用。

Java代码：
``` java
/**
  * 获取秘钥-RSA
  * @return
  */
@RequestMapping(value = "/getKey",method = RequestMethod.POST)
@ResponseBody
public Result<String> getKeyOfRSA() {
    Result<String> result = new Result<>();

    RSA rsa = new RSA();
    String privateKeyBase64 = rsa.getPrivateKeyBase64();
    String publicKeyBase64 = rsa.getPublicKeyBase64();

    // 使用当前用户的session进行保存公钥私钥对
    Subject currentUser = SecurityUtils.getSubject();
    Session session = currentUser.getSession();
    session.setAttribute(publicKeyBase64, privateKeyBase64);
    return result.successWithData(publicKeyBase64);
}


/**
     * 解密password
     * @param password
     * @param publicKey
     * @return
     * @throws Exception
     */
    private String checkPassword(String password, String publicKey, String algorithm) throws Exception {
        Subject currentUser = SecurityUtils.getSubject();
        Session session = currentUser.getSession();

        // publicKey需要前端返回
        String privateKey = (String) session.getAttribute(publicKey);
        if(privateKey ==null){
            log.error("session中私钥失效.publickey={},password={}",publicKey,password);
            return null;
        }
        // 获取到私钥之后，需要将session中的该公钥私钥对信息移除
        session.removeAttribute(publicKey);
        // 构建，当只用私钥进行构造对象时，只允许使用该私钥进行加密和解密操作，本文只需要进行私钥解密，故只使用私钥构造对象
        RSA rsa = new RSA(privateKey, null);
        // 密码的密文先进行base64解码，之后再进行解密
        byte[] decrypt = rsa.decrypt(Base64.decode(password), KeyType.PrivateKey);
        String decryptStr = StrUtil.str(decrypt, CharsetUtil.CHARSET_UTF_8);
        
        return decryptStr;
    }
```
