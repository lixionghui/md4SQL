

# 第一部分：常用函数

用 DUAL 系统表来做函数测试
```sql
SELECT * FROM DUAL;
SELECT ROUND(99.98) FROM DUAL;
```

## TRUNC() 截断函数



在这之前，先了解个关于时间日期的关键字 `date`，将文本转换为日期
```sql
SELECT date'2015-06-25' FROM DUAL;
SELECT date'2015-6-25' FROM DUAL;
```

### 获取当期系统时间

有了系统时间就可以，将其日期/时间作为动态变量了
```sql
SELECT SYSDATE FROM DUAL;
```

日期可以相加减；数值1代表1天
```sql
SELECT SYSDATE - 1 FROM DUAL;
SELECT date'2015-06-25' - date'2015-06-01' FROM DUAL;
```
### trunc() 日期 

> TRUNC(date,[fmt])日期

函数返回值还是日期格式
```sql
/*
format参数表：
   unit --单位        参数格式  valid format parameters
   Year                   SYYY,YYYY,YEAR,SYEAR,YYY,YY,Y
   ISO YEAR                                   IYYY,IY,I
   Quarter                                            Q
   Month                                MONTH,MON,MM,RM
   Week                                              WW
   IW                                                IW
   W                                                  W
   Day                                         DDD,DD,J
   Start day of week                           DAY,DY,D
   Hour                                    HH,HH12,HH24
   Minute                                            MI
*/
```

--trunc(date) 无format参数时，默认为 'dd', 返回“日”格式
SELECT TRUNC(SYSDATE) FROM DUAL;

---时间日期 trunc(date, [format]) 

    SELECT SYSDATE FROM dual;  
    --Output:04.06.2012 22:37:03  
      
    SELECT trunc(sysdate,'yyyy') FROM dual;
    SELECT trunc(sysdate,'Y') FROM dual;
    --Output:01.01.2012 00:00:00,返回当年第一天. 

    SELECT trunc(sysdate,'Q') FROM dual; 
    --Output:01.01.2012 00:00:00,返回当季第一天. 
      
    SELECT trunc(sysdate,'mm') FROM dual; 
    select trunc(sysdate,'MM') from dual; 
    --Output:01.06.2012 00:00:00 返回当月第一天.  
      
    SELECT trunc(sysdate,'d') FROM dual;  
    --Output:03.06.2012 00:00:00 返回当前星期的第一天. (周日；周日为第一天)

    SELECT trunc(sysdate,'iw') FROM dual;  --本周第一天（周一）
    SELECT trunc(sysdate,'d') + 1 - 7 FROM dual; --等价： 本周第一天（周一）

    SELECT trunc(sysdate,'w') FROM dual; --一周前的那天（往前推7天）

    SELECT trunc(sysdate,'WW') FROM dual; 
      
    SELECT trunc(sysdate,'dd') FROM dual;  
    --Output:04.06.2012 00:00:00 返回当前年月日  

    SELECT TRUNC(SYSDATE,'HH') FROM dual;  
    SELECT TRUNC(SYSDATE,'HH12') FROM dual;
    SELECT TRUNC(SYSDATE,'HH24') FROM dual;  


--跟时间相关的几个函数
  add_months(date, x) 
  --x任意整数，x > 0 则向后添加月份， x < 0 则往前倒数月份

----查询上月和去年同期上月
--昨天所在月的上月，月初第一天
SELECT add_months(trunc(sysdate-1,'mm'),-1) FROM dual;
--去年昨天所在月的上月，月初第一天
SELECT add_months(trunc(sysdate-1,'mm'),-13) FROM dual;

  last_day(date) --月末日期
SELECT LAST_DAY(SYSDATE) FROM DUAL;
--上个月月末
select trunc(last_day(add_months(sysdate-1, -1))) from dual;
SELECT TRUNC(SYSDATE,'MM') - 1 FROM DUAL;

--MONTHS_BETWEEN---返回两日期之间的月数,当data1  
    --格式: MONTHS_BETWEEN(data1,data2)  
    SELECT months_between(SYSDATE , date'2000-08-20') FROM dual;  
    


----与时间相关的函数，还和转化函数相关


----转换函数 
to_date(), to_char(), to_number()  

    --TO_DATE 转换字符串为日期型  
    --格式∶ TO_DATE(STRING[,’FORMAT’])  
    SELECT to_date('2012-02-01', 'yyyy-mm-dd') FROM dual;  
    SELECT To_Date('20150501', 'yyyymmdd') FROM DUAL;
    SELECT to_date('2014-01-08 15:27:20','yyyy-mm-dd HH24:mi:ss') FROM DUAL;--时间格式
    　　  
    --TO_CHAR 转换日期型或数值型为字符串。
    --最重要的函数之一．其FORMAT格式多种多样  
    --格式∶TO_CHAR(DATE [,’FORMAT’])  
    SELECT to_char(SYSDATE , 'yyyy-mm-dd') FROM dual;  
    SELECT TO_CHAR(SYSDATE, 'yyyy-mm') FROM DUAL;
    --RESULT "2015-06"
    SELECT TO_CHAR(SYSDATE, 'yyyymm') FROM DUAL;
    --RESULT "201506"

    --TO_NUMBER 转换字符串为数字  
    --格式∶TO_NUMBER(string [ , format])  
    SELECT to_number('9') FROM dual;  




--处理字符串的函数--

--|| CONCAT 并置运算符  
    --格式:CONCAT(STRING1, STRING2)  
    SELECT CONCAT('wang','lin') FROM dual;  
    SELECT 'wang'||'lin' FROM dual; 
    --
    SELECT 'wang&lin' FROM dual; --特殊&符号报错
    SELECT CONCAT(CONCAT('wang','&'),'lin') FROM dual;  
    SELECT 'wang'||'&'||'lin' from dual;

    --SUBSTR 提取子串 第二个参数为正的时候从左开始提取 为负时从右开始提取  
    --格式∶ SUBSTR(STRING , START [ , COUNT])  
    SELECT SUBSTR('wanglin',5,3) FROM dual;  
      
    --REPLACE 搜索指定字符串并替换  
    --格式∶REPLACE(string , substring , replace_string)  
    SELECT REPLACE('wanglin','n','m') FROM dual;  


    --- 。。。。。。 ---
--处理字符串的函数--
--ROUND 四舍五入
	SELECT　ROUND(9.7)　FROM　dual;  
	SELECT　ROUND(9.4)　FROM　dual;  
--CEIL 返回大于等于特定值的最小整数  
    --格式∶CEIL(value)  
    SELECT　CEIL(9.7)　FROM　dual;  


----实用函数-----

DECODE() 
类似与 
CASE FIELD WHEN X THEN Z1 WHEN Y THEN Z2 ELSE Z3 END

decode(m.biz_unit, 1, '自营', 3, '商城', '其他') as 业务单元
等价于
case m.biz_unit when 1 then  '自营' when 3 then '商城' else '其他' end as 业务单元
case when m.biz_unit = 1 then '自营' when m.biz_unit = 3 then '商城' else  '其他' end as 业务单元


	--自营-进口食品数据--顾客口径
	select m.mth_id 年月
	, decode(m.biz_unit, 1, '自营', 3, '商城', '其他') as 业务单元
	--, case m.biz_unit when 1 then  '自营' when 3 then '商城' else '其他' end as 业务单元
	--, case when m.biz_unit = 1 then '自营' when m.biz_unit = 3 then '商城' else  '其他' end as 业务单元
	, c1.categ_lvl1_name 一级类目
	, m.cust_num 顾客数
	, m.cust_num_new 新客数
	, m.ordr_num 成交订单数
	, m.net_amt 成交订单净额
	, m.pm_num 成交订单商品数量
	from bic.CUST_CRM_INFO_M m
	inner join dw.dim_categ_lvl1 c1 on m.categ_lvl1_id = c1.categ_lvl1_id
	where m.comb_type_id = 202
	and m.mth_id in (add_months(trunc(sysdate-1,'mm'),-1),add_months(trunc(sysdate-1,'mm'),-13))
	and m.biz_unit in (1,3)
	and m.categ_lvl1_id = 8644
	order by m.yr_mth desc
	;


--DECODE 补充
    --DECODE IF语句的另一形式。将输入数值与参数列表比较，返回对应值。
    --应用于将表的行转换成列以及IF语句无法应用的场合。
    --当与SIGN联合使用时功能扩展,可以判断大于小于的情况.  
    --格式: DECODE(input_value , value1 , result1 , value2 , result2 , ….defult_result)  
    SELECT DECODE(a.empno,1,100,2,300,500) FROM emp a;  
    --当VALUE=1时返回100　当VALUE=2时返回300 否则返回500  
      
    DECODE(SIGN(VALUES-100), -1,-10,1,10,0)  
    --当VALUE<100时返回-10  
    --当VALUE>100时返回10  
    --当VALUE=100时返回0  
      
    SELECT SUM(DECODE(EST_INT_KEY,77771,1,0)) A,  
           SUM(DECODE(EST_INT_KEY,77772,1,0)) B,  
    　　     SUM(DECODE(EST_INT_KEY,77773,1,0)) C  
    　　FROM PMS_BLK  






    --NVL 空值置换  
    --格式: NVL(value,替换值)  
    NVL(value,’nullvalue’)  
    --当value为NULL值时返回nullvalue否则返回value的值  




----第二部分：常用关键字----

--commit; 提交操作
--有些更改操作需要提交才能真正保存


--join
--关联的表，通常要求在关联条件下至少有一个表的记录是唯一的
--否则结果会多出很多行
--这就是大多数的 dim_维表需要添加  cur_flag = 1 这个条件
--在关联的时候，需要多想想/验证，被关联的表是否唯一



                CROSS JOIN：笛卡尔乘积（所有可能的行对）；
                INNER JOIN：仅对满足联接条件的 CROSS 中的列；
                LEFT OUTER JOIN：一个表满足条件的行，和另一个表的所有行；
                RIGHT OUTER JOIN：与 LEFT 相同，但两个表的角色互换；
                FULL OUTER JOIN：LEFT OUTER 和 RIGHT OUTER中所有行的超集。


--对外发布：子品
--对内分析：主品
SELECT decode(t1.biz_unit, 1, '自营', 3, '商城', '其他') 业务单元, 
       COUNT(DISTINCT prod.main_prod_id) 主品, 
       COUNT(DISTINCT prod.prod_id) 子品 
FROM   dw.dim_yhd_pm t 
INNER  JOIN dw.dim_prod prod 
ON     t.prod_id = prod.prod_id 
AND    prod.cur_flag = 1  -- 使得 dw.dim_prod 表每个 prod_id 只有一行记录
INNER  JOIN dw.dim_mrchnt t1 
ON     t.sale_mrchnt_id = t1.mrchnt_id 
AND    t1.biz_unit IN (1, 3) 
WHERE  t.cur_flag = 1 
AND    t.sale_flag = 1 
AND    t.show_flag = 1 
AND    t.sale_mrchnt_id <> 0 
GROUP  BY decode(t1.biz_unit, 1, '自营', 3, '商城', '其他');




--自连接：join ，inner join

--自连接  ：只返回两张表连接列的匹配项。
--以下三种查询结果一样。
select * from student s inner join class c on s.classid=c.id; 
select * from student s join class c on s.classid=c.id;
select * from student s,class c where s.classid=c.id;


--笛卡儿乘积：cross join

--笛卡儿乘积连接 ：即不加任何条件，达到 M*N 的结果集。
--以下两种查询结果一样。
select * from student s cross join class c;
select * from student,class;

--注意：如果cross join加上where s.classid=c.id条件，会产生跟自连接一样的结果：

--加上条件，产生跟自连接一样的结果。
select * from student s cross join class c where s.classid=c.id;



--左外连接：left join 

--左连接 ：列出左边表全部的，及右边表符合条件的，不符合条件的以空值代替。
--在(+)计算时，哪个带(+)哪个需要条件符合的，另一个全部的。即放左即右连接，放右即左连接。
--以下结果集相同。
select * from student s left join class c on s.classid=c.id;
select * from student s,class c where s.classid=c.id(+);

--右外连接：right join

--右外连接 ：与左连接一样，列出右边表全部的，及左边表符合条件的，不符合条件
--的用 空值  替代。
--(+)一样，它的位置与连接相反。
select * from student s right join class c on s.classid=c.id;
select * from student s,class c where s.classid(+)=c.id;


--全连接：full join
--全连接 ：产生M+N的结果集，列出两表全部的，不符合条件的，以空值代替。
select * from student s full join class c on s.classid=c.id;





--union ----------------------

-- union/union all运算：将查询的返回组合成一个结果， union all不过滤重复。

    SELECT product_id FROM order_items  
    UNION  
    SELECT product_id FROM inventories;  
      
    SELECT location_id  FROM locations   
    UNION ALL   
    SELECT location_id  FROM departments;  


-- intersect运算：返回查询结果中相同的部分。


    SELECT product_id FROM inventories  
    INTERSECT  
    SELECT product_id FROM order_items;  


-- minus运算：返回在第一个查询结果中与第二个查询结果不相同的那部分行记录。


    SELECT product_id FROM inventories  
    MINUS  
    SELECT product_id FROM order_items;  



--dbms_random.value 随机排序  rownum 

select col from
	(
	select col
	from table
	order by dbms_random.value --将结果随机排序
	) t 
where rownum < 20001 --从结果中取前面N行



select col_n from 
	(
	select col_n
	from table
	order by order_col desc --正常排序
	) t 
where rownum < 100 --从结果中取前面N行





--cube -- roll up -- groupping set

-- cube
-- roll up
-- groupping set

-- http://blog.csdn.net/t0nsha/article/category/938072/3


select case when grouping(biz_unit)=1 then '全站'
            when biz_unit= 1 then '自营'
            when biz_unit= 3 then '商城'
              else 'ohter'end 
         as biz_name
        , case when grouping(prod_biz_line_name) = 1 then '全部' else c1.prod_biz_line_name end 
        as prod_biz_line_name
        , case when grouping(categ_lvl1_name) = 1 then '全部' else c1.categ_lvl1_name end 
        as categ_lvl1_name
, sum(a.actl_sls_amt) as actl_sals_amt
, sum(a.actl_gp_amt) as sale_gp_amt
from hyc_sale_20141221_a a
inner join dw.v_dim_categ_lvl1_cur c1 on c1.categ_lvl1_id = a.categ_lvl1_id
group by cube(biz_unit, c1.prod_biz_line_name, c1.categ_lvl1_name)




--over()


--Oracle over函数

/*
http://www.cnblogs.com/umen/archive/2011/04/11/2012136.html
*/


--动销商品的销售占比
--select count(1) from bottom_list_sold_b1;
create table bottom_list_sold_b1 compress for archive high as
select  a1.pm_id
      , a1.mrchnt_id
      , a1.prod_id
      , c.categ_lvl3_id
      , sum(actl_sls_amt) over (partition by categ_lvl3_id, mrchnt_id order by actl_sls_amt desc) as cumulative
      , sum(actl_sls_amt) over (partition by categ_lvl3_id, mrchnt_id) as total
      , actl_sls_amt / (sum(actl_sls_amt) over (partition by categ_lvl3_id, mrchnt_id)) as pm_percent
      , (sum(actl_sls_amt) over (partition by categ_lvl3_id, mrchnt_id order by actl_sls_amt desc)) / (sum(actl_sls_amt) over (partition by categ_lvl3_id, mrchnt_id)) as xxx_percent
from bottom_list_sold_a1 a1
inner join dw.v_dim_prod_cur p on a1.prod_id = p.prod_id
inner join dw.v_hier_categ_cur c on c.categ_lvl_id = p.categ_id
where actl_sls_amt > 0 --退货不算
;
