# Promise

==callback hell (回调地狱)==

![image-20210309202444001](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210309202444001.png)

无法保证执行的顺序

```javascript
var fs= require('fs')

fs.readFile('./a.js','utf8',(err,data) => {
  if (err) {
    throw err
  }
  console.log(data);
})

fs.readFile('./b.js','utf8',(err,data) => {
  if (err) {
    throw err
  }
  console.log(data);
})

fs.readFile('./c.js','utf8',(err,data) => {
  if (err) {
    throw err
  }
  console.log(data);
})
```

回调嵌套

```javascript
var fs= require('fs')

fs.readFile('./a.js','utf8',(err,data) => {
  if (err) {
    throw err
  }
  console.log(data);
  fs.readFile('./b.js','utf8',(err,data) => {
    if (err) {
      throw err
    }
    console.log(data);
    fs.readFile('./c.js','utf8',(err,data) => {
      if (err) {
        throw err
      }
      console.log(data);
    })
  })
})


```

链式编程

```javascript
var fs = require('fs')

//对 promise 进行封装
var pfileread = (filepath) => {
  return new Promise((resolve, reject) => {
    fs.readFile(filepath,'utf8',(err,data) => {
      if (err) {
        return reject(err)
      }
      resolve(data)
    })
  })
}

pfileread('./a.js')
  .then((res) => {
  console.log(res);
  return pfileread('./b.js')
}).then((res) => {
  console.log(res);
  return pfileread('./c.js')
}).then((res) => {
  console.log(res);
}).catch((err) => {
  console.log('读取失败');
})

```

mongoose 所有的 API 都支持 Promise

```javascript
Students.find().then((data) => {
    console.log(data);
  })
```

![image-20210313170738303](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210313170738303.png)

```javascript
User.findOne({
  username: 'mazi'
}).then((user) => {
  if (user) {
    console.log('用户已存在');
  } else {
    return new User({
      username: 'mazi',
      passworld: '66666',
      email: '333.com'
    }).save()
  }
}).then((res) => {
  if (res) {
    return console.log('注册成功');
  }
  console.log('注册失败');
})
```

