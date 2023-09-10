# 常用

获取公网ip

```bash
$ curl ifconfig.me
$ curl icanhazip.com
$ curl ident.me
$ curl ipecho.net/plain
$ curl whatismyip.akamai.com
$ curl tnx.nl/ip
$ curl myip.dnsomatic.com
$ curl ip.appspot.com
```

隐藏操作历史执行 space+command

```bash
#edit .bash_profile add 
export HISTCONTROL=ignorespace
```

```
// Some code
unset HISTORY HISTFILE HISTSAVE HISTZONE HISTORY HISTLOG; export HISTFILE=/dev/null; export HISTSIZE=0; export HISTFILESIZE=0
```

```
// Some code
# echo > /var/log/wtmp
# echo > /var/log/btmp
# echo > /var/log/lastlog
```

test
