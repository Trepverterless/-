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
create table ϵ��
(
ϵ����� char(4) primary key,
ϵ������ varchar(50) not null,
ϵ�������� varchar(20),
������� varchar(100),
)
go
create table �༶
(
��� char(8) primary key,
�༶���� varchar(50),
�꼶 char(4) check(�꼶 like '[0-9][0-9][0-9][0-9]'),
����Ա char(8),
ϵ����� char(4) ,
 foreign key(ϵ�����) references ϵ��(ϵ�����),
)
go

##�������е�һЩ����

- primary key --��������
- not null --����Ϊ����
- foreign key --�������
  �� references {table} ��{����}�� ����
  ���� constraint id_fk foreign key (id) references student (id) ����
  ͬ������ constraint id_pk primary key (id) ��������

#create ����

use toyunivers
go
creat [unique] [clustered] [nonclustered] index idx_id
on id����ͼ����) ({column} asc/desc)

#insert

use toyunivers
insert into dbo.�༶ values('1001','��Ϣ��ȫ151','2015')

#update

use toyunivers
update dbo.ѧ��
set ����='��С��'
where ѧ��=2015122001
order by {��} asc

- order by ����

#select

##������ѯ
use toyunivers
select �Ա�,����,�������� ���� from dbo.ѧ��
where {����}

##������ѯ
use toyunivers
select �Ա�,count(*) ���� from dbo.ѧ�� 
group by �Ա�

- ���þۺϺ��� count(*) group by 

##���ݳ������ڲ�ѯ����

use toyunivers
select  *,datediff(year,��������,getdate()) as ���� from dbo.ѧ��  where datediff(year,��������,getdate()) >='20'

- datediff( year,��������,getdate()) �������ݼ�ȥ�м��������ǰ���������ʾ

## ��ѯ���ŵ�ͬѧ

use toyunivers
SELECT * FROM dbo.ѧ��
where ���� LIKE '��%'
 
- like '��%'��ѯ�������ſ�ͷ��ѧ��