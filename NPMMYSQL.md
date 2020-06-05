### mysql (npm)


#### connection 
- var connection=mysql.createConnection({})
- connection.connect(function(error){})
- connection.query("sql",function(error,results,fields){})
- connection.end(function(error){})
- connection.destroy()  (没有回调函数)

#### pool 
- var pool = mysql.createPool({})
- pool.getConnection(function(err,connection){})
- connection.query("sql",function(error,results,fields){})
- connection.release()

- pool.query("sql",function(error,results,fields){})   (这是一种快捷形式)

- pool.on("acquire",function(connection))
- pool.on("connection",function(connection){})
- pool.on('enqueue', function () {});
- pool.on("release", function(connection) {})

#### crud
- query("select * from table_name where name=?",["min"],function(error,results,fields){})   // 中间只有一个参数时，可以为字符串，不必为数组
- query("delete from table_name where name=?","min",function(error,results,fields){})
- query("update table_nam e set name=3 where id=1")
- query("insert into table_name values(?,?,?)",["1","men","min"])
- query("insert into table_name set ?",{title:"test"},function(error,results,fields){})

 
#### 执行多条sql语句  (为防止sql注入,尽量不开启)
- mysql.createConnection({multipleStatements: true});
- mysql.createPool({multipleStatements: true});