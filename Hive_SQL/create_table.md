
```sql
create table page_view  
(  
page_id bigint comment '页面ID',  
page_name string comment '页面名称',  
page_url string comment '页面URL'  
)  
comment '页面视图'  
partitioned by (ds string comment '当前时间，用于分区字段')  
row format delimited  
stored as rcfile  
location '/user/hive/test';  
```
