## 前端知识小拷问 001
---
>1. `prototype`和`__proto__`的关系是什么？

`prototype`和`__proto__`都指向原型对象；一个是原型，一个是原型链，原型创建可继承的方法和属性，原型链访问其构造方法的原型对象；
补充：
所有对象都有`__proto__`属性，函数这个特殊对象除了具有`__proto__`属性，还有特有的原型属性`prototype`。`prototype`对象默认有两个属性，`constructor`属性和`__proto__`属性。`prototype`属性可以给函数和对象添加可继承的方法、属性，而`__proto__`是查找某函数或对象的原型链方式。这个属性包含了一个指针，指回原构造函数

> 2. meta viewport 原理是什么？


* 参数：`width`、`initial-scale`、`minimum-scale`、`maximum-scale`、`height`、`user-scalable`
* layout viewport：通过`document.documentElement.clientWidth`来获取
* visual viewport： 通过`document.documentElement.innerWidth`来获取
* ideal viewport：`deal viewport` 是一个能完美适配移动设备的viewport
参考地址：[https://blog.csdn.net/zhouziyu2011/article/details/60570547](https://blog.csdn.net/zhouziyu2011/article/details/60570547)

> 3. 域名收敛与域名发散是什么？

* 域名收敛：又名`DNS`优化，将静态资源放在一个域名下
* 域名发散： http 静态资源采用多个子域名，目的是充分利用现代浏览器的多线程并发下载能力 


4. float和display:inline-block的区别是什么？

`display`是在`html`文档中的一个显示状态，`float`是针对块级元素的位置的浮动

5. 前端优化策略列举

<kbd>网络方面</kbd>
* 尽可能减少`http`的请求
* 图片脚本样式表等静态资源优化，压缩打包，雪碧图，使用`base64`，图标使用字体代替等
* 开启缓存：`DNS`缓存、`CDN`部署和缓存、`http`缓存
* 不要滥用 `web`字体

<kbd>DOM操作方面</kbd>
* `css`的文件放在头部，`js`文件放在尾部或者异步
* 减少频繁的`DOM`操作
* 做动画，尽量使用`css`动画
* 合理使用事件代理
* 在移动端使用`touchstart`、`touchend`代替`click`
* 开启`GPU`渲染加速

<kbd>数据方面</kbd>
* 图片加载，最好懒加载，有进度条预渲染最好
* `json`数据格式交互
* 常用数据缓存处理
