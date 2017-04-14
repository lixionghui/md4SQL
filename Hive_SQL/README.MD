


## 日期时间 


**to_date 日期时间转日期函数**

to_date(string timestamp)   返回值: int 返回值:   string

说明: 返回日期时间字段中的日期部分。

```sql
select to_date('2011-12-08 10:03:01') from dual; -- 2011-12-08
```
---

**datediff 日期比较函数**

datediff(string enddate, string startdate) 返回值: int

说明: 返回结束日期减去开始日期的天数。

```sql
select datediff('2012-12-08','2012-05-09') from dual; -- 213
```

---

**date_add 日期增加函数**

date_add(string startdate, int days)  返回值: string

说明: 返回开始日期startdate增加days天后的日期。

```sql
select date_add('2012-12-08',10) from dual; -- 2012-12-18
```


**date_sub 日期减少函数**

date_sub(string startdate, int days) 返回值: string

说明: 返回开始日期startdate减少days天后的日期。

```sql
select date_sub('2012-12-08',10) from dual; -- 2012-11-28
```
