
# ��ֵת������ IFNULL
`IFNULL(expr1,expr2)` 
>�÷������expr1����NULL��IFNULL()����expr1������������expr2��IFNULL()����һ�����ֻ��ַ���ֵ��ȡ��������ʹ�õ������Ļ�����



ʾ����
```sql
select IFNULL(NULL��0);  -- 0 
select IFNULL(1,0);  -- 1
select IFNULL(0,10); -- 0
select IFNULL(1/0,10); -- 10
select IFNULL(1/0,'yes'); -- 'yes'
```

�� `NULL` ת��Ϊ `0` �ǳ����Ĳ�����ͨ��Ӧ����ĳ���ֶ��� `IFNULL(col, 0)`��

