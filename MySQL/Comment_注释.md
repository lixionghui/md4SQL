# Comment 注释

MySQL服务器支持3种注释风格：

* 从‘#’字符从行尾。
* 从‘-- ’序列到行尾。请注意‘-- ’(双破折号)注释风格要求第2个破折号后面至少跟一个空格符(例如空格、tab、换行符等等)。该语法与标准SQL注释语法稍有不同。
* 从/*序列到后面的*/序列。结束序列不一定在同一行中，因此该语法允许注释跨越多行。

下面的例子显示了3种风格的注释：
```sql
mysql> SELECT 1+1;     # This comment continues to the end of line

mysql> SELECT 1+1;     -- This comment continues to the end of line

mysql> SELECT 1 /* this is an in-line comment */ + 1;
```
