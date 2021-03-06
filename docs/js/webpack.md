# webpack入门

---

很多从事前端开发的程序员，都会接触到 webpack 非常熟悉的概念，但是我想很多人对webpack只是一知半解，知道这是一个打包器，可以将我们编写的Vue代码、React代码打包编译成原生的JS代码，方便浏览器识别。

但是对于webpack更底层的知识，比如：如何配置webpack，webpack为什么可以对我们的代码进行打包编译等，了解甚少。

## webpack基本简介

---

什么是webpack呢，下面我们引出 官方定义 ：

webpack 是一个现代 JavaScript 应用程序的静态模块打包器(module bundler)。当 webpack 处理应用程序时，它会递归地构建一个依赖关系图(dependency graph)，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 bundle。

![img](../img/js/webpack/1.png)

说的直白一点，就是讲我们的代码进行编译打包，变成能够被浏览器识别的前端脚本。就拿一个Vue项目为例：

一开始我们是用 Vue-cli脚手架 快速搭建一个项目，随后在项目中都是采用Vue语法来编写我们的项目，不仅如此，我们还会使用 ES6 语法，还会使用SCSS等CSS预处理器等等。

这些语法我们是熟悉的，但是浏览器不认识呀，浏览器能够识别的是原生JS语法，而且就目前情况来说，只能识别ES5语法，不能识别我们使用的ES6语法。这就意味着，我们的Vue项目是跑不起来的。这该怎么办呢？

这个时候webpack就开始发挥它的作用了，webpack通过分析Vue语法、理清代码模块之前的依赖关系、分析SCSS预处理器、分析项目中引用的图片等静态资源等，将这些浏览器不识别的语法进行打包编写编译，最终打包输出 `.js`、`.css`、`.jpg`、`.png` 等能够被浏览器识别的语法和文件。如此一来，我们的项目就可以顺利地在浏览器上面跑起来了。

## webpack的作用总结

---

结合上面的简单介绍，我们来总结一下webpack的作用：

**代码转换**
webpack可以将ES6语法转换为ES5语法，可以将LESS、SASS语法转换成CSS语法

**文件优化**
在webpack打包的过程中，可以合并文件，压缩文件体积

**代码分割、模块合并**
在开发的过程中，将一些公共的模块进行抽离，形成单独的模块，方便其他模块进行调用

**自动刷新**
即我们熟悉的热更新，在开发过程中，webpack会帮我们启动一个本地服务，每当产生新代码的时候，该服务会自动刷新，然我们看到最新的页面

**代码校验**
在开发过程中，webpack可以帮助我们检查代码语法规范，减少bug的数量

**自动发布**
项目开发完成之后，我们可以借助webpack帮助我们自动发布代码，部署到服务器上
