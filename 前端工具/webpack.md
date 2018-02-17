# webpack 相关问题
### 1.对webpack的理解，和gulp有什么不同
* Webpack是模块打包工具，他会分析模块间的依赖关系，然后使用loaders处理它们，最后生成一个优化并且合并后的静态资源。

* gulp是前端自动化工具 能够优化前端工作流程，比如文件合并压缩

### 2.webpack打包速度慢，你觉得可能的原因是什么，该如何解决
模块太多
Webpack 可以配置 externals 来将依赖的库指向全局变量，从而不再打包这个库

### 3.webpack常用到哪些功能

设置入口  设置输出目 设置loader  extract-text-webpack-plugin将css从js代码中抽出并合并 处理图片文字等功能 解析jsx解析bable
### 4.
