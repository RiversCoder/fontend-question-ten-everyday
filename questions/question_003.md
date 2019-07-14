## 前端知识小拷问 003
---
>1. 处理跨域的几种方式？

**浏览器配置**

* jsonp跨域，优点：浏览器支持广泛，方便快捷 缺点：只支持`get`请求，不支持`https`
* `iframe`请求，访问`iframe`加载出的内容，缺点：只适用于顶级域名相同的情况
* `window.name` 跨域 好用，推荐；缺点：只适用于两个iframe之间的跨域； 参考文档：https://www.cnblogs.com/zhuzhenwei918/p/7403796.html
* `h5`新特性`postMessage` 通信， 好用，推荐；缺点：不能和服务器交换数据，只能在两个窗口（`iframe`）之间交换数据；

** 第三方配置 **

* 后台服务配置允许跨域，例如`node.js`
* 客户端配置代理，例如：`nginx`，`node.js` 等
* `webSocket`协议跨域，参考文档：https://www.cnblogs.com/goeasycloud/p/9389360.html

**参考文档**

* 跨域的详解请参考文档：https://blog.csdn.net/weixin_30363263/article/details/81587025


> 2. 如何压缩CSS，JS代码？

**gulp**

* 使用`gulp-uglify`压缩`javascript`
* 使用`gulp-clean-css`压缩`css`

**webpack**

* 使用`uglifyjs-webpack-plugin`压缩js
* 使用`mini-css-extract-plugin`抽离压缩css


> 3. get和post的区别？

**功能上：**
* `get` -> 拉取数据，`post`  -> 推送数据

**使用上**
* `get`参数特点：地址栏明文可见，长度限制，可缓存，安全性低；
* `post`参数特点：采用`send`发送数据，无长度限制，不可缓存，安全性高；

***详细文档**
https://blog.csdn.net/m_nanle_xiaobudiu/article/details/81063997

> 4. 什么是事件模型？

**事件模型种类**

* 原始事件模型(`DOM0`级)、`DOM2`事件模型、`IE`事件模型

**原始事件模型**

* 描述：标签绑定事件
* 优点：兼容所有浏览器
* 缺点： 逻辑结构未分离；单独绑定，后面覆盖前面的绑定；不支持事件委托、冒泡等

**DOM2事件模型**

* 描述：`W3C`标准模型，现代浏览器所支持；一次事件发生包含三个过程：（1）事件捕获（2）事件目标（3）事件冒泡
![]() 展示
* 阻止事件传播：（1）`stopPropagation()` （2）`IE`下使用`cancelBubble=true`（3）
* 绑定事件：`addEventListener("eventType","handler","true|false");`

**IE事件模型**

* 描述：`IE`把事件作为全局对象`window`的一个属性
* 事件传播：（1）先执行元素的监听函数（2）然后事件沿着父节点一直冒泡到`document`
* 事件监听：（1）绑定`attachEvent( "eventType","handler")`（2）解除`detachEvent("eventType","handler" )`（3）注意`eventType`需要加上`on`

**详细文档**
https://www.cnblogs.com/leftJS/p/11068426.html

> 5. 如何编写一个元素拖拽的插件?

* *实现的核心要素**

* 获取当前元素相对于窗口文档的偏移量
* 鼠标按下元素的时候获取相对元素的偏移量`offsetX`和`offsetY`
* 鼠标移动时，监听`document`下的`clientX`与`clientY`，减去点击时的偏移量，即是当前元素的`left`和`top`的值

```js

module.exports = (dom) => {
    let startX = dom.getBoundingClientRect().left
    let startY = dom.getBoundingClientRect().top

    dom.onmousedown = function(ev){
        let offsetX = ev.offsetX
        let offsetY = ev.offsetY
        
        document.onmousemove = function(ev){
            dom.style.left = (ev.clientX - offsetX) + 'px'
            dom.style.top = (ev.clientY - offsetY) + 'px'
        }

        document.onmouseup = function(ev){
            document.onmouseup = dom.onmouseup = null
            document.onmousemove = null
        }
    }
}

```

