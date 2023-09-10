# mysql unicode 转中文 func

```sql
DROP FUNCTION IF EXISTS STRINGDECODE;
DELIMITER //

CREATE FUNCTION STRINGDECODE(str TEXT CHARSET utf8)
RETURNS text CHARSET utf8 DETERMINISTIC
BEGIN
declare pos int;
declare escape char(6) charset utf8;
declare unescape char(3) charset utf8;
set pos = locate('\\u', str);
while pos > 0 do
    set escape = substring(str, pos, 6);
    set unescape = char(conv(substring(escape,3),16,10) using ucs2);
    set str = replace(str, escape, unescape);
    set pos = locate('\\u', str, pos+1);
end while;
return str;
END//

DELIMITER ;

```
