# Smart management system front-end SQL injection vulnerability

BUG_Author: Murasaki

Vulnerable website:

- https://110.191.213.249:8443
- https://113.9.192.214:8443
- http://113.140.35.86:8443
- http://60.29.117.204:8443/
- http://103.121.164.62:8443/
- https://221.178.130.210:8443/
- https://117.28.240.102:8443/
- https://221.216.94.123:8443/

Vulnerable URI:

* /importexport.php

There are many other websites. Here are some examples of assets on the public Internet.

Link:https://www.byzoro.com/



Vulnerability discovery process：

The system has a log export function. When exporting, the data package contains two parameters, sql and tab. The sql parameter is the URL and base64-encoded SQL query statement, and tab is the table to be operated on.

![image-20240202144946382](https://github.com/1MurasaKi/Smart_SQKi/blob/main/1.png)

![image-20240202144951675](https://github.com/1MurasaKi/Smart_SQKi/blob/main/2.png)

So operations can be performed at these two parameters.

Query statement 

```sql
select * from information_schema.SCHEMATA --
```

After encoding, pass in the parameter sql and modify the tab.

![image-20240202145037668](https://github.com/1MurasaKi/Smart_SQKi/blob/main/3.png)

At this time, you can see that the content of the information_schema.SCHEMATA table has been queried, and I have deleted the cookie, and the content can still be queried. Therefore, it is determined that the interface is unauthorized and SQL injection can be performed.
