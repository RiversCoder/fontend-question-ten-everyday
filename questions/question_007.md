## 前端知识小拷问 007 vue、react、angular 相关
---
今天的前端知识点有如下：

* `vue`与`react`的对比，如何选型？从性能，生态圈，数据量，数据的传递上，作比较
*  `vue slot` 是做什么的?
* `vue`和`angular`的优缺点以及适用场合?
* `vue` 路由实现原理?
* `vue`的双向绑定的原理，和`angular`的对比？

* 仓库地址：https://github.com/RiversCoder/fontend-question-ten-everyday

> 1. `vue`与`react`的对比，如何选型？从性能，生态圈，数据量，数据的传递上，作比较

### 共同点

* 都是基于组件化的开发思想
* 同属于MVVM类型的框架
* 都通过虚拟DOM实现快速渲染

### 不同点比较

* 性能：目前来看，`vue`的性能是优于`react`的
* 生态圈：
    （1）vue: vue+vue-router+vuex+单文件组件+(iview/element…)+es6+webpack+unit/e2e
    （2）react：react+react-router+redux+es6+webpack+enzyme
* 数据量：简单好用，快速开发请选择`vue`；大型多端大生态圈，请选择`react`；
* 数据的传递：
    （1）vue: 父 -> 子，`props`；子 -> 父，`emit`；
    （2）react: 父 -> 子，`props`；子 -> 父，利用父传给子组件的函数回调`callback`传递；

> 2.   `vue slot` 是做什么的?

* 定义：插槽，在父组件内向子组件内部插入自定义的内容时候用到
* 分类：具名插槽，匿名插槽

> 3. `vue`和`angular`的优缺点以及适用场合?

* `vue` 更好用，更轻量级，双向绑定更简单
* `angular` 适合大型项目
* 参考文档：https://blog.csdn.net/powertoolsteam/article/details/79538230

> 4. `vue` 路由实现原理?

* 监听 `hashchange` 事件，然后在获取`hash`值，去匹配显示对应的组件

> 5. `vue`的双向绑定的原理，和`angular`的对比？

* `angular`: 脏检查机制，手动触发，性能难以优化
* `vue`: 依赖收集的观测机制，精确、主动地追踪数据的变化，将原生数据对象的属性改造为`getter`和`setter`
* 详细文档：https://elephantme.github.io/2016/07/31/two-way-bind-beween-angular-and-vue/


