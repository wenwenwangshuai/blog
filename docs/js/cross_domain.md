# JavaScript之请求跨域

---

## 跨域的产生

**浏览器同源策略**

同源策略是浏览器最基本的最核心的安全功能，A 网页的 cookie B 网页不能使用，除非这两个网页同源。同源即"协议 + 域名 + 端口"三者相同（两个不同的域名指向同一个 ip 地址也非同源）

在进行异步网络请求的时候，如果请求的地址与当前地址的`域名(ip)`、 `协议`、 `端口`中有任何一个不同就会产生跨域。

## 解决跨域方案

---

### JSONP (JSON with Padding)

* 利用浏览器允许 <script> 下载不同网站的 JS 脚本
* 通过手动创建一个 script 标签
* 相当于在客户端提供一个接口供服务器调用。不过一般服务器对客户端是 1 对多的模式，所以通常由客户端将本地提供的接口（函数）通过传递参数的形式传递给服务器。

```html
//index.html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  
</head>
<body>
    <script src="./demo.js"></script>
</body>
</html>
```

```js
//demo.js
var script = document.createElement('script');
script.src = 'http://127.0.0.1:8880?callback=sayHello';
document.head.appendChild(script);

// 传递给后台的接口函数,这个函数的参数可以由后台提花
function sayHello(msg) {
  console.log(msg)
}

// 本地的测试函数，没有显示传递给后台
function demo() {
  console.log('这是前台的函数')
}
```

```js
//server.js
//服务器端
var qs = require('querystring')
var http = require('http');
var server = http.createServer(function (req, res) {
  var params = qs.parse(req.url.split('?')[1]);
  var fn = params.callback;
  const msg = '后台已经收到'

  const ret = fn + '("' + msg + '")'; // sayHello("后台已经收到")
  fn && res.write(ret) //调用前端提供的函数接口，并传递数据给前端
  res.write(';demo()') //调用前台的其他函数
  res.write(';document.title="通过后台修改前台的网页标题"') //
  res.end();
});

server.listen(8880, function () {
  console.log('Server is running at port 8880...');
});
```

* 当访问 index.html 时 浏览器控制输出

```
后台已经收到
这是前台的函数
```

**缺点**

* 只能实现 get 一种请求
* 前端的数据可能遭受到服务器的恶意修改（上面的后台修改掉前台的网站标题）虽然我们信任服务器，但对前后台分离开发模式下，我前端不想被你后台横插一脚。

### document.domain + iframe

* 只适用于顶级域名相同的情况
* 例： demo1.example.com  想获取 demo2.example.com 的数据 
  1. 在 demo1.example.com 下设置当前的 domain document.domain = 'xxx'
  2. 在 demo1.example.com 下通过 iframe 加载 demo2.example.com
  3. 修改 demo2.example.com 的 domain 和 setp 1 的 domain 一致。
  4. 这个时候就可以在 demo1.example.com 下通过 iframe 获取 demo2.example.com 的 window 对象

### location.hash + iframe 跨域

* 和 document.domain + iframe 类似
* 使用 window.onhashchange 进行双向交流，父窗口可以对 iframe 的 url 进行读写，iframe 也可以对父窗口的 url 进行读写

### 跨域资源共享（CORS）

* 服务器设置 Access-Control-Allow-Origin
* 也是常用的方法

### Nginx 反向代理

* 通过 Nginx 设置反向代理访问我们需要请求的资源
* 跨域受浏览器（同源策略）影响，但服务器上的 Nginx 是不受跨域限制（没有浏览器的同源策略）
* 通过 Nginx 设置代理，当 A 访问 B 跨域时，我们可以设置一个 Nginx（C）帮我们转发请求，就变成了 A->C->B

### postMessage + iframe onload

* postMessage 允许用户在两个窗口或 iframe 之间传递数据，无论这个 window 对象是不是同源都能发送。