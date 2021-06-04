# Node 操作 MySQL

安装

```sh
npm install mysql
```

```javascript
//导包
var mysql      = require('mysql');

//1.创建连接
var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'root',
  password : 'wlglb0065',
  database : 'users'
});

//2.连接数据库
connection.connect();

//3.执行数据操作
//查询数据
connection.query('SELECT * FROM `users`', function (error, results, fields) {
  if (error) throw error;
  console.log('The solution is: ', results);
});

//插入数据
// connection.query('INSERT INTO users VALUES (1,"admain","123456")', function (error, results, fields) {
//   if (error) throw error;
//   console.log('The solution is: ', results);
// });

//4.关闭连接
connection.end();
```

