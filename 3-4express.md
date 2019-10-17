## express

### 路由

**路由**是指应用程序端点（URI）的定义以及它们如何响应客户端请求。

```js
// GET method route
app.get('/', function (req, res) {
  res.send('GET request to the homepage')
})

// POST method route
app.post('/', function (req, res) {
  res.send('POST request to the homepage')
})

app.all('/secret', function (req, res, next) {
  console.log('Accessing the secret section ...')
  next() // pass control to the next handler
})
```

其他方法：

`get`，`post`，`put`，`head`，`delete`，`options`，`trace`，`copy`，`lock`，`mkcol`，`move`，`purge`，`unlock`，`report`，`mkactivity`，`checkout`，`merge`，`m-search`，`notify`，`subscribe`，`unsubscribe`，`patch`和`search`。

路由转换为无效JavaScript变量名称的方法：

`app['m-search']('/', function ...`

##### 路由路径

路径路径可以是字符串，字符串模式或正则表达式。

##### 路线参数

```js
Route path: /users/:userId/books/:bookId
Request URL: http://localhost:3000/users/34/books/8989
req.params: { "userId": "34", "bookId": "8989" }
```

##### 路由处理程序

路由处理程序可以采用函数，函数数组或两者的组合的形式。

`next('route')`绕过剩余的路由回调。

##### response响应方法

| 方法               | 描述                                                   |
| :----------------- | :----------------------------------------------------- |
| res.download()     | 提示要下载的文件。                                     |
| res.end()          | 结束响应过程。                                         |
| res.json（）       | 发送JSON响应。                                         |
| res.jsonp（）      | 用JSONP支持发送JSON响应。                              |
| res.redirect（）   | 重定向请求。                                           |
| res.render（）     | 呈现视图模板。                                         |
| res.send（）       | 发送各种类型的响应。                                   |
| res.sendFile（）   | 以八位字节流的形式发送文件。                           |
| res.sendStatus（） | 设置响应状态代码并将其字符串表示形式作为响应主体发送。 |
| res.status（）     | 设置响应状态代码                                       |

##### app.all()

##### app.route()

```js
app.route('/book')
  .get(function (req, res) {
  res.send('Get a random book')
})
  .post(function (req, res) {
  res.send('Add a book')
})
  .put(function (req, res) {
  res.send('Update the book')
})
```



### 使用中间件

**中间件**功能是可以访问请求对象（`req`），响应对象（`res`）以及应用程序请求 - 响应周期中的下一个中间件功能的函数。下一个中间件函数通常用名为`next`的变量表示。

中间件功能可以执行以下任务：

- 执行任何代码。

- 对请求和响应对象进行更改。

- 结束请求 - 响应循环。

- 调用堆栈中的下一个中间件功能。

如果当前的中间件功能没有结束请求 - 响应周期，则它必须调用`next()`以将控制传递给下一个中间件功能。否则，请求将被挂起。

```js
var express = require('express')
var app = express()

var myLogger = function (req, res, next) {
  console.log('LOGGED')
  next()
}

app.use(myLogger)

app.get('/', function (req, res) {
  res.send('Hello World!')
})

app.listen(3000)
```

##### 可配置的中间件

```js
//File: my-middleware.js
module.exports = function(options) {
  return function(req, res, next) {
    // Implement the middleware function based on the options object
    next()
  }
}
//使用中间件
var mw = require('./my-middleware.js')
app.use(mw({ option1: '1', option2: '2' }))
```

Express应用程序可以使用以下类型的中间件：

- Application-level middleware

- 路由器级中间件

- 错误处理中间件

- 内置中间件

- 第三方中间件

##### Application-level middleware

这个例子显示了没有安装路径的中间件功能。每次应用程序收到请求时都会执行该功能。

```js
var app = express()

app.use(function (req, res, next) {
  console.log('Time:', Date.now())
  next()
})
```

此示例显示`/user/:id`路径上安装的中间件功能。该函数针对`/user/:id`路径上的任何类型的HTTP请求执行。

```js
app.use('/user/:id', function (req, res, next) {
  console.log('Request Type:', req.method)
  next()
})//      /user/007/hello/123
```

这个例子显示了一个路由及其处理函数（中间件系统）。该函数处理对`/user/:id`路径的GET请求。

```js
app.get('/user/:id', function (req, res, next) {
  res.send('USER')
})//      /user/007   /hello/123
```

下面是一个在装载点加载一系列中间件功能的例子，带有装载路径。它演示了一个中间件子堆栈，用于打印任何类型的HTTP请求到`/user/:id`路径的请求信息。

```js
app.use('/user/:id', function (req, res, next) {
  console.log('Request URL:', req.originalUrl)
  next()
}, function (req, res, next) {
  console.log('Request Type:', req.method)
  next()
})
```

此示例显示处理GET请求到`/user/:id`路径的中间件子堆栈。

```js
app.get('/user/:id', function (req, res, next) {
  console.log('ID:', req.params.id)
  next()
}, function (req, res, next) {
  res.send('User Info')
})

// handler for the /user/:id path, which prints the user ID
app.get('/user/:id', function (req, res, next) {
  res.end(req.params.id)
})
```



######  next('route')

```js
app.get('/user/:id', function (req, res, next) {
  // if the user ID is 0, skip to the next route
  if (req.params.id === '0') next('route')
  // otherwise pass the control to the next middleware function in this stack
  else next()
}, function (req, res, next) {
  // render a regular page
  res.render('regular')
}, function (req, res, next) {
  // render a regular page
  res.render('regular')
}, function (req, res, next) {
  // render a regular page
  res.render('regular')
})

// handler for the /user/:id path, which renders a special page
app.get('/user/:id', function (req, res, next) {
  res.render('special')
})
```

##### 路由器级中间件

```js
var app = express()
var router = express.Router()

// a middleware function with no mount path. This code is executed for every request to the router
router.use(function (req, res, next) {
  console.log('Time:', Date.now())
  next()
})

// a middleware sub-stack shows request info for any type of HTTP request to the /user/:id path
router.use('/user/:id', function (req, res, next) {
  console.log('Request URL:', req.originalUrl)
  next()
}, function (req, res, next) {
  console.log('Request Type:', req.method)
  next()
})

// a middleware sub-stack that handles GET requests to the /user/:id path
router.get('/user/:id', function (req, res, next) {
  // if the user ID is 0, skip to the next router
  if (req.params.id === '0') next('route')
  // otherwise pass control to the next middleware function in this stack
  else next()
}, function (req, res, next) {
  // render a regular page
  res.render('regular')
})

// handler for the /user/:id path, which renders a special page
router.get('/user/:id', function (req, res, next) {
  console.log(req.params.id)
  res.render('special')
})

// mount the router on the app
app.use('/', router)
```

##### 错误处理中间件

错误处理中间件始终需要**四个**参数。您必须提供四个参数来将其标识为错误处理中间件功能。即使您不需要使用该`next`对象，也必须指定它以维护签名。否则，该`next`对象将被解释为常规中间件，并且将无法处理错误。

```js
app.use(function (err, req, res, next) {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})
```

##### 内置中间件

Express具有以下内置中间件功能：

- express.static提供静态资产，如HTML文件，图像等。

- express.json使用JSON有效负载分析传入的请求。**注：适用于Express 4.16.0+**

- express.urlencoded使用URL编码的有效负载分析传入的请求。**注：适用于Express 4.16.0+**

##### 第三方中间件

https://github.com/senchalabs/connect#middleware



### 使用模板引擎

(dust|ejs|hbs|hjs|jade|pug|twig|vash)。 jade

1.`views`，模板文件所在的目录。例如：`app.set('views', './views')`。这默认为`views`应用程序根目录中的目录。

2.`view engine`，要使用的模板引擎。例如，要使用Pug模板引擎：`app.set('view engine', 'pug')`。

3.app.engine(ext, callback)

```javascript
app.engine('html', require('ejs').renderFile);
```

在这种情况下，EJS提供了一个具有Express期望的相同签名`(path, options, callback)`的`.renderFile()`方法，但请注意，它在`ejs.__express`内部将此方法进行了别名，因此如果使用“.ejs”扩展名，则不需要执行任何操作。

### 错误处理

您最后定义错误处理中间件，在其他`app.use()`路由之后并路由呼叫; 例如：

```js
var bodyParser = require('body-parser')
var methodOverride = require('method-override')

app.use(bodyParser.urlencoded({
  extended: true
}))
app.use(bodyParser.json())
app.use(methodOverride())
app.use(function (err, req, res, next) {
  // logic
})
```

```js
var bodyParser = require('body-parser')
var methodOverride = require('method-override')

app.use(bodyParser.urlencoded({
  extended: true
}))
app.use(bodyParser.json())
app.use(methodOverride())

//打印错误
app.use(logErrors)
//判断是否是ajax请求，如果是，响应500
app.use(clientErrorHandler)
//是页面请求，告诉你一个404的页面
app.use(errorHandler)

function logErrors (err, req, res, next) {
  console.error(err.stack)
  next(err)
}

function clientErrorHandler (err, req, res, next) {
  if (req.xhr) {
    res.status(500).send({ error: 'Something failed!' })
  } else {
    next(err)
  }
}

function errorHandler (err, req, res, next) {
  res.status(500)
  res.render('error', { error: err })
}

```



### 调试Express

Mac or linux:

```javascript
$ DEBUG=express:* node index.js
```

windows:

```javascript
set DEBUG=express:* & node index.js
```



### 补充

##### Request 对象

 request对象表示HTTP请求，包含了请求查询字符串，参数，内容，HTTP头部等属性。常见属性有：

1. req.app：当callback为外部文件时，用req.app访问express的实例
2. req.baseUrl：获取路由当前安装的URL路径
3. req.body / req.cookies：获得「请求主体」/ Cookies
4. req.fresh / req.stale：判断请求是否还「新鲜」
5. req.hostname / req.ip：获取主机名和IP地址
6. req.originalUrl：获取原始请求URL
7. req.params：获取路由的parameters
8. req.path：获取请求路径
9. req.protocol：获取协议类型
10. req.query：获取URL的查询参数串
11. req.route：获取当前匹配的路由
12. req.subdomains：获取子域名
13. req.accpets（）：检查请求的Accept头的请求类型
14. req.acceptsCharsets / req.acceptsEncodings / req.acceptsLanguages
15. req.get（）：获取指定的HTTP请求头
16. req.is（）：判断请求头Content-Type的MIME类型

##### Response 对象

response对象表示HTTP响应，即在接收到请求时向客户端发送的HTTP响应数据。常见属性有：

1. res.app：同req.app一样
2. res.append（）：追加指定HTTP头
3. res.set（）在res.append（）后将重置之前设置的头
4. res.cookie（name，value ，option）：设置Cookie
5. opition: domain / expires / httpOnly / maxAge / path / secure / signed
6. res.clearCookie（）：清除Cookie
7. res.download（）：传送指定路径的文件
8. res.get（）：返回指定的HTTP头
9. res.json（）：传送JSON响应
10. res.jsonp（）：传送JSONP响应
11. res.location（）：只设置响应的Location HTTP头，不设置状态码或者close response
12. res.redirect（）：设置响应的Location HTTP头，并且设置状态码302
13. res.send（）：传送HTTP响应
14. res.sendFile（path ，options）：传送指定路径的文件 -会自动根据文件extension设定Content-Type
15. res.set（）：设置HTTP头，传入object可以一次设置多个头
16. res.status（）：设置HTTP状态码
17. res.type（）：设置Content-Type的MIME类型





