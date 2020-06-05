### mysql数据库备份  

## [Document](https://www.runoob.com/mysql/mysql-regexp.html)

#### 把旧表插入新表
- select * into newTable from oldTable where name="min"

#### 创建数据库
- create database database_name

#### 创建表
- create table table_name{
	id int,
	name varchar(255),
	keyword char(50)
}

#### 删除表
- drop table table_name

#### 模糊匹配
- select * from table_name where name like "%min_"

#### 正则表达式匹配
- select * from table_name where name regexp "^st$"

#### alter命令使用
- alter table table_name drop id  (移除字段id)
- alter table table_name add id int   (添加字段id)
- alter table table_name add id int first  (指定位置)
- alter table table_name add id int after c   (指定位置在c字段后面)
- alter table table_name modify c char(10)   (修改字段c的类型)
- alter table table_name change i j int (修改字段名i为j，并指定类型)
- alter table table_name modify j int not null default 100;  (修改字段并指定不为空和默认值)
- alter table old_name rename to new_name;  (更改表名)

#### 创建临时表
- create temporary table table_name(
  id int,
  name varchar(255)
)
- drop table table_name    (当然这一步可以省略,断开数据连接时会自动销毁临时表)

#### 复制表
- show create table table_name  (获取创建表时语句)

1. 方法一
- create table new_table like old_table 
- insert into new_table select * from old_table

2. 方法二
- create table new_table select * from old_table

3. 方法三
- create table new_table (id int not null auto_increment primary key) as (select * from old_table);

### 导出数据

#### 普通文本导出
- select * from table_name into outfile "/tmp/runoob.txt"

#### 导出表作为原始数据
- mysqldump -u root -p koa users > dump.txt   (-p 跟数据库及表名)
- mysqldump -u root -p koa > dump.txt (导出整个数据库)
- mysqldump -u root -p --all-databases > database_dump.txt (备份所有数据库)  
- mysqldump -h other-host.com -P port -u root -p database_name > dump.txt

### 导入数据

#### mysql命令 
- mysql -uroot -p123456 < runoob.sql  (将整个数据库runoob.sql导入)

#### source命令 (在某一个数据库下操作)
- source /home/abc/abc.sql 

#### load data命令  (在某一个数据库下操作)
- load data local infile "dump.txt" into table table_name

#### mysqlimport命令
- mysqlimport -u root -p --local mytbl dump.txt