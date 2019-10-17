## EJS

##### 什么是EJS

EJS是一个简单高效的模板语言，通过数据和模板，可以生成HTML标记文本。可以说EJS是一个JavaScript库，EJS可以同时运行在客户端和服务器端，客户端安装直接引入文件即可，服务器端用npm包安装。

##### EJS的特点

快速编译与绘制输出

简洁的模板标签：<% %>

自定义分割符（例如：用 <? ?> 替换 <% %>）

引入模板片段

同时支持服务器端和浏览器 JS 环境

JavaScript 中间结果静态缓存

模板静态缓存

兼容 express视图系统

##### EJS的成员函数

render(str,data,[option]):直接渲染字符串并生成html

str：需要解析的字符串模板

data：数据

option：配置选项

##### EJS的常用标签

<%= %>输出标签  （原文输出HTML标签）

<%- %>输出标签   （HTML会被浏览器解析）

<% %>流程控制标签 (if    for    while    arr.forEach)

<%# %>注释标签

% 对标记进行转义

##### Includes

```js
<ul>
  <% users.forEach(function(user){ %>
    <%- include('user/show', {user: user}); %>
  <% }); %>
</ul>
```













## 静态资源服务器

>npm i http-server -g
>
>静态资源服务器
>
>npm i chalk 
>
>修饰console
>
>npm i nodemon -g
>
>监听node程序的变化，重新node命令



##### MIME

Content-Type

##### 文件压缩

accept-encoding       浏览器可以接受的压缩格式是哪些   request headers

Content-Encoding       服务器告诉浏览器数据采用的压缩格式是什么。  response header

##### 范围请求

range: bytes=[start]-[end]

Accept-Ranges: bytes

Content-Range: bytes start-end/total

Content-Length: count

##### 缓存

强制缓存:

Expires  设置过期时间。  2019.10.30。    http1.0

Cache-Control      设置缓存时间 600s。

协商缓存：

If-Modified-Since/Last-Modified

If-None-Match/ETag





客户端第一次发送请求

得到了服务器的数据后缓存下来



客户端第二次发送请求

检查是否有缓存

没有缓存：重新请求服务器

有：判断缓存是否过期。没有过期，直接用缓存状态是200

过期了：取服务器，服务器获得请求后，不直接告诉客户端数据

服务器先判断这个文件是否修改过，如果修改过，告诉客户端新的数据

如果没有修改过，那么就告诉客户端虽然过期了，但是客户端的缓存还是可以使用的。

更新客户端 的过期时间。

























































