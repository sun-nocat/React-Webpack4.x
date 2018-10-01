# React-Webpack4.x

- 基于Webpack4.x的React学习过程



## 创建基本的webpack4.x项目

- 1.运行 `npm init -y` 快速初始化项目

- 2.在项目里创建`src`和`dist`目录

- 3.在src目录下创建`index.html`,`index.js`

- 4.使用npm安装webpack   `npm i webpack -D`   npm i `webpack-cli -D`

- 5.在项目的根目录创建webpack.config.js文件。用来配置webpack

  ~~~js
  //webpack.config.js
  //向外暴露一个大包的配置对象，因为webpack是基于node构建的，所以支持所有的node语法。
  module.exports = {
      mode :'production',//设置是开发环境好还是声场换将  production

  }
  ~~~

  ​

- 6.注意：webpack4.x提供了约定大于配置，目的是尽量减少配置文件的体积
  - 默认约定了：
  - 打包的入口文件 `src` -> `index.js`
  - 打包的输出文件是 `dist` -> `main.js`
  - 4.x中新增了mode选项(必选)，可选的值为 `development` 和 `production`
  - 安装 npm i webpack-dev-server -D  用来自动打包
  - 安装 npm i html-webpack-plugin -D  将html放在内存中

- 7.webpack-dev-server的使用

  - 首先 npm install webpack-dev-server -D 安装

  - 然后在package.json中进行配置

    ~~~js
    "script":{
        "dev":"webpack-dev-server --open --port 3000 --hot"
    }
    ~~~

  - 在script中配置dev属性之后，就可以在命令行中使用 npm run dev 来使用 webpack-dev-server 了。

  - --open是指运行命令之后会自动打开浏览器，--port是用来指定打开的短空，--hot使用用来指定热更新的。

  - webpack会默认将文件打包到localhost:3000/main.js的位置。所以在index.html中，只需要使用    <script src="/main.js"></script>  来引入打包之后的文件

- 8.html-webpack-plugin的使用

  - 用来将页面保存在内存中，提高开发的效率


  - 首先使用 npm install html-webpack-plugin -D 安装

    - 在webpack.config.js文件中进行插件配置

      ~~~
      const path = require('path')
      const HtmlWebpackPlugin = require('html-webpack-plugin')
      //导入在内存中自动声场html的插件

      //创建一个插件的实力对象
      const htmlPlugin = new HtmlWebpackPlugin({
          template: path.join(__dirname,'./src/index.html'),//源文件
          filename: 'index.html' //生成内存中首页的名称
      })


      //向外部暴露一个打包的配置对象  因为日webpack是基于NOde构建的，所以webpack支持所有node语法
      module.exports = {

          mode:'development',//development   production  开发环境和生产环境的选项 不同与是否打包
          //在webpack4.x中 有一个很大的特性，就是  约定大于配置，约定的打包入口文件是src下的index.js
          plugins:[
              htmlPlugin
          ]

          // export default {}
          //这是ES6中 向外导出模块的API 与之对应的是 import*** from '标识符'
          //那些特性node支持？ 如果浏览器支持那些，则Node就支持那些
      }
      ~~~

    - 因为插件会将打包之后的main.js文件插入到index.html文件中，所以不需要再index.html文件中手动引入main.js文件。

## JSX语法
> 什么是JSX语法，符合html规范的JS语法；

### 如何使用jsx语法？
- 安装`babel`插件
  - 运行 `npm install babel-core babel-loader babel-plugin-transform-runtime -D`
  - 运行 `cpm install babel-preset-env babel-preset-stage-0 -D`
- 安装能够识别转换jsx语法的包`babel-preset-react`
  - 运行 `npm install babel-preset-react -D`


## 在项目中使用react
- 运行 `npm install react react-dom -S` -s 指从开发到上线都要用到的模块