# vue-md-loader

> vue-md-loader


## 什么是webpack loader

`loader`用于对模块的源代码进行转换。`loader`可以使你在`import`或"加载"模块时预处理文件。因此`loader`类似于其他构建工具中“任务(task)”，并提供了处理前端构建步骤的强大方法。`loader`可以将文件从不同的语言（如 `TypeScript`）转换为 `JavaScript`，或将内联图像转换为 `data URL`。`loader`甚至允许你直接在 JavaScript 模块中`import CSS`文件。

由此可见，`loader`就像是一个“处理器”，输入特定的内容，处理后进行输出。当必要时，可以把一些合适的`loader`串起来使用，使前一个`loader`的输出变成后一个 `loader`的输入，最终得到自己想要的结果。

对于本文要提到的`markdown-loader`来说，它需要进行的处理就是，将 `markdown`文件内容解析并包装成一个与`vue`单文件组件内容相似的，然后传给它后面的`vue-loade`, 所以一个最简单的`vue markdown-loader`可以长这德性：

```
module.exports = function (src) {
  const res = (
    `<template>\n` +
    `<h1>hello world</h1>\n` +
    `</template>`
  )
  return res
}
```

## 手写封装自定义loader

### 文件目录结构
将自定义的markdown-loader放在文件夹rules内与webpack配置文件同级;
![](https://github.com/zuopf769/vue-md-loader/blob/master/src/assets/1559471956311-image.png)
这个存放路径看个人，是可以修改的，这里说明路径地址，是因为webpack配置中需要引用该路径


### webpack配置

 + 配置resolveLoader

webpack默认使用的loader路径为node_modules，可以直接在rules配置引用，

而自定义的loader，不在指定范围内是无法调用到的，即使在一开始声明require也无法正确使用，

便需要在此加入自定义loader的路径，增加webpack调用loader的范围

 + 增加module.rules
按照引用别的第三方loader一样配置

![](https://github.com/zuopf769/vue-md-loader/blob/master/src/assets/1559472162440-image.png)

### 安装需要的包

```
yarn add -D markdown-it markdown-it-anchor markdown-it-container markdown-it-emoji markdown-it-table-of-contents
```

```
包名称	功能说明
markdown-it	渲染 markdown 基本语法
markdown-it-anchor	为各级标题添加锚点
markdown-it-container	用于创建自定义的块级容器
markdown-it-emoji	渲染 emoji
markdown-it-table-of-contents	自动生成目录
highlight.js	代码高亮
```


### 样式
```
 "github-markdown-css" 、"normalize.css":
```
自定义部分需要自己添加 

[自定义](https://github.com/zuopf769/vue-md-loader/blob/master/src/style/main.scss)

```
:::tip
友情提示
:::
```

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```


## 参考文章

+ [webpack自定义loader 手写封装loader](https://blog.csdn.net/leeleejoker/article/details/81083428)
+ [自己撸个 vue markdown loader](https://segmentfault.com/a/1190000014666185)