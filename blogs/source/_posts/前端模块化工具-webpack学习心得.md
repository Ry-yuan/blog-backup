---
title: 前端模块化工具--webpack学习心得
date: 2017-07-24 21:35:15
tags: webpack
---
## 话说前头
* webpack前段时间有听说一下，现在已经到了3.x的版本，作为一个前端小白前段时间没去接触太多。因为之前使用gulp来作为自己的项目构建工具。现在感觉gulp使用的趋势在减少。现在这段时间去接触了webpack，感觉很不错，它的模块化打包机制，对前端开发和性能方面都带来好处。这里不是说gulp不好，两者不作比较

*  接下来会说说自己对webpack使用的感受，我不会一步步写出使用webpack的流程，因为关于webpack的教程有很多，但会写一些关键地方，注意地方，来加深对webpack的见解。

* 学习就是这样，东看看西看看，看人家的对某件东西的见解，加上自己的理解，是否异同，慢慢积累，最终成为自己的知识。

## webpack介绍

### 1.（引用了webpack官网的一句话）：
> webpack 是一个现代 JavaScript 应用程序的模块打包器(module bundler)。当 webpack 处理应用程序时，它会递归地构建一个依赖关系图(dependency graph)，其中包含应用程序需要的每个模块，然后将所有这些模块打包成少量的 bundle - 通常只有一个，由浏览器加载。
它是高度可配置的，但是，在开始前你需要先理解四个核心概念：入口(entry)、输出(output)、loader、插件(plugins)。

### 2.个人理解：
这里说了这么多就是它能把项目中资源文件看成一个个模块，然后将他们打包成少量或一个文件，然后我们去引用这文件。

### 3.疑惑：
大家这里可能会疑惑，当时我也想，怎么能做到这个？怎么就打包成一个文件了？那么js，css，图片什么的怎么搞？还有这种操作？我能怎么办，那只能选择相信它。
### 4.感受：
其实学习某一样工具，我们只需要知道这东西能做什么，然后怎么用它，但它具体实现的细节，有时我们不必深究。我们只需知其然，不必知其所以然。尽管去用这个东西，它本来就是一个工具。就好比开一辆车，我们只需去学习怎么开，而不用太在意他为什么能开，开多了一样成为老司机，不是吗，没毛病吧。工具它能给我们带来便利，就足够了。除非你是制造工具的。但是如果对webpack非常感兴趣，可以去它的github上看看。

## webpack能做的事：
上面说webpack能打包模块，其实还有很多功能。
 * webpack可以对Js进行转译，当前浏览器很多不支持es6，但是我们想使用es6的语法，webpack可以将es6语法转成es5语法
* webpack可以对less，sass，stylus等css的预处理语言进行转译
* webpack可以热更新
* webpack可以对图片处理，压缩，转成base64格式。
* webpack可以对j代码进行压缩。
* webpack可以进行语法检查，可以生成自动化html模板等等

上面举例是常用，其功能还多得多。都是通过webpack 的 loader和plugins实现的，可以说是很强大了。


## webpack安装：
1. 前提有nodejs和npm，在网上搜索安装，现在的nodejs都会带有npm，所以直接安装nodejs即可。
2. 通过 cmd（用的是win操作系统）运行：node -v 和 npm -v 若都能返回版本号表明安装成功。
3.  接着正式安装webpack,命令行中运行：
```
//全局安装
npm install -g webpack
//创建一个文件夹
mkdir webpack-demo
//进入项目中
cd webpack-demo
//初始化，生成默认package.json 文件
npm init -y
//在当前项目中安装webpack
npm install webpack --save-dev
//到这里就安装成功了
```
>感受：整个流程和安装gulp差不多，是npm模块的那套安装流程。
说到npm，在国内推荐使用cnpm淘宝镜像，很不错，速度快很多。还有可以逛npm的官网去查询自己想要看的模块，里面都有模块的详细介绍。


## webpack的关键文件:webpack.config.js
*  webpack.config.js是webpack的配置文件，对项目中的webpack进行配置。
* 文件中用到的插件和loader需要先试用npm安装好：  
``` 
// 安装css-loader
npm install css-loader  --save-dev
// 安装htmlWebpackPlugin
npm install html-webpack-plugin --save-dev
```
* 项目根目录新建简单的webpack.config.js文件：
``` 
//引入模块
const webpack = require('webpack'); 
const path = require('path');
const htmlWebpackPlugin = require('html-webpack-plugin');
//配置
const config = {
  entry: './path/to/my/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'my-first-webpack.bundle.js'
  },
  module: {
    rules: [
      { test: /\.css$/, use: 'css-loader' }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};
```

* 这个文件中关键的东西就是上述提到的：四个核心概念：入口(entry)、输出(output)、loader、插件(plugins)。弄懂这四个核心的东西，webpack也就懂得差不多了。起码懂得怎么用。

* 各大核心的作用：
1. entry： 入口文件，也就是想要被打包的文件，这里可以是一个或者多个。
2. output： 输入文件，表示打包后的文件将会被输出到哪里，可以一个或多个。
3. module：模块，里面的rules是一个数组，存放则项目中需要用到的loader，loader可以对资源文件进行一系列的处理。常见的loader：style-loader，css-loader，less-loader，babel-loader，url-loader等等。
4. plugins：插件，为webpack添加所需的功能，如例子里面的是自动生成html模板插件。
更多细节在webpack的官网上查看。

## 最后再说说：
* 本次文章主要说说自己使用webpack时的一些想法和收获，可能写得不是很好，但这是个学习的过程，我很享受。
* 再提提，以前我不怎么喜欢去看一些官方的文档，因为全都是英文，自己英语也不是很好。但是后来硬着头皮看，发现在文档中学到的东西很多，也更有助于理解，有的文档写得很详细，会懂得很多。这过程中不会的英语单词就去查，顺便就补补英语，其实挺好。通过自己看文档，然后能用，能做，心里美滋滋。
