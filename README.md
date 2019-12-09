# Shiro-1.4.1-RCE
Shiro&lt;=1.4.1 padding oracle attack导致RCE

### 0x01 原理
cookie的cookiememeMe已通过AES-128-CBC模式加密，这很容易受到填充oracle攻击的影响。攻击者可以使用有效的RememberMe cookie作为Padding Oracle Attack 的前缀，然后制作精心制作的RememberMe来执行Java反序列化攻击，例如SHIRO-550。

### 0x02 重现此问题的步骤：

* 登录网站，并从cookie中获取RememberMe。
* 使用RememberMe cookie作为Padding Oracle Attack的前缀。
* 加密syserial的序列化有效负载，以通过Padding Oracle Attack制作精心制作的RememberMe。
* 请求带有新的RememberMe cookie的网站，以执行反序列化攻击。
* 攻击者无需知道RememberMe加密的密码密钥。


### 0x03 影响

* 1.2.4<shiro<=1.4.1

### 0x04 参考链接

* https://issues.apache.org/jira/browse/SHIRO-721
* http://www.svenbeast.com/post/-leT8b8Kh/
