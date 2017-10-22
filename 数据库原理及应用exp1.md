#create database

use master 
go
create database toyunivers
on primary
(
name=toyunvers_Data,
filename='d:\test\toyunvers_Data_MDF',
size=10,
maxsize=unlimited,
FILEGROWTH = 5
)
log on
(
name=toyunivers_Log,
filename='d:\test\toyunvers_Log_LDF',
size=10,
maxsize=200,
FILEGROWTH = 5%
)
go

#craet table

use toyunivers
go
create table 系别
(
系别代码 char(4) primary key,
系别名称 varchar(50) not null,
系主任姓名 varchar(20),
书记姓名 varchar(100),
)
go
create table 班级
(
班号 char(8) primary key,
班级名称 varchar(50),
年级 char(4) check(年级 like '[0-9][0-9][0-9][0-9]'),
辅导员 char(8),
系别代码 char(4) ,
 foreign key(系别代码) references 系别(系别代码),
)
go

##关于其中的一些设置

- primary key --设置主键
- not null --设置为不空
- foreign key --设置外键
  与 references {table} （{主键}） 连用
  或者 constraint id_fk foreign key (id) references student (id) 设置
  同样可以 constraint id_pk primary key (id) 设置主键

#create 索引

use toyunivers
go
creat [unique] [clustered] [nonclustered] index idx_id
on id（视图名称) ({column} asc/desc)

#insert

use toyunivers
insert into dbo.班级 values('1001','信息安全151','2015')

#update

use toyunivers
update dbo.学生
set 姓名='张小三'
where 学号=2015122001
order by {列} asc

- order by 排序

#select

##条件查询
use toyunivers
select 性别,姓名,出生日期 年龄 from dbo.学生
where {条件}

##人数查询
use toyunivers
select 性别,count(*) 人数 from dbo.学生 
group by 性别

- 调用聚合函数 count(*) group by 

##根据出生日期查询年龄

use toyunivers
select  *,datediff(year,出生日期,getdate()) as 年龄 from dbo.学生  where datediff(year,出生日期,getdate()) >='20'

- datediff( year,出生日期,getdate()) 最后的数据减去中间的数据以前面的数据显示

## 查询姓张的同学

use toyunivers
SELECT * FROM dbo.学生
where 姓名 LIKE '张%'
 
- like '张%'查询姓名以张开头的学生