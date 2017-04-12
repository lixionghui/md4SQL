

注释：Ctrl+K、Ctrl+C （按住Ctrl,然后K、C）

取消注释：Ctrl+K、Ctrl+U（按住Ctrl,然后K、U）

### How to drop a table if it exists in SQL Server?

物理表
```sql
IF OBJECT_ID('dbo.Scores', 'U') IS NOT NULL 
  DROP TABLE dbo.Scores; 
```

临时表
```sql
IF OBJECT_ID('tempdb.dbo.#T', 'U') IS NOT NULL
  DROP TABLE #T; 
```

## 时间日期

### Trunc_Date
```sql
--当前日期： 2013-12-31 
select convert(varchar(10), getdate(),120) 

--当前日期+ 时间：2013-12-31 14：36：46.860
select getdate()  
  
--一个月的第一天：2013-12-31 00：00：00.000  
select dateadd(mm,datediff(mm,0,getdate()),0)  
  
--本周的星期一：2013-12-30 00：00：00.000 
select dateadd(wk,datediff(wk,0,getdate()),0)  
  
-- 一年的第一天：2013-01-01 00：00：00.000 
select dateadd(yy,datediff(yy,0,getdate()),0)  
  
-- 季度的第一天：2013-10-01 00：00：00.000   
select dateadd(qq,datediff(qq,0,getdate()),0)  
  
-- 上个月的最后一天：2013-11-31 23：59：59.997 
select dateadd(ms,-3,dateadd(mm, datediff(mm,0,getdate()), 0))  
  
--去年的最后一天：2012-12-31 23：59：59.997  
select dateadd(ms,-3,dateadd(yy, datediff(yy,0,getdate()), 0))  
   
--本月的最后一天：2013-12-31 23：59：59.997   
select dateadd(ms,-3,dateadd(mm, datediff(m,0,getdate())+1, 0))  
  
--本年的最后一天：2013-12-31 23：59：59.997   
select dateadd(ms,-3,dateadd(yy, datediff(yy,0,getdate())+1, 0))  
   
--本月的第一个星期一：2013-12-02 00：00：00.000   
select dateadd(wk, datediff(wk,0, dateadd(dd,6-datepart(day,getdate()),getdate())), 0) 
```
