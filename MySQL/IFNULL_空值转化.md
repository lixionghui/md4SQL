
# 空值转化函数 IFNULL
`IFNULL(expr1,expr2)` 
>用法：如果expr1不是NULL，IFNULL()返回expr1，否则它返回expr2。IFNULL()返回一个数字或字符串值，取决于它被使用的上下文环境。



示例：
```sql
select IFNULL(NULL，0);  -- 0 
select IFNULL(1,0);  -- 1
select IFNULL(0,10); -- 0
select IFNULL(1/0,10); -- 10
select IFNULL(1/0,'yes'); -- 'yes'
```

将 `NULL` 转化为 `0` 是常见的操作，通常应用在某个字段上 `IFNULL(col, 0)`。

