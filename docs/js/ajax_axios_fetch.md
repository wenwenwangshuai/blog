# AJAX、Axios和Fetch

---

## 前言

前端这几年的高速发展，让人大叫真的学不动了。前后端交互方式也大大的升级了，现在经常用的三种交互方式，ajax、axios 和 fetch，他们之间的不同也常常是面试的重点，接下来我们就聊聊他们。

## Ajax

Ajax 即“Asynchronous Javascript And XML”（异步 JavaScript 和 XML），是指一种创建交互式、快速动态网页应用的网页开发技术，无需重新加载整个网页的情况下，能够更新部分网页的技术，俗称的局部刷新。
Ajax 的核心就是应用了 XMLHttpRequest 对象，通过这个对象，就可以实现在不重载页面的情况与 Web 服务器交换数据，即在不需要刷新页面的情况下，就可以产生局部刷新的效果。
在运用原生 JS 时，对 AJAX 的封装往往使人头疼，在 Promise 还没出现的时代，回调函数一不小心就带你展现什么是地狱级别。
随着 Jquery 的出现，AJAX 也变的简单了起来，Jquery 内部封装了一个 AJAX。

```js
$.ajax({
  type: "POST",
  url: url,
  data: data,
  dataType: dataType,
  success: function () {},
  error: function () {},
});
```

Jquery 的 AJAX 是对原生 AJAX 的封装，使 AJAX 用起来更加的简单，并且支持 JSONP，已经将 AJAX 封装的很完美了，但是随着三大框架的出现，Jquery 慢慢的也退出了历史的舞台，想要用 Jquery 封装的 AJAX，必须引入体积庞大的 Jquery，这样很不利于项目的优化，此时 Axios 出现在了大众的视野。

## Axios

Axios 是一个第三方提供的方法，它与 AJAX 一样，都是对 XMLHttpRequest 对象进行封装，并加入了 Promise 方法解决了回调地狱的问题，提供了可使用的大量的 API。

```js
axios({
  method: "post",
  url: url,
  data: data,
})
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

Axios 能被大量的使用，主要是拥有如下几个特点：

* 支持 node 端和浏览器端
* 支持 Promise
* 丰富的配置项
* 社区支持
* 客户端支持防止 CSRF

## Fetch

Fetch 是对原生的 XMLHttpRequest 对象一个替代的方案，它更加底层，所以用起来也是更加的耐人寻味。

它同样是用 Promise 进行的封装，但是与 Axios 不同的是：
* 当接收到一个代表错误的 HTTP 状态码时，从 fetch() 返回的 Promise 不会被标记为 reject， 即使响应的 HTTP 状态码是 404 或 500。相反，它会将 Promise 状态标记为 resolve （但是会将 resolve 的返回值的 ok 属性设置为 false ），仅当网络故障时或请求被阻止时，才会标记为 reject。
* fetch 不会发送 cookies。除非你使用了 credentials 的初始化选项。（自 2017 年 8 月 25 日以后，默认的 credentials 政策变更为 same-origin。）
* fetch() 可以接受跨域 cookies；也可以使用 fetch() 建立起跨域会话。

```js
fetch(url)
  .then(function (response) {
    return response.json();
  })
  .then(function (myJson) {
    console.log(myJson);
  });
```

Fetch 与 Axios 最大的不同，就是 Fetch 在第一次 then 返回的是一个 HTTP 响应，而不是真的 JSON。为了获取 JSON 的内容，我们需要使用 json() 方法。

三者比较还是觉得 Axios 更胜一筹。