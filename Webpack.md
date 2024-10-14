# 基本使用

webpack是一个静态资源打包工具，将代码编译成浏览器能识别的

## 功能介绍





初始化一个包文件package.json

```jsx
npm init -y
```

依赖

```jsx
npm i webpack-cli -D
```

打包

```jsx
npx webpack ./src/main.js --mode=development

npx webpack ./src/main.js --mode=production
```

在dist文件夹中

在html文件中引入

```jsx
<script src="../dist/main.js"></script>
```



## 基本配置介绍

1. entry(入口)

   指示Webpack从哪个文件开始打包

2. output(输出)

   指示Webpack打包完的文件输出到哪里去，如何命名等

3. loader(加载器)

   Webpack本身只能处理js、json等资源，其他资源如css需要借助loader，Webpack才能解析

4. plugins(插件)

   扩展Webpack功能

5. mode

   development(开发模式)：仅能编译JS中的ES Module语法

   production(生产模式)：能编译JS中的ES Module语法 还能压缩JS代码

## 配置文件

创建配置文件`webpack.config.js`

```js
const path = require("path"); //node.js核心模块
module.exports = {
  // 入口
  entry: "./src/main.js",
  // 输出
  output: {
    // 文件输出路径[绝对路径]
    // __dirname node.js变量， 代表当前文件夹目录
    path: path.resolve(__dirname, "dist"),
    // 文件名
    filename: "main.js",
    // 自动清空上次打包结果（在打包前将path目录清空）
    clean: true,
  },
  // 加载器
  module: {
    rules: [
      // loader配置
    ],
  },
  // 插件
  plugins: [
    // plugins的配置
  ],
  //  模式
  mode: "development",
};

```

运行

```cmd
npx webpack
```

# 处理样式资源

## css

1. 创建css文件

2. 在main.js中引入css文件

3. 下载对应`loader`

   ```jsx
   npm install --save-dev style-loader
   npm install --save-dev css-loader
   ```

4. 在webpack.config.js中添加rule

   注意 use[]中用了几个loader包就要去对应的[webpack官网](https://webpack.docschina.org/concepts/)下载几个包

   ```jsx
   rules: [
         {
           test: /\.css$/i, //检测.css文件
           use: ["style-loader", "css-loader"], //从右向左执行
         },
   ```

   > - css-loader 将css资源编译成common.js的模块到js中
   > - style-loader 将js中css通过创建style便签添加到html文件中生效

## less

操作同上 

```jsx
npm install less less-loader --save-dev
```

```js
rules: [
      // loader配置
      {
        test: /\.css$/i, //检测.css文件
        use: ["style-loader", "css-loader", "less-loader"], //从右向左执行
        // css-loader 将css资源编译成common.js的模块到js中
        // style-loader 将js中css通过创建style便签添加到html文件中生效
      },
      {
        test: /\.less$/i,
        use: [
          // compiles Less to CSS
          "style-loader",
          "css-loader",
          "less-loader",
        ],
      },
    ],
```

### 图片资源

```jsx
{
  	test: /\.(png|svg|jpg|jpeg|gif)$/i,
    type: "asset/resource",
},
```

优化：实现小于一定kb的转化成base64，从而减少请求次数[详见[通用资源类型]](https://webpack.docschina.org/guides/asset-modules#inlining-assets)

```jsx
{
  test: /\.(png|jpe?g|webp|svg)/,
    type: "asset",
      parser: {
        dataUrlCondition: {
          // 小于100kb的图片转base64
          // 优点：减少请求数量 缺点：体积会更大
          maxSize: 100 * 1024, // 100kb
        },
      },
},
```

### 其他资源

想处理什么就添加什么

```jsx
{
  test: /\.(ttf|woff2?|mp3|mp4|avi)/, // 检测图片文件
    type: "asset/resource",
      generator: {
        filename: "static/media/[hash][ext][query]",
      },
},
```

# 修改输出路径

main.js

```jsx
module.exports = {

  entry: "./src/main.js",

  output: {
    // 文件输出路径[绝对路径]
    path: path.resolve(__dirname, "dist"), 
    // 入口文件 main.js 输出文件名
    filename: "static/js/main.js",
  },
```

图片

```jsx
      {
        test: /\.(png|jpe?g|webp|svg)/, 
        type: "asset", 
        parser: {
          dataUrlCondition: {
            maxSize: 100 * 1024, 
          },
        },
        generator: {
          // 输出图片的文件名
          // [hash:10] hash只去前10位这样文件名就短了
          filename: "static/images/[hash:10][ext][query]",
        },
      },
```

字体

```jsx
{
  test: /\.(ttf|woff2?)/, // 检测图片文件
    type: "asset/resource",
      generator: {
        filename: "static/media/[hash][ext][query]",
      },
},
```

# js

## [Eslint](https://webpack.docschina.org/plugins/eslint-webpack-plugin/#root)

可组装JavaScript和JSX检查工具

### 在根目录创建`.eslintrc.js`配置文件

> 1. rules 具体规则
>
>    - `"off"` 或 `0` - 关闭规则
>
>    - `"warn"` 或 `1` - 开启规则，使用警告级别的错误：`warn` (不会导致程序退出)
>
>    - `"error"` 或 `2` - 开启规则，使用错误级别的错误：`error` (当被触发的时候，程序会退出)
>
>      ```jsx
>      rules: {
>        semi: "error", // 禁止使用分号
>        'array-callback-return': 'warn', // 强制数组方法的回调函数中有 return 语句，否则警告
>        'default-case': [
>          'warn', // 要求 switch 语句中有 default 分支，否则警告
>          { commentPattern: '^no default$' } // 允许在最后注释 no default, 就不会有警告了
>        ],
>        eqeqeq: [
>          'warn', // 强制使用 === 和 !==，否则警告
>          'smart' // https://eslint.bootcss.com/docs/rules/eqeqeq#smart 除了少数情况下不会有警告
>        ],
>      }
>      ```
>
> 2. extends 继承
>
>    开发中一点点写 rules 规则太费劲了，所以有更好的办法，继承现有的规则。
>
>    现有以下较为有名的规则：
>
>    - [Eslint 官方的规则](https://eslint.bootcss.com/docs/rules/)：`eslint:recommended`
>    - [Vue Cli 官方的规则](https://github.com/vuejs/vue-cli/tree/dev/packages/@vue/cli-plugin-eslint)：`plugin:vue/essential`
>    - [React Cli 官方的规则](https://github.com/facebook/create-react-app/tree/main/packages/eslint-config-react-app)：`react-app`
>
>    ```js
>    // 例如在React项目中，我们可以这样写配置
>    module.exports = {
>      extends: ["react-app"],
>      rules: {
>        // 我们的规则会覆盖掉react-app的规则
>        // 所以想要修改规则直接改就是了
>        eqeqeq: ["warn", "smart"],
>      },
>    };
>    ```
>

```jsx
module.exports = {
  env: {
    node: true, // 启用node中全局变量
    browser: true, // 启用浏览器中全局变量
  },
  //   继承Eslint规则
  extends: ["eslint:recommended"],
  parserOptions: {
    ecmaVersion: 6,
    sourceType: "module",
  },
  rules: {
    "no-var": "error", // 不能使用 var 定义变量
  },
};

```

### 在`webpack.config.js`中添加配置

1. 首先在文件顶部引入插件

   ```jsx
   const ESLintPlugin = require("eslint-webpack-plugin");
   ```

2. 引入该插件后，得到的是一个构造函数，通过 `new`来创建对象。插件配置在webpack 配置对象的 `plugins`节点下，该节点是一个数组，数组每个元素都是一个插件。

```jsx
  // 插件
  plugins: [
    // 插件配置
    new ESLintPlugin({
      // 检测哪些文件
      context: path.resolve(__dirname, "src"),
    }),
  ],  plugins: [
    // 插件配置
    new ESLintPlugin(options),
  ],
```

## bebel

JavaScript 编译器。

主要用于将 ES6 语法编写的代码转换为向后兼容的 JavaScript 语法，以便能够运行在当前和旧版本的浏览器或其他环境中

### 下载babel-loader

```
npm install -D babel-loader @babel/core @babel/preset-env webpack
```

### 配置文件

`babel.config.js`

```jsx
module.exports = {
  // 智能预设
  presets: ["@babel/preset-env"],
};
```

### webpack配置

```jsx
rules: [
        {
        test: /\.m?js$/,
        exclude: /node_modules/, // 排除node_modules中js文件不处理
        use: {
          loader: "babel-loader",
          //options可以写在babel.config.js中方便以后修改配置
          options: {
            presets: ["@babel/preset-env"],
          },
        },
      },
]
```

# html

原先需要再html中手动引入js文件，现在通过插件[HtmlWebpackPlugin](https://webpack.docschina.org/plugins/html-webpack-plugin/#root)实现自动引入

```jsx
<!-- 手动引入的js不需要了，通过js插件自动引入 -->
<!-- <script src="../dist/static/js/main.js"></script> -->
```

安装

```jsx
npm install --save-dev html-webpack-plugin
```

基本用法

```jsx
const HtmlWebpackPlugin = require('html-webpack-plugin');
const path = require('path');

plugins: [    
  new HtmlWebpackPlugin({
      // 模版：以public/index.html文件为模版创建新的html文件
      // 新的html文件特点：1. 结构和原来一致 2. 自动引入打包输出的资源
      template: path.resolve(__dirname, "public/index.html"),
    }),
],
```

# 自动化

使用自动化打包工具[webpack-dev-server](https://webpack.docschina.org/configuration/dev-server/#root)实现每次更新代码无需再次使用npx webpack，保存后即可自动更新

> `webpack-dev-server` 在编译之后**不会写入任何输出文件**，而是将 bundle 文件保留在内存中，然后将它们作为可访问资源部署在 server 中，就像是挂载在 server 根路径上的真实文件一样。

### 安装

```
npm install --save-dev webpack-dev-server
```

### webpack基本配置

```jsx
const path = require('path');


// 开发服务器
  devServer: {
    static: {
      directory: path.join(__dirname, "public"),
    },
    compress: true,
    port: 3000, // 启动服务器端口号
    open: true, //是否自动打开浏览器
  },
```

### 启动服务器

```
npx webpack server
```

### 关闭服务器

ctrl + c
