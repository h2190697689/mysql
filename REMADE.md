### MySQL 数据库  

## [Document]((https://www.w3school.com.cn/sql/sql_select_into.asp))

#### 创建数据库
- create database dataName
   
#### 删除数据库
- drop database dataName
   
#### 选择数据库
   use dataName
#### 创建数据表
1. create table tableName(id int primary key,name  varchar(10))
2. create table if not exists tableName(id int unsigned auto_increment,title varchar(10) not null,primary 
   key(id))engine=InnoDB default charset=utf8   //默认字符集为utf8 
   auto_increment=10;

#### 删除数据表
- drop table tableName
   
#### 增加、减少列
-  alter table tableName add columnName dataType  --添加列
-  alter table tableName drop columnName  --删除列
-  alter table tableName modify columnName dataType   --改变某列数据类型
   （ sql server 中 为alter table tableName alter columnName dataType ）
#### 插入数据表
- insert into tableName values(value1,value2,value3)
- insert into tableName(field1,field2,field3) values(value1,value2,value3)

#### 查询数据表
- select * from tableName
- select * from tableName limit 3 offset 2   //offset为下偏移量，配合limit一起使用
  select name from tableName where id=2

#### 更新数据表
- update tableName set name=3 where id=2;

#### 删除数据表
- delete from tableName where id=2




### 字段


#### like  --not like  
1. select * from tableName where name like '%化_'  
   (% 代表1个或多个字符          _ 代表一个字符) 
   
2. not like 
- select * from tableName where name not like '%化%'

3. [ABC] 字符列中的任何单一字符    
- [^ABC]或[!ABC] 不在字符列中的任何单一字符

#### select * from tableName where city like '[!ABC]%'
- 选择居住城市不以A、B、C开头的人
  
#### distinct
- select distinct name from tableName
   
#### where 
- select * from tableName where id>10
   
#### AND & OR 
1. select * from tableName where id<6 and name="马云"
2. select * from tableName where id=6 or name="马云"
#### 排序 order by
- desc(降序)  asc(升序,默认值)
- select company,orderNumber from tableName order by company desc, orderNumber asc\

#### limit
1. select name from tableName limit 3
- (sql server 中的为 top, select top 3 name from tableName)
     
### in  --not in
- select name from tableName where age in (56,23,36)
    
### between(两数之间)   --not between
- select name from tableName where id between 3 and 6
    
### as (别名使用)
1. select name as goodName from tableName   --应用列
2. SELECT po.OrderID, p.LastName, p.FirstName
   FROM Persons AS p, Product_Orders AS po
   WHERE p.LastName='Adams' AND p.FirstName='John'  --应用表
       
### group by （合计函数）
- select role,sum(age) from staff group by role
    
### having (与group by 配合使用，用于判定)
- SELECT role,SUM(age) FROM staff WHERE role IN ('aus','bus') GROUP BY role HAVING SUM(age)>100

#### isnull 函数(便于计算)
1. sql server:  isnull(num, 0) 函数
2. oracle:  nvl(num, 0)函数
3. mysql: ifnull(num, 0)、 coalesce(num, 0)函数
     
#### null 的判断(使用is 而不是使用等于号)   --is not null
- select * from tableName where age is null
     
#### 自增（auto_increment）
 1. create table Persons(id int not null auto_increment,name varchar(255) not null,primary key(id))
 2. alter table persons auto_increment=100



### 连接join


#### inner join(内连接，等同于join)
1. 不使用join
- select staff.name,staff.age,staff.role,product.name from staff,product where staff.id=product.other_id
2. 等同使用join
- select staff.name,staff.age,staff.role,product.name from staff inner join product on 
staff.id=product.other_id

#### left join(左连接，侧重左边必须全部列出，即使右表没有匹配行)
1. SELECT staff.NAME,staff.age,staff.role,produce.NAME FROM staff LEFT JOIN produce ON staff.id=produce.other_id 

    name   age  role name
    马云    56   aus  淘宝
    张一鸣  23   bus  字节跳动
    马化腾  36   cus  null

#### right join(右连接，侧重右边必须全部列出，即使左表没有匹配行)
1. SELECT staff.NAME,staff.age,staff.role,produce.NAME FROM staff RIGHT JOIN produce ON staff.id=produce.other_id  
    name   age  role name
    马云    56   aus  淘宝
    张一鸣  23   bus  字节跳动
    null  null  null  百度

#### full join(全连接，只要存在属性就全部展示，mysql不支持)
    name   age  role name
    马云    56   aus  淘宝
    张一鸣  23   bus  字节跳动
    马化腾  36   cus  null
    null  null  null  百度



### 连接多表和字段约束 

#### union  （union all 不去除重复项）
- select * from emp union select * from staff  //列出两表总数据，去除重复项

#### select into(表的拷贝)
- select * into newTableName in dataName from oldTableName
    
#### constraints(sql约束):
1. not null

2. unique
- create table tableName(id int,unique(id))   //或者 id int unique 也可以定义
- alter table tableName add unique(id)   //drop

3. primary key
- create table tableName(id int,primary key(id))   // 或者 id int primary key 也可以定义
- alter table tableName add primary key(id)  // drop

4. foreign key
- create table tableName(id int,other_id int,foreign key(other_id) references OtherTabelName(id)
)
- alter table tableName add foreign key(other_id) references OtherTabelName(id)
- alter table tableName drop foreign key (TODO???)
5. check
- 同上 alter table tableName add check(id>5)

6. default
- alter table tableName alter city set default 'hangzhou'

7. Index (创建索引)
- create INDEX indexName on tableName(columnName)

