# vue.js相关问题

### 1.Vue双向数据绑定的实现
* [JavaScript数据双向绑定的简单演示](http://div.io/topic/1645)
* [Vue双向绑定的实现原理Object.defineproperty](https://www.w3cplus.com/vue/vue-two-way-binding-object-defineproperty.html)
* [剖析Vue原理&实现双向绑定MVVM](https://segmentfault.com/a/1190000006599500) 

### 2.Vue和react区别
* 相同点：
    * 都用了virtual dom的方式, 性能都很好
    * ui上都是组件化的写法，开发效率很高
* 不同点：
    * Vue的优势是：双向数据绑定，适合不会持续的，小型的web应用，使用vue.js能带来短期内较高的开发效率，当工程规模比较大时双向数据绑定会很难维护
    * react的优势是：单向数据绑定，更适合大型应用和更好的可测试性，Web端和移动端原生APP通吃，更大的生态系统，更多的支持和好用的工具
* 其他不同：
    
    > React 推荐的做法是 JSX + inline style，也就是把 HTML 和 CSS 全都整进 JavaScript 了。Vue 的默认 API 是以简单易上手为目标，但是进阶之后推荐的是使用 webpack + vue-loader 的单文件组件格式
    
    > JSX 在逻辑表达能力上虽然完爆模板，但是很容易写出凌乱的 render 函数，不如模板看起来一目了然










