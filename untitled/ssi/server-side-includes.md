# Server Side Includes

### config

```markup
<!--#config sizefmt="bytes" -->
```

### cookies

```markup
<!--#cookie get="C1" alt="hello" -->, 
display the value of the cookie "C1" or "hello" if the cookie 
is not in the incomming request.

<!--#cookie if="C1" then="hello" alt="bye"-->, 
display "hello" if the cookie "C1" is in the request. If not display "bye"
```

### **CountCommand**

This command inserts the number of recorded accesses to this resource, as reported by [CounterFilter](https://www.w3.org/Jigsaw/Doc/Reference/org.w3c.jigsaw.filters.CounterFilter.html).Parameters: **none**

```
<!--#hitcount -->
```

### **echo**

```markup
<!--#echo var="DOCUMENT_URI" -->
display the document uri

<!--#echo reqheader="referer"  -->
display the referer header of the request

<!--#echo reqstate="pathinfo"  -->
display the request state "pahtinfo"
```

### exec command

```
<!--#exec cmd="ls -lsa" -->
display the result of the ls command
```

### The standard **lastmod** SSI command.

```
<!--#flastmod-->
```

### **FSizeCommand**

```
<!--#fsize -->
```

### **IncludeCommand**

```markup
<!--#include file="included.html" -->
include the file "included.html" in the current file

<!--#include ifheader="Referer" file="included.html" else="included2.html" -->
if the request has a Referer header then include "included.html"
else include "included2.html"
```

### **jdbcCommand**

The SSI **jdbc** command allows you to query a SQL database via JDBC. Combinated with some [Control Commands](https://www.w3.org/Jigsaw/Doc/User/SSI.html#controls), it allows you to display the content of a database easyly.Parameters:

* **select** = the SQL request
* **url** = the database URL
* **driver** = the JDBC driver class
* **user** = the username
* **password** = the password
* **name** = the result name
* **column** = the column number
* **next** = a flag



```css
<!--#jdbc select="SELECT * FROM services" name="result"
    driver="com.imaginary.sql.msql.MsqlDriver" 
    url="jdbc:msql://www43.inria.fr:4333/services" -->
this is the setup of the command.

<!--#jdbc name="result" next="true" -->
this command move the pointer to the next line of the result set.

<!--#jdbc name="result" column="1" -->
display the first column of the current line.

<!--#jdbc name="result" column="2" -->
display the second column of the current line.

<!--#jdbc name="result" column="3" -->
display the third column of the current line.
```

### **ServletCommand**

The SSI **servlet** command. Servlet can be executed simply by providing a url path to a servlet class.Parameters:

* **name** = the command identifier
* **code** = the servlet URL
* **param** = a parameter name
* **value** = a parameter value

```
<!--#servlet name="Snoop" param="p1" value="v1" -->
<!--#servlet name="Snoop" param="p2" value="v2" -->
<!--#servlet name="Snoop" param="p3" value="v3" -->
<!--#servlet name="Snoop" code="/servlet/snoop" -->
```

### **CounterCommand**

```css
<!--#cpt name="cpt1" init="0" -->
Initialisation: cpt1 = 0

<!--#cpt name="cpt1" incr="1" -->
cpt1 = cpt1 + 1

<!--#cpt name="cpt1" value="true" -->
display the current value of cpt1
```
