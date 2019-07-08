## 前端知识小拷问 002
---
>1. 如何计算白屏、首屏时间？

* 白屏时间：`<head>` 标签解析完就是白屏的结束时间点，在`head`标签中前后打点，计算差值  
* 首屏时间：首屏时间是指用户打开网站开始，到浏览器首屏页面内容渲染完成的时间，重要；由于在页面上可能存在很多异步加载的需求，所以建议最好使用`devtool`中的`timeline`工具


> 2. 什么是闭包？

* 闭包就是能够读取其他函数内部变量的函数


> 3. 什么是作用域链？

* 作用域是针对变量的
* 作用域的特点就是，先在自己的变量范围中查找，如果找不到，就会沿着作用域逐级往上查找变量。


> 4. ajax的实现，readyState中的五种状态分别代表什么含义？

* ajax请求实现调用

```js
var getXmlHttpRequest = function () {
    if (window.XMLHttpRequest) {
        //主流浏览器提供了XMLHttpRequest对象
        return new XMLHttpRequest();
    }
    else if (window.ActiveXObject) {
        //低版本的IE浏览器没有提供XMLHttpRequest对象
        //所以必须使用IE浏览器的特定实现ActiveXObject
        return new ActiveXObject("Microsoft.XMLHTTP");
    }
};
var xhr = getXmlHttpRequest();
xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && xhr.status === 200) {
        //获取成功后执行操作
        //数据在xhr.responseText
    }
};
xhr.open("TYPE", "URL", true);
xhr.send("");
```

* readyState中的五种状态

状态码 | 代表的含义 
:-: | :-: 
0 | 未初始化状态  初始化`xhr`对象
1 | 准备发送状态  调用`open`
2 | 已经发送状态  调用`send`
3 | 正在接收状态  响应到`HTTP`响应头部信息
4 | 响应完成状态  完成了`HTTP`响应的接收

* 目前则更多的是使用 `onload` 方法

> 5. 如何实现 jsonp？
* 定义一个函数，用于处理接收到的跨域数据。
* 创建一个script节点，然后`src`属性上拼接发送的目的`URL`以及`callback`字符参数。
* 在跨域服务器端接收`GET`请求，获取`cabback`参数，拼接好，返回数据。
* 删除之前生成的script节点。
