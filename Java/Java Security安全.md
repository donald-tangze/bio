# notes

[Money](https://engineertang.github.io/notes/Money)

[macOS Essential](https://engineertang.github.io/notes/macOS%20Essential)

[Spring Bean Lifecycle](https://engineertang.github.io/notes/Spring Bean Lifecycle)

[mac开发工具使用](https://engineertang.github.io/notes/mac开发工具使用)

### java安全的开发者指导

https://docs.oracle.com/en/java/javase/18/security/index.html

> Java security technology, tools, and implementations of commonly used security algorithms, mechanisms, and protocols on the Java Platform, Standard Edition (Java SE).

5.Java Security

#### 1. Public-key cryptography

公开密钥加密（**Public-key cryptography**），又叫非对称加密：如RSA，它需要兩個[密钥](https://zh.wikipedia.org/wiki/密钥)，一個是公開密鑰，另一個是私有密鑰；公鑰用作加密，私鑰則用作解密。 

Public Key

Private Key

####  2.Digital Signature   **數位簽章**

（英語：**Digital Signature**，又称**公鑰數位簽章**）是一種功能類似写在[纸](https://zh.wikipedia.org/wiki/纸)上的普通[签名](https://zh.wikipedia.org/wiki/签名)、但是使用了[公钥加密](https://zh.wikipedia.org/wiki/公钥加密)领域的技术，以用于鉴别数字訊息的方法。一套数字签名通常會定义两种互补的运算，一个用于签名，另一个用于验证。在数字签名中，會使用私钥加密（相当于生成签名），公钥解密（相当于验证签名）。

#### 3. [public key certificates](https://en.wikipedia.org/wiki/Public_key_certificate)

X509 defines the format of public-key certificates. The certificates are used in many internet protocols like TLS, SSL. 

**X.509**是密码学里[公钥证书](https://zh.wikipedia.org/wiki/公钥证书)的格式标准。



#### 4.[KeyTool](https://docs.oracle.com/javase/6/docs/technotes/tools/solaris/keytool.html)

```shell
 keytool -genkeypair -dname "cn=Don Tang, ou=JavaSoft, o=Sun, c=HK" -alias swift -keypass kpi123 -keystore "swift.jks"  -storepass kpi123 -validity 180  -keyalg RSA
```



-w3.org/2001/84/xmlenc#sha256"›</ds:DigestMethod›<ds:DigestValue»UUttAsyXPU
BSNy/ploos=</ds:DigestValue›</ds:Reference›</ds:SignedInfo›ds:SignatureValue›J0P1aUd7WFH01sDNort7ke10851SeriSaad,4

```
<ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
        <ds:SignedInfo>
            <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"></ds:CanonicalizationMethod>
            <ds:SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#hmac-sha256"></ds:SignatureMethod>
            <ds:Reference URI="">
                <ds:Transforms>
                    <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"></ds:Transform>
                    <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"></ds:Transform>
                </ds:Transforms>
                <ds:DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256"></ds:DigestMethod>
                <ds:DigestValue>7CUUMGNW8O5A89mIQv0DnnC3YhvKZ3jqLMJrXfQxCmI=</ds:DigestValue>
            </ds:Reference>
        </ds:SignedInfo>
    </ds:Signature>
```
