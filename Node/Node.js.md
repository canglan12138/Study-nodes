# 第一章

#### 1.1.Node.js

- Node.js不是一门语言
- Node.js不是库，不是框架
- Node.js是一个JavaScript运行时环境
- Node.js可以解析和执行JavaScript代码
- 以前只有浏览器可以解析JavaScript代码
- 现在JavaScript可以完全脱离浏览器来运行，一切都归功于Node.js

#### 1.2.浏览器中的JavaScript

- EcmaScript
  - 基本语法
  - if
  - var
  - function
  - Object
  - Array
- Bom
- Dom

#### 1.3.Node.js中的JavaScript

- **没有Bom、Dom**
- EcmaScript
- Node.js这个JavaScript执行环境中为JavaScript提供了一些服务器级别的操作API
  - 例如文件读写
  - 网络服务的构建
  - 网络通信
  - http服务器
  - 等处理

#### 1.4.Node.js的特性

- event-driven 事件驱动
- non-blocking I/O model 非阻塞IO模型（异步）
- lightweight and efficient 轻量和高效 

#### 1.5.npm

- npm 是基于Node.js环境的包管理工具

- npm 是世界上最大的开源库生态系统

- 绝大多数 JavaScript 相关的包都存放在 npm 上，目的是为了让开发人员更方便地下载使用

- ```
  npm install xxxx
  ```

####  1.6.Node.js能做什么

- Web 服务器后台

- 命令行工具
  - npm
  - git(C语言)
  - hexo(node)
  - ....

- 对于前端，接触最多的是命令行工具

#### 1.7.学习Node.js可以

- B/S编程模型

  - Browser - Server
  - back-end
  - 任何服务端技术B/S模型一样，和语言无关
  - Node只是作为学习 BS 编程模型的工具
- 模块化编程

  - 在Node.js中可以像 `@import()`一样来引用加载JavaScript脚本文件
- Node 常用API
- 异步编程
  - 回调函数
  - Promise
  - async
  - generator
- Express Web 开发框架
- Ecmascript 6 

# 第二章

#### 2.1 Hello world

1. 创建编写 JavaScript 脚本文件
2. 打开终端，定位到脚本文件所属目录
3. 输入 `node 文件名` 执行对应的文件

**注意: 文件名不要使用 `node.js`** 

#### 2.2 文件操作模块

- 导入 fs (**filesystem**)
- 读文件 **readFile**

```javascript
//1.使用 require 方法加载 fs 文件模块
var fs = require('fs')
//2.读取文件
// 第一个参数 路径
// 第二个参数 回调函数
/*
*    成功
*       data 数据
*       error null
*    失败
*       data undefined
*       error 错误对象
* */

//data 是16进制数据
//通过 toString 方法转化成字符串
fs.readFile('./text.txt',(error,data) => {
  if (error) {
    console.log('读取文件失败');
    console.log(error);
  }else {
    console.log('读取文件成功');
    console.log(data.toString());
  }
})
```

- 写文件 **writeFile**

```javascript
var fs = require('fs')

/*
* 第一个参数 文件路径
* 第二个参数 文件内容
* 第三个参数 回调函数
* */

/*
*  成功
*     文件写入成功
*     error null
*  失败
*     文件写入失败
*     error 错误对象
* */
fs.writeFile('./你好.txt','666',(error) => {
  if (error) {
    console.log('文件写入失败');
    console.log(error);
  }else {
    console.log('文件写入成功');
  }
})
```

- 读目录

  ```javascript
  var fs = require('fs')
  fs.readdir('F:/www',(err,files) => {
    if (err) {
      return console.log('目录读取失败');
    }
    console.log(files); //目录存在数组里
  })
  ```

  ![image-20210224122845066](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210224122845066.png)

#### 2.3 http

- 收到请求==无响应==

```javascript
/*
* Node 提供了一个核心模块：http
* http这个模块就是帮助创建服务器
* */

//1.加载 http 模块
var http = require('http')

//2.使用 http.createServer() 方法创建一个 Web 服务器
//  返回一个 Server 实例
var Server = http.createServer()

/*
* 3.服务器
* 接收请求
* 处理请求
* 响应
* */
/*
* 监听 request 请求事件
* 触发事件后，执行回调函数
* */
Server.on('request',() => {
  console.log('收到请求了');
})

/*
* 4.启动服务器
* 绑定端口号
* */
Server.listen(3000,() => {
  console.log('服务器启动成功了');
})

```

![image-20210222194239953](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210222194239953.png)

- 收到请求==有响应==

```javascript
var http = require('http')
var Server = http.createServer()

/*
* 回调函数有两个参数
*   Request 请求对象
*     获取客户端的请求信息，例如请求路径
*   Response 响应对象
*     给客户端发送响应信息
* */
Server.on('request',(request,response) => {
  console.log('收到请求了，请求路径是：' + request.url);
  //response 对象有一个方法：write 给客户端发送响应数据
  //write 可以使用多次，但最后一定要用 end 来结束响应，否则客户端会一直等待
  switch (request.url) {
    case '/':
      response.end('index');
      break;
    case '/login':
      response.end('login');
      break;
  }
  // if (request.url == '/') {
  //   response.write('index');
  //   response.end()
  // }else if (request.url == '/login'){
  //   response.write('666');
  //   response.end()
  // }
})
Server.listen(3000,() => {
  console.log('服务器启动成功了');
})
```

![image-20210222202643992](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210222202643992.png)

- 响应数组对象

```javascript
var http = require('http')
var Server = http.createServer()
Server.on('request',(request,response) => {
  console.log('收到请求了，请求路径是：' + request.url);
  switch (request.url) {
    case '/':
      response.end('index');
      break;
    case '/login':
      response.end('login');
      break;
    case '/apple':
      var products = [
        {
          name: 'apple',
          price: 888
        },
        {
          name: 'apple',
          price: 888
        },
        {
          name: 'apple',
          price: 888
        },
      ]
        /*
        *响应内容只能是二进制数据或者字符串
        * 数字
        * 对象
        * 数组
        * 布尔值
        * 都不行
        * */
      response.end(JSON.stringify(products));//JSON.stringify() 方法用于将 JavaScript 值转换为 JSON 字符串。
      break;
    default:
      response.end('404');
  }

  // if (request.url == '/') {
  //   response.end('index');
  // }else if (request.url == '/login'){
  //   response.end('666');
  // }else if (request.url === '/apple') {
  //   var products = [
  //     {
  //       name: 'apple',
  //       price: 8888
  //     },
  //     {
  //       name: 'apple',
  //       price: 8888
  //     },
  //     {
  //       name: 'apple',
  //       price: 8888
  //     }
  //   ]
  //   response.end(JSON.stringify(products));
  // }else {
  //   response.end('404');
  // }
})
Server.listen(3000,() => {
  console.log('服务器启动成功了');
})
```

![image-20210223113451792](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210223113451792.png)

#### 2.4 path 路径操作模块

- path.basename
  - 获取一个路径的文件名（默认包含扩展名）
- path.dirname
  - 获取一个路径中的目录部分
- path.extname
  - 获取一个路径中的扩展名部分
- path.parse
  - 把一个路径转为对象
    - root 根路径
    - dir 目录
    - base 包含后缀名的文件名
    - ext 后缀名
    - name 不包含后缀名的文件名
- path.join
  - 对路径进行拼接
- path.isAbsolute
  - 判断一个路径是否是绝对路径

#### 2.5 Node中的JavaScript

- EcamScript

  - ==没有 DOM、BOM==

- 核心模块

  - Node 为 JavaScript 提供了很多服务器级别的 API ,这些 API 绝大多数被包装到了一个具名的核心模块中。

    例如

    - 文件操作的 fs
    - http 服务的 http 模块
    - path 路径操作模块
    - os 操作系统信息模块

    加载模块

  - ```javascript
    var fs = require('fs')
    ```

    

- 第三方模块

  - art-template
  - 通过 npm 下载使用

- 用户自定义模块

  - 自己创建的文件
  
  - ```javascript
  require('./')
    ```

  - ==相对路径（./ 或 ../）不能省略==

  - 只有模块作用域，没有全局作用域

  - 可以省略后缀名

  - require

    1. 加载文件模块并执行里面的代码

    2. 拿到被加载文件模块导出的接口对象
  
       - 每个文件模块都提供了一个对象：==exports==
     - 默认是一个空对象
       - 把需要被外部访问的成员挂载到 ==exports== 对象中
  
       ![image-20210223135535399](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210223135535399.png)

#### 2.6 Web服务器开发

IP 地址和端口号

- ==ip 地址用来定位计算机(服务器)==
- ==端口号用来定位具体的应用程序==
- ==一切需要联网通信的软件都会占用一个端口号==
- ==端口号的范围从 0 - 65535 之间==
- ==在计算机中有一些默认的端口号，最好不要去使用==
  - ==例如 http 服务的 80==
- ==开发过程中使用简单的端口号即可==
  - ==例如 3000，5000 等没什么具体含义的端口号==

#### 2.7 解决中文乱码

```javascript
var http = require('http')
var server = http.createServer()
server.on('request',(req,res) => {
  /*
  * 服务器默认发送的数据是 utf8 编码的内容
  * 但是浏览器会按照当前操作系统的默认编码去解析
  * 中文操作系统默认 gbk
  * 解决方法：
  * 服务器要正确地告诉浏览器响应的内容是使用什么编码的
  * http 协议中，Content - type 是用来告诉对方我给你发送的数据内容是什么类型
  * */
  // res.setHeader('Content-Type','text/plain;charset=utf-8')
  // res.end('hello world 世界');
  var url = req.url
  if(url === '/plain') {
    //text/plain 普通文本
    res.setHeader('Content-Type','text/plain;charset=utf-8')
    res.end('hello world 世界');
  }else if(url === '/html') {
    //text/html html文本
    res.setHeader('Content-Type','text/html;charset=utf-8')
    res.end('<p>hello world<a href="">点我</a></p>')
  }
})
server.listen(5000,() => {
  console.log('Server is running...');
})
```

![image-20210223162400016](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210223162400016.png)

#### 2.8 Content - Type

```javascript
var http = require('http')
var fs = require('fs')

var server = http.createServer()
server.on('request',(req,res) => {
  var url = req.url

  if(url === '/') {
    fs.readFile('./resource/index.html',(err,data) => {
      if (err) {
        res.setHeader('Content-type','text/plain;charset=utf-8')
        res.end('文件读取失败')
      }else {
        res.setHeader('Content-type','text/html;charset=utf-8')
        res.end(data)
      }
    })
  }else if(url === '/picture') {
    //url:统一资源定位符
    fs.readFile('./resource/10周年.png',(err,data) => {
      if (err) {
        res.setHeader('Content-type','text/plain;charset=utf-8')
        res.end('图片读取失败')
      }else {
        //图片不需要指定编码，编码一般指字符编码
        res.setHeader('Content-type','image/png')
        res.end(data)
      }
    })
  }else if (url === '/txt') {
    fs.readFile('./resource/hello.txt',(err,data) => {
      if (err) {
        res.setHeader('Content','text/plain;charset=utf-8')
        res.end('txt文件读取失败')
      }else {
        res.setHeader('Content-type','text/plain;charset=utf-8')
        res.end(data)
      }
    })
  }
})

server.listen(5000,() => {
  console.log('Server is running...');
})

```

# 第三章

#### 3.1 无分号代码风格

==需注意以下情况==

当一行代码是以

- (
- [
- `（反引号）

开头的时候，则在前面补上一个 ; 避免语法解析错误		

```javascript
var foo = 'hello,world'
console.log(foo)
;(() => {
  console.log('666');
})()
```

![image-20210223201815433](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210223201815433.png)

#### 3.2 Apache

```javascript
var http = require('http')
var fs = require('fs')

var server = http.createServer()

server.on('request',(req,res) => {
  var url = req.url
  var wwwDir = 'F:/www'
  var filePath = '/index.html'
  if (url !== '/') {
    filePath = url
  }
  fs.readFile(wwwDir + filePath,(err,data) => {
    if (err) {
      return res.end('404 not found')
    }
    res.end(data)
  })
})

server.listen(3000,() => {
  console.log('server is running');
})
```

- 动态更改目录列表

  ```javascript
  var http = require('http')
  var fs = require('fs')
  
  var server = http.createServer()
  
  server.on('request',(req,res) => {
    var url = req.url
    var wwwDir = 'F:/www'
    //读取目录
    fs.readdir(wwwDir,(err,files) => {
      var content = ''
      if (err) {
        return res.end("Can Not Found Dir")
      }
      //在 ES6 反引号字符串中，可以使用 ${} 来引用变量
      //遍历目录名
      files.forEach((item) => {
        content += `
          <tr>
            <td data-value=".idea/">
              <a class="icon dir" href="/F:/www/.idea/">${item}</a>
            </td>
            <td class="detailsColumn" data-value="0"></td>
            <td class="detailsColumn" data-value="1614135189">2021/2/24 上午10:53:09</td>
          </tr>
        `
      })
      fs.readFile('./template.html',(err,data) => {
        if (err) {
          return res.end('404 not found')
        }
        //转成字符串
        data = data.toString()
        //替换内容
        data = data.replace('@@',content)
        //响应数据
        res.end(data)
      })
    })
  })
  
  server.listen(3000,() => {
    console.log('server is running');
  })
  ```

  ![image-20210224154803908](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210224154803908.png)

#### 3.3 模板引擎

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
//导入模板引擎
<script src="node_modules/art-template/lib/template-web.js"></script>
//定义模板内容
<script type="text/template" id="tpl">
		我是{{ name }}
		我喜欢{{ each hobbies }} {{ $value }} {{ /each }}
</script>

<script>
      //将替换的对象挂载到模板上
	var ret = template('tpl',{
	  name: 'lg',
		hobbies: [
		    '打游戏',
		    '看电影',
		    '吃美食'
		]
	})
  console.log(ret);
</script>
</body>
</html>
```

![image-20210224155020790](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210224155020790.png)

- 通过模板引擎动态改变目录列表

  ```javascript
  var http = require('http')
  var fs = require('fs')
  var template = require('art-template')
  
  var server = http.createServer()
  server.on('request',(req,res) => {
    var wwwDir = 'F:/www'
    //读取模板文件
    fs.readFile('./template.html',(err,data) => {
      if (err) {
        return res.end('404 not found')
      }
      //读取目录
      fs.readdir(wwwDir,(err,files) => {
        if (err) {
          return res.end("Can Not Found Dir")
        }
        //模板文件转换成字符串
        data = data.toString()
        //将目录替换到模板文件中（用render函数）
        //参数1 模板字符串
        //参数2 解析替换对象
        var htmlStr = template.render(data,{
          files: files
        })
        //响应模板文件
        res.end(htmlStr)
      })
    })
  })
  
  server.listen(3000,() => {
    console.log('server is running');
  })
  ```

  ![image-20210224154803908](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210224154803908.png)

#### 3.4 案例：留言本

![image-20210226233944135](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210226233944135.png)

```javascript
var http = require('http')
var fs = require('fs')
var url = require('url')
var template = require('art-template')


var comments = [
  {
    name: '张三',
    message: '你好',
    date: '2020.02.02'
  },
  {
    name: '张三2',
    message: '你好',
    date: '2020.02.02'
  },
  {
    name: '张三3',
    message: '你好',
    date: '2020.02.02'
  },
  {
    name: '张三4',
    message: '你好',
    date: '2020.02.02'
  },
  {
    name: '张三5',
    message: '你好',
    date: '2020.02.02'
  }
]
/*
* HTML 文件放到 views中
* 静态资源存放在 public 中
* */

http.createServer((req,res) => {
  //true： query （查询字符串）转为对象，方便操作
  var parseObj = url.parse(req.url,true)
  var pathname = parseObj.pathname
  if (pathname === '/') {
    fs.readFile('./views/index.html',(err,data) => {
      if (err) {
        return res.end('404 Not Found.');
      }
      var htmlStr = template.render(data.toString(),{
        comments: comments
      })
      res.end(htmlStr)
    })
  }else if (pathname === '/post') {
    fs.readFile('./views/post.html',(err,data) => {
      if (err) {
        return res.end('404 Not Found.');
      }
      res.end(data)
    })
  }else if (pathname === '/pinglun') {
    //获取 query 对象，添加时间属性，插入到 comments 数组中
    var comment = parseObj.query
    comment.date = '2020.08.08'
    comments.unshift(comment)
    //服务端重定向
  /*
    * 状态码设置为 302 临时重定向
    *  statusCode
    * 在响应头中通过 Location 告诉客户端往哪重定向
    *   SetHeader
    * 最后需要结束响应
    * */
    res.statusCode = 302
    res.setHeader('Location','/')
    res.end()
  }else if (pathname.indexOf('/public/') !== -1) {
    fs.readFile('.' + pathname,(err,data) => {
      if (err) {
        return res.end('404 Not Found.');
      }
      res.end(data)
    })
  }else {
    fs.readFile('./views/404.html',(err,data) => {
      if (err) {
        return res.end('404 Not Found.');
      }
      res.end(data)
    })
  }

}).listen(3000,() => {
  console.log('running...');
})
```

# 第四章

#### 4.1 什么是模块化

- 文件作用域
- 通信规则
  - 加载 require
  - 导出 

#### 4.2 CommonJS 模块规范

在 Node 中的 JavaScript 还有一个重要概念，模块系统

- 模块作用域
- 使用 require 方法来加载模块
- 使用 exports 接口对象导出模块中的成员

#### 4.3 加载 `require `

语法：

```javascript
 var 自定义变量名称 = require('模块')
```

两个作用

- 执行被加载模块中的代码
- 得到被加载模块中的 `exports` 导出的接口对象

#### 4.4 导出 `exports`

- Node 中是模块作用域，默认文件中所有的成员只在当前文件模块有效

- 对于希望可以被其他模块访问的成员，需要把这些公开的成员都挂载到 `exports` 接口对象中

  ```javascript
  exports.a = 123
  exports.b = 'hello'
  exports.c = function () {
  	console.log('ccc')
  }
  exports.d = {
  	foo: 'bar'
  }
  ```

  

- 导出单个成员，拿到的就是函数，字符串

  ```javascript
  moudle.exports = 'hello'
  ```

  以下情况会覆盖

  ```javascript
  moudle.exports = 'hello'
  //后者会覆盖前者
  moudle.exports = function (x,y) {
  	return x + y
  }
  ```

  也可以这样导出多个成员

  ```javascript
  moudle.exports = {
  	add: function (x,y) {
  		return x + y
  	},
  	str: 'hello'
  }
  ```

- exports 和 module.exports 的区别
  + 每个模块中都有一个 module 对象
  + module 对象中有一个 exports 对象
  + 我们可以把需要导出的成员都挂载到 module.exports 接口对象中
  + 也就是：`moudle.exports.xxx = xxx` 的方式
  + 但是每次都 `moudle.exports.xxx = xxx` 很麻烦，点儿的太多了
  + 所以 Node 为了你方便，同时在每一个模块中都提供了一个成员叫：`exports`
  + `exports === module.exports` 结果为  `true`s
  + 所以对于：`moudle.exports.xxx = xxx` 的方式 完全可以：`expots.xxx = xxx`
  + 当一个模块需要导出单个成员的时候，这个时候必须使用：`module.exports = xxx` 的方式
  + 不要使用 `exports = xxx` 不管用
  + 因为每个模块最终向外 `return` 的是 `module.exports`
  + 而 `exports` 只是 `module.exports` 的一个引用
  + 所以即便你为 `exports = xx` 重新赋值，也不会影响 `module.exports`
  + 但是有一种赋值方式比较特殊：`exports = module.exports` 这个用来重新建立引用关系的
  + 之所以让大家明白这个道理，是希望可以更灵活的去用它

#### 4.5 require 方法加载规则

- 优先从缓存加载

- 判断模块标识

  - 核心模块

    - 本质上是文件，已被编译到二进制文件中了

  - 第三方模块

    - ==以 art-template 为例==

    - 第三方模块通过 npm 下载使用

    - 通过 require('包名')加载使用

    - 不可能有任何一个第三方包与核心模块的名字是一样的

    - 既不是核心模块，也不是路径形式的模块

      - 路径形式的模块
        - ./ 当前目录，不可省略
        - ../ 上一级目录，不可省略
        - .js 后缀名可以省略
        - 例如：require('./foo.js')

    - 查找规则

      1. 先找到当前文件所处目录中的 node_modules 目录

      2. node_modules/art-template

      3. node_modules/art-template/package.json 文件

      4. node_modules/art-template/package.json 文件中的 main 属性

      5. main 属性中就记录了 art-template 的入口模块

      6. 然后加载使用第三方包，实际上加载的还是文件

      7. 如果 package.json 文件不存在，或者 main 指定的入口模块也没有

         则会自动找该目录下的 index.js

         如果以上任何一个条件都不成立，则会进入上一级目录的 node_modules 目录查找，如果还没有，继续向上查找。如果直到当前磁盘根目录还找不到，最后报错：

         can not find module xxx

         ==注意==：一个项目有且只有一个 node_module 而且是存放到项目的根目录

  - 自定义模块


#### 4.6 npm

全称 node package manage

- npm 网站

  www.npmjs.com

- npm 命令行工具

  npm 有版本概念

  在命令行输入

  ```bash
  npm --version
  ```

  升级 npm(自己升级自己)

  ```bash
  npm install --global npm
  ```

- npm 常用命令

  - npm init

    npm init -y 可以跳过向导，快速生成

  - npm install

    npm i

    一次性把 dependencies 选项中的依赖项全部安装

  - npm install 包名 

    npm i 包名

    只下载

  - npm install --save 包名 

    npm i 包名 ==-S==

    下载并保存依赖项（package.json文件中的 dependencies 选项）

  - npm uninstall 包名

    npm un 包名

    只删除，依赖项依然会保存

  - npm uninstall 包名 --save

    npm un 包名 ==-S==

    删除的同时也会把依赖信息去除

  - npm help

    查看使用帮助

  - npm 命令 --help

    查看指定命令的使用帮助

    如命令的简写忘记，可通过此进行查看

- 解决 npm 被墙问题

  淘宝的开发团队把 npm 在国内做了一个备份

  http://npm.taobao.org/

  安装淘宝的 npm

  ```shell
  #任意目录都可以执行
  npm install --global cnpm
  ```

  把 `npm ` 替换成 `cnpm`

  ```sh
  #官方 npm 下载
  npm install jquery
  
  #淘宝服务器下载
  cnpm install jquery
  ```
  不安装 `cnpm` 使用淘宝服务器来下载

  ```sh
  #把这个选项加入配置文件中
  npm config set registry https://registry.npm.taobao.org
  #查看 npm 配置信息
  npm config list
  ```

  

#### 4.7 package.json

每个项目都有 package.json 文件（包描述文件）

通过 `npm init` 的方式来自动初始化出来

```javascript
E:\NodeJs>npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defau
lts.

See `npm help init` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (nodejs)
version: (1.0.0)
description: 这是一个测试文件
entry point: (index.js)
test command:
git repository:
keywords:
author: lg
license: (ISC)
About to write to E:\NodeJs\package.json:

{
  "name": "nodejs",
  "version": "1.0.0",
  "description": "这是一个测试文件",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "lg",
  "license": "ISC"
}
Is this OK? (yes) yes
```

```javascript
{
  "name": "nodejs",
  "version": "1.0.0",
  "description": "这是一个测试文件",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "lg",
  "license": "ISC",
  "dependencies": {
    "jquery": "^3.5.1",
    "save": "^2.4.0"
  }
}

```

`dependencies` 选项，用来保存第三方包的依赖信息

如果 `node_modules` 删除了，只需要 `npm install` 就会自动把 `package.json` 中的 `dependencies` 所有的依赖项都下载下来

# 第五章

#### 5.1 Express

安装

```sh
npm install express --save
```

```javascript
//加载 express 第三方模块
var express = require('express')
//相当于创建服务器
var app = express()

//公开目录
app.use('/public',express.static('./public'))

//相当于监听请求事件
app.get('/',(req,res) => {
  res.send('hello')
})
app.get('/about',(req,res) => {
  res.send('hello,你好')
})
//设置端口号，启动服务器
app.listen(3000,() => {
  console.log('app is running');
})
```

#### 5.2 修改完代码自动重启

第三方命令行工具 `nodemon`

```sh
npm install --global nodemon
```

安装完毕后使用

```sh
nodemon app.js
```

`nodemon` 会监视文件变化，文件发生变化，会自动重启服务器

#### 5.3 在 Express 中配置使用 art-template 模板引擎

安装

```sh
npm install art-template --save
npm install express-art-template --save
```

配置

```sh
app.engine('html',require('express-art-template'))
```

使用

```sh
app.get('/',(req,res) => {
	//默认会去项目中的 views 目录找 index.html
  res.render('index.html',{
  	title: 'hello world'
  })
})
```

如果希望修改默认的 `views` 视图渲染存储目录

```sh
//第一个参数就是 views
app.set('views','目录路径')
```

#### 5.4重改留言本

```javascript
var express = require('express')

var comments = [
  {
    name: '张三',
    message: '你好',
    date: '2020.02.02'
  },
  {
    name: '张三2',
    message: '你好',
    date: '2020.02.02'
  },
  {
    name: '张三3',
    message: '你好',
    date: '2020.02.02'
  },
  {
    name: '张三4',
    message: '你好',
    date: '2020.02.02'
  },
  {
    name: '张三5',
    message: '你好',
    date: '2020.02.02'
  }
]

var app = express()
//配置使用 art-template 模板引擎
/*
* 第一个参数 当渲染以 .html 结尾的文件时，使用 art-template 模板引擎
* express-art-template 是专门用来在 Express 中把 art-template 整合到 Express中
* 虽然不用，但是必须安装，因为依赖了 art-template
* */
app.engine('html',require('express-art-template'))

app.use('/public',express.static('./public'))

/*
* res.render('html模板名',{模板数据})
* 第一个参数不能写路径，默认会去项目中的 views 目录找该模板文件
* */
app.get('/',(req,res) => {
  res.render('index.html',{
    comments:comments
  })
})
app.get('/post',(req,res) => {
  res.render('post.html')
})
app.get('/pinglun',(req,res) => {
  //获取 query 对象，添加时间属性，插入到 comments 数组中
  var comment = req.query
  comment.date = '2020.08.08'
  comments.unshift(comment)
  //服务端重定向
  res.redirect('/')
})
app.listen(3000,() => {
  console.log('app is running');
})

```

#### 5.5 在 Express 中获取表单 POST 请求体数据

在 Express 中没有内置获取表单 POST 请求体的 API，需要使用第三方包 `body-parser` 

安装

```sh
npm install --save body-parser
```

配置

```javascript
//引包
var bodyParser = require('body-parser')
//配置 body-parser 中间件，用来解析 POST 请求体
/*
* 加入这个配置，req 请求对象会多出来一个属性：body
* 可以直接通过 req.body 来获取表单 POST 请求体数据
* */
app.use(bodyParser.urlencoded({extended: false}))
app.use(bodyParser.json())
```

使用

```javascript
app.post('/post',(req,res) => {
  var comment = req.body
  comment.date = '2020.08.08'
  comments.unshift(comment)
  res.redirect('/')
})
```

```javascript
var express = require('express')
var bodyParser = require('body-parser')

var comments = [
  {
    name: '张三',
    message: '你好',
    date: '2020.02.02'
  },
  {
    name: '张三2',
    message: '你好',
    date: '2020.02.02'
  },
  {
    name: '张三3',
    message: '你好',
    date: '2020.02.02'
  },
  {
    name: '张三4',
    message: '你好',
    date: '2020.02.02'
  },
  {
    name: '张三5',
    message: '你好',
    date: '2020.02.02'
  }
]

var app = express()

//配置使用 art-template 模板引擎
/*
* 第一个参数 当渲染以 .html 结尾的文件时，使用 art-template 模板引擎
* express-art-template 是专门用来在 Express 中把 art-template 整合到 Express中
* 虽然不用，但是必须安装，因为依赖了 art-template
* */
app.engine('html',require('express-art-template'))

//配置 body-parser 中间件，用来解析 POST 请求体
/*
* 加入这个配置，req 请求对象会多出来一个属性：body
* 可以直接通过 req.body 来获取表单 POST 请求体数据
* */
app.use(bodyParser.urlencoded({extended: false}))
app.use(bodyParser.json())

app.use('/public',express.static('./public'))

/*
* res.render('html模板名',{模板数据})
* 第一个参数不能写路径，默认会去项目中的 views 目录找该模板文件
* */
app.get('/',(req,res) => {
  res.render('index.html',{
    comments:comments
  })
})
app.get('/post',(req,res) => {
  res.render('post.html')
})

app.post('/post',(req,res) => {
  var comment = req.body
  comment.date = '2020.08.08'
  comments.unshift(comment)
  res.redirect('/')
})
app.listen(3000,() => {
  console.log('app is running');
})

```



#### 5.6 在 Express 中获取表单 GET 请求体数据

Express 内置了一个 API，可以直接通过 `req.query` 来获取

```javascript
req.query
```

# 第六章

#### 6.1 回调函数

```javascript
var add = (x,y,callback) => {
  console.log('等待1s');
  setTimeout(() => {
    var res = x + y
    callback(res)
  },1000)
}

add(10,20,(ret) => {
  console.log(ret);
})
```

# 第七章

#### 7.1 Node 中的其他成员

在每个模块中，除了 `require` 、`exports` 等模块相关的 API 之外，还有两个特殊的成员：

- `__dirname`  **动态获取** 可以用来获取当前文件模块==所属目录==的绝对路径
- `__fielname` **动态获取** 可以用来获取==当前文件==的绝对路径
- `__dirname` 和 `__fielname` 是不受执行 node 命令所属路径影响的

在文件操作中，使用相对路径是不可靠的，因为在 Node 中文件操纵的路径被设计为相对于执行 node 命令所处的路径。

所以为了解决这个问题，只需要把相对路径变为绝对路径。

可以使用 `__dirname` 或者 `__fullname` 来解决这个问题

建议文件操作统一转换为 **动态的绝对路径**

==补充==：模块中的路径标识不受影响（相对于文件模块）

# 第八章

#### Express中间件

![image-20210324220805347](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210324220805347.png)

```javascript
var express = require('express')

var app = express()

/*
* 当请求进来，会从第一个中间件开始进行匹配
*     如果匹配，则进来
*         如果请求在进入中间件之后，没有调用 next()，则请求会停在当前中间件中，不会进入下一个中间件
*         如果调用了 next()，则会向后继续找第一个匹配的中间件
*     如果不匹配，则继续去匹配判断下一个中间件
* */

//不关心请求路径和请求方法的中间件
/*
* 中间件本身是一个方法，该方法接收 3 个参数
* Request 请求对象
* Response 响应对象
* next 下一个中间件
* */

// app.use((req,res,next) => {
//   console.log('1');
//   next()
// })
//
// app.use((req,res,next) => {
//   console.log('2');
//   next()
// })
//
// app.use((req,res,next) => {
//   console.log('3');
//   res.send('666')
//   next()
// })

//-------------------------------------------------

// app.use((req,res,next) => {
//   console.log('1');
//   next()
// })
//
// //以 /XXX 开头的中间件
// app.use('/a',(req,res,next) => {
//   console.log(req.url);
// })
//
// app.use('/b',(req,res,next) => {
//   console.log(req.url);
// })

//-----------------------------------------------------

/*
* 严格匹配请求方法和请求路径的中间件
* app.get
* app.post
* */

app.get('/',(req,res,next) => {
  console.log('/');
})

app.get('/a',(req,res,next) => {
  console.log('/a');
})


app.listen(3000,() => {
  console.log('running');
})
```

