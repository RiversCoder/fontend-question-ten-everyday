## 前端知识小拷问 004
---
今天的前端知识点有如下：

* 如何进行`cdn`托管，图片整合？
*  如何利用`webpack`把代码上传服务器以及转码测试？
* 项目上线流程是怎样的？
* 工程化怎么管理的?
* 如何编写一个元素拖拽的插件?
* 仓库地址：https://github.com/RiversCoder/fontend-question-ten-everyday

>1. 如何进行`cdn`托管，图片整合？

* cdn托管：把静态资源文件和动态网页分集群部署，静态资源会被部署到`CDN`节点上，网页中引用的资源也会变成对应的部署路径
* 图片整合：图片压缩、整合图片，减少请求（根据情况）、`base64`、使用`webp`、字体图标
* cdn参考文档：https://juejin.im/post/59a50dc1f265da246e6e108f

> 2. 如何利用`webpack`把代码上传服务器以及转码测试？

* 代码上传服务器：

（1）使用`SCP2`模块自动发布编译好的代码目录 ；参考文档：https://www.jianshu.com/p/a45868f29814
（2）使用`ftp-webpack-plugin`自动上传同步到`ftp`服务器；参考文档：https://github.com/varSmallRookie/ftp-webpack-plugin
（3）使用`gulp-sftp`直接上传到对应服务器目录，推荐，超简单; 参考文档：https://xiaozhuanlan.com/topic/1379680524

* 转码测试：

（1）webpack+babel可以编译代码成`es5`, 开启工具`devtool: 'inline-source-map'`浏览器错误定位测试；
（2）也可以使用`mocha`或者`karma`做单元测试

> 3. 项目上线流程是怎样的？

* 开发 -> 合并代码到`develop`分支 -> 开发环境 -> 自测 -> 合并代码到`stading`分支-> 测试环境 -> 测试 -> 合并代码到`master`分支 -> `gitlib`自动部署构建 ->线上部署

> 4. 前端工程化怎么管理的?

* 模块化 （`js/css`）
* 组件化（`ui`）
* 规范化 （目录结构、编码、文档、`git`管理、代码审查）
* 自动化（构建、部署、测试）
* 性能优化

**详细参考文档：**https://www.jianshu.com/p/0d0f268ec73d

> 5. `webpack` 和`gulp`对比，以及如何解决`webpack`打包文件太大的情况?

**webpack和gulp的对比**

* 侧重点： `webpack`更加侧重模块打包，`gulp`更加侧重任务的流程管理
* 详细文档：https://www.cnblogs.com/RuMengkai/p/6667321.html

**解决webpack打包文件太大的情况**

* 生产环境，建议关闭`devtool`中的`source-map`
* 剥离`css`文件，单独打包 （使用插件`extract-text-webpack-plugin`）
* 压缩`js`、`css`文件 （使用插件`UglifyJSPlugin`）
* 提取公共的依赖 （使用插件`CommonsChunkPlugin`）
* 开启`gzip`压缩 （使用插件`compression-webpack-plugin`）
* 压缩`html`文件，加上版本号 （使用插件：html-webpack-plugin）

