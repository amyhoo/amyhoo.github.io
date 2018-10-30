---
tags: [sql]
categories: database 	
---

# management
## tables ,columns info
```
# postgresql
select * from information_schema.columns

# check if all table contains essential columns
select table_name from 
(select * from information_schema.columns  where table_catalog='db'  and table_schema='net' and column_name in ('delete_flag','create_time','update_time','create_user','update_user' )) as T1
group by table_name having count(table_name)<5  
```

# data structure
## category
### 基础数据
#### 机构tree结构表
```
postgres=# drop table xxorg;
DROP TABLE
postgres=# create table xxorg(id int8,name varchar(100),parentid int8);
CREATE TABLE
postgres=# insert into xxorg(id,name,parentid)values(1,'总部',0);
 insert into xxorg(id,name,parentid)values(10,'A分公司',1),(20,'B分公司',1);
 insert into xxorg(id,name,parentid)values(100,'AA经营部',10),(110,'AB经营部',10),(200,'BA经营部',20);
 insert into xxorg(id,name,parentid)values(1000,'AAA办事处',100),(2000,'BAA办事处',200);

postgres=# \d
        List of relations
 Schema | Name | Type  |  Owner   
--------+------+-------+----------
 public | xxorg | table | postgres
(1 row)
postgres=#
postgres=#
postgres=# select * from xxorg;
  id  |   name    | parentid 
------+-----------+----------
    1 | 总部      |        0
   10 | A分公司   |        1
   20 | B分公司   |        1
  100 | AA经营部  |       10
  110 | AB经营部  |       10
  200 | BA经营部  |       20
 1000 | AAA办事处 |      100
 2000 | BAA办事处 |      200
(8 rows)

```
#### 用户机构表
```
postgres=# create table xxuserorg(userid varchar(100),orgid int8);
CREATE TABLE
postgres=# insert into xxuserorg(userid,orgid)values('user1',1),('user2',10),('user3',100),('user3',110),('user4',2000);
INSERT 0 5
postgres=#
postgres=#
postgres=# select * from xxuserorg;
 userid | orgid 
--------+-------
 user1  |     1
 user2  |    10
 user3  |   100
 user3  |   110
 user4  |  2000
(5 rows)
```
### 初步写法
#### 向上递归
```
postgres=# with recursive tmp0 as
(  
SELECT id,name,parentid
FROM xxorg
where id = 200 --初始化节点
union
SELECT t1.id,t1.name,t1.parentid
FROM xxorg t1,  
     tmp0 t0  
where 1=1
  and t1.id=t0.parentid
)  
SELECT id,name,parentid   
FROM tmp0;  

 id  |   name   | parentid 
-----+----------+----------
 200 | BA经营部 |       20
  20 | B分公司  |        1
   1 | 总部     |        0
(3 rows)
	
```

#### 向下递归
```
postgres=# with recursive tmp0 as
(  
SELECT id,name,parentid
FROM xxorg
where id = 200 --初始化节点
union
SELECT t1.id,t1.name,t1.parentid
FROM xxorg t1,  
     tmp0 t0  
where 1=1
  and t1.parentid=t0.id  
)  
SELECT id,name,parentid   
FROM tmp0; 

  id  |   name    | parentid 
------+-----------+----------
  200 | BA经营部  |       20
 2000 | BAA办事处 |      200
(2 rows)	
```

不管是向上递归还是向下递归，符合需求的数据都筛选出来了，只是没有层级，不太直观。
最好有类似oracle 的 tree 结构的功能。

###修改后写法
#### 向上递归 修改后
```
postgres=# with recursive tmp0(id,name,parentid,path,depth) as
(  
SELECT id,name,parentid,array[id] as path,1 as depth
FROM xxorg
where id in (select orgid from xxuserorg where userid='user2') --初始化节点
union
SELECT t1.id,t1.name,t1.parentid,t1.id||t0.path,t0.depth+1 as depth
FROM xxorg t1,  
     tmp0 t0
where 1=1
  and t1.id=t0.parentid
)  
SELECT id,name,parentid,path,depth   
FROM tmp0
order by depth desc,id
;  

```

#### 向下递归 修改后
```
postgres=# with recursive tmp0 as
(  
SELECT id,name,parentid,array[id] as path,1 as depth
FROM xxorg
where id in (select orgid from xxuserorg where userid='user2') --初始化节点
union
SELECT t1.id,t1.name,t1.parentid,t0.path||t1.id,t0.depth+1 as depth
FROM xxorg t1,  
     tmp0 t0  
where 1=1
  and t1.parentid=t0.id  
)  
SELECT id,name,parentid,path,depth    
FROM tmp0
order by depth,id
; 
	
```

### 整合后的最终sql
```
postgres=# with recursive tmp0(id,name,parentid,path,depth) as (  
    --向上递归
	SELECT id,name,parentid,array[id] as path,1 as depth
	  FROM xxorg
	 where id in (select orgid from xxuserorg where userid='user1') --初始化节点
	union
	SELECT t1.id,t1.name,t1.parentid,t1.id||t0.path,t0.depth+1 as depth
	  FROM xxorg t1,  
		   tmp0 t0
	 where 1=1
	   and t1.id=t0.parentid
), tmp1 (id,name,parentid,path,depth) as (  
	--向下递归
	SELECT id,name,parentid,array[id] as path,1 as depth
	  FROM xxorg
	 where id in (select orgid from xxuserorg where userid='user1') --初始化节点
	union
	SELECT t1.id,t1.name,t1.parentid,t0.path||t1.id,t0.depth+1 as depth
	  FROM xxorg t1,  
	  	   tmp1 t0  
	 where 1=1
	   and t1.parentid=t0.id  
), tmp2 as ( 
--涉及到的所有有权限的机构
	SELECT id,name,parentid   
	  FROM tmp0
	union 
	SELECT id,name,parentid  
	  FROM tmp1
), tmp3 (id,name,parentid,path,depth) as (
	--再次对过滤出的机构向下递归，构成tree
	SELECT id,name,parentid,array[id] as path,1 as depth
	  FROM tmp2
	 where parentid = 0 --这里一定要为root节点，否则出错
	union
	SELECT t1.id,t1.name,t1.parentid,t0.path||t1.id,t0.depth+1 as depth
	  FROM tmp2 t1,  
	       tmp3 t0
	 where 1=1
	   and t1.parentid=t0.id
)
select a0.id,a0.name,a0.parentid,
       '/'||array_to_string(a0.path,'/') as path,
	   a0.depth,
	   lpad(a0.name, 2*a0.depth-1+length(a0.name),' ') as tree_name,
	   --原始维护的机构
	   case when a0.id = a1.orgid then '*' else null end as orgid_original,
	   --该节点的子节点自动继承父权限
	   case when position( a1.prefix_orgid in '/'||array_to_string(path,'/')||'/' ) >0 then '+' end as orgid_extend
  from tmp3 a0
       left outer join (select distinct '/'||orgid||'/' as prefix_orgid,orgid
	                      from xxuserorg
						 where 1=1
						   and userid='user1'
						   and orgid is not null ) a1
	                on position( a1.prefix_orgid in '/'||array_to_string(path,'/')||'/' ) >0
order by '/'||array_to_string(path,'/'),a0.depth  
; 

  id  |   name    | parentid |      path      | depth |    tree_name     | orgid_original | orgid_extend 
------+-----------+----------+----------------+-------+------------------+----------------+--------------
    1 | 总部      |        0 | /1             |     1 |  总部            | *              | +
   10 | A分公司   |        1 | /1/10          |     2 |    A分公司       |                | +
  100 | AA经营部  |       10 | /1/10/100      |     3 |      AA经营部    |                | +
 1000 | AAA办事处 |      100 | /1/10/100/1000 |     4 |        AAA办事处 |                | +
  110 | AB经营部  |       10 | /1/10/110      |     3 |      AB经营部    |                | +
   20 | B分公司   |        1 | /1/20          |     2 |    B分公司       |                | +
  200 | BA经营部  |       20 | /1/20/200      |     3 |      BA经营部    |                | +
 2000 | BAA办事处 |      200 | /1/20/200/2000 |     4 |        BAA办事处 |                | +
(8 rows)

```


## the schema update
```
with tmp_sch as (
  select 'au75'::text as schema1,
         'au169'::text as schema2,
         '根据75 更改 169 的'::text as memo
),tmp_tab as (
   select c.table_name,
          max(case when c.table_schema in (select schema1 from tmp_sch) then c.table_schema else null end ) as schema_au1,
          max(case when c.table_schema in (select schema2 from tmp_sch) then c.table_schema else null end ) as schema_au2
     from information_schema.tables c
    where 1=1
      and c.table_schema in (select schema1 from tmp_sch union select schema2 from tmp_sch )
    group by c.table_name
    order by 2 nulls first,3 nulls first,c.table_name
),tmp_col as (
	select 'alter table '||c.table_schema||'.'||c.table_name||' add column '||c.column_name||' '||
	       case when c.data_type in ('character','character varying') then c.data_type||'('||c.character_maximum_length||') ' 
	            when c.data_type in ('timestamp without time zone') then  c.data_type||' '
	            when c.data_type in ('smallint','integer') then  c.data_type||' '
	            when c.data_type in ('numeric') then c.data_type||'('||c.numeric_precision||','||c.numeric_scale||') ' 
	        end||
	        case when c.is_nullable='YES' then ' null '
	             when c.is_nullable='NO' then ' not null '
	         end ||
	         case when c.column_default is null then ' '
	              else ' DEFAULT '||c.column_default
	         end ||
	         ' ;' as add_column,
	        'alter table '||c.table_schema||'.'||c.table_name||' drop column '||c.column_name||' ;' drop_column,
	         
	        c.table_schema,
	        c.table_name,
	        c.column_name,
	        c.ordinal_position,
	        c.data_type
	        --c.* 
	from information_schema.columns c
	where 1=1
	and c.table_schema in (select schema1 from tmp_sch union select schema2 from tmp_sch)
	--and c.table_name='au_servers_his'
	order by c.table_schema,c.table_name,c.ordinal_position
)
select (select memo from tmp_sch) as memo,tab.table_name::text,''::text as column_name,tab.schema_au1::text,tab.schema_au2::text,
       'create table'::text as tab_result,
       ''::text as col_result
  from tmp_tab tab
 where 1=1
   and (tab.schema_au1 is null or schema_au2 is null )
union all 
select '##########'::text,'##########'::text,'##########'::text,'##########'::text,'##########'::text,'##########'::text,'##########'::text
union all
select 
      (select memo from tmp_sch) as memo,
      t0.table_name,
      t0.column_name,
      t0.schema_au1,
      t0.schema_au2,
      t0.tab_result,
      case when t0.schema_au1 is null and t0.schema_au2 is not null then t0.drop_col_result2
           when t0.schema_au1 is not null and t0.schema_au2 is null then 'alter table '||(select schema2 from tmp_sch limit 1)||'.'||substring(t0.add_col_result1 from (12+(select length(schema1) from tmp_sch limit 1)+2) for length(t0.add_col_result1)-(12+(select length(schema1) from tmp_sch limit 1)+1))
           else 'i do no know'
       end as col_result
from (
	select col.table_name::text,col.column_name::text,
	       max(case when col.table_schema in (select schema1 from tmp_sch) then col.table_schema else null end )::text as schema_au1,
	       max(case when col.table_schema in (select schema2 from tmp_sch) then col.table_schema else null end )::text as schema_au2,
	       ''::text as tab_result,
	       max(case when col.table_schema in (select schema1 from tmp_sch) then col.add_column else null end )::text as add_col_result1,
	       max(case when col.table_schema in (select schema2 from tmp_sch) then col.add_column else null end )::text as add_col_result2,
	       max(case when col.table_schema in (select schema1 from tmp_sch) then col.drop_column else null end )::text as drop_col_result1,
	       max(case when col.table_schema in (select schema2 from tmp_sch) then col.drop_column else null end )::text as drop_col_result2
	 from tmp_col col
	where 1=1
	  and col.table_name not in (
	     select distinct tab.table_name
		  from tmp_tab tab
		 where 1=1
		   and (tab.schema_au1 is null or schema_au2 is null )
	  )
	group by col.table_name,col.column_name
	having ( max(case when col.table_schema in (select schema1 from tmp_sch) then col.table_schema else null end )::text is null 
	      or max(case when col.table_schema in (select schema2 from tmp_sch) then col.table_schema else null end )::text is null
	     )
	order by col.table_name,col.column_name
	) t0
;
```