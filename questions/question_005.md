## 前端知识小拷问 005 资源、bug管理相关
---
今天的前端知识点有如下：

* 如果不想让别人盗用你的图片，访问你的服务器资源该怎么处理？
* 面对精灵图和`base64`如何选择？
* `webpack`怎么引入第三方的库？
* `git`如何管理线上的`bug`？
* `nginx`有哪些好用的功能？
* 仓库地址：https://github.com/RiversCoder/fontend-question-ten-everyday

>1. 如果不想让别人盗用你的图片，访问你的服务器资源该怎么处理？（图片防盗链）

* 如果是第三方云存储（阿里云等）：直接设置`IP`白名单，非对应`IP`禁止访问
* 如果是类似`nginx`服务：可以匹配对应的资源，判断`refer`，再决定是否返回正确图片资源

>2. 面对精灵图和base64如何选择？

* 精灵图：
            * 原理：所有零星图片都包含到一张大图中，`background-position`属性定位某个图片位置，来达到在大图片中引用某个部位的小图片的效果
            * 优点：减少`http`请求；减少字节总数；
            * 缺点：合并小图，工作量大；若经常改变，维护麻烦；
            * 适用场景： 变动少的图标，表情等；多应用小图片；
* base64:
            * 原理：将资源原本二进制形式转成以`64`个字符基本单位，所组成的一串字符串。
            * 优点：处于`html`中，减少请求；避免跨域；
            * 缺点：低版本浏览器不兼容；体积更大；`css`使用过多不利于加载；
            * 适用场景：很小的图片；雪碧图不利处理的图片（背景平铺图片）

>3. webpack怎么引入第三方的库？

* 最简单方法是：使用`html-webpack-plugin`的模板`template`，直接引入`cdn`第三方库

**模板文件 template/index.ejs**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>third library</title>
</head>
<body>
    <script src="https://cdn.bootcss.com/jquery/3.3.1/jquery.min.js"></script>
</body>
</html>
```
**webpack.config.js配置***
```js
var HtmlWebpackPlugin = require('html-webpack-plugin')
    
webpackconfig = {
    ...
    plugins: [
        new HtmlWebpackPlugin({
            template: 'template/index.ejs'
        })
    ]
}
```

* 使用`ProvidePlugin`插件
```js
const webpack = require('webpack')
module.exports = {
    plugins: [
        new webpack.ProvidePlugin({
            $: 'jquery'
        })
    ]
}
```

* 使用`exports-loader`全局暴露变量
```js
module: {
    rules: [
        {
             test: require.resolve('jquery.min.js'), // 这里也可以换成jquery模块 npm install jquery
             use: 'exports-loader?$'
       }
    ]
  }
```

>4. git如何管理线上的bug？

**方法1：在当前主分支修改bug**

* 暂存当前的改动的代码，目的是让工作空间和远程代码一致：`git stash`
* 修改完`bug`后提交修改：
```shell
git add .
git commit -m "bug one"
git push
```
* 从暂存区把之前的修改恢复，这样就和之前改动一样了: `git stash pop`
* 如有冲突，需要解决

**方法2：拉一个新分支修改**

* 暂存一下工作空间改动：`git stash`
* 新建一个分支，并且换到这个新分支: `git checkout -b edit_bug`
* 在分支`edit_bug`上修改`bug`，提交 `git push`
* 将代码合并到`master`， 提交
* 恢复代码，`git stash pop`
* 如有冲突，需要解决

> 5. nginx有哪些好用的功能？

* 静态`http`服务器
* 反向代理服务器
* 负载均衡，自动分配请求到多台服务器
* 虚拟主机，将多个网站部署在同一台服务器上

