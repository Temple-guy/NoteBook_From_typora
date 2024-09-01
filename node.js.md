```cmd
node --version

// create your first node app
Cmkdir first-app

cd first-app/

//use vscode to opne it
code .
//执行
node App.js
```

![image-20240825171035563](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20240825171035563.png)

node don't have window or document objects

## Global variables

`__dirname`: This variable stores the path to the current working directory.

`__filename`: This variable stores the path to the current working file.

```jsx
// __dirname Global Variable
console.log(__dirname);

// __filename Global Variable
console.log(__filename);

C:\Desktop\NodeJSTut
C:\Desktop\NodeJSTut\app.js
```

module every node application has at least one file or one module which we called main module

![image-20240825172322665](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20240825172322665.png)

in node every file is a module

Hello.js

```jsx
function sayHello(name){
    console.log(`Hello ${name}`);
}

module.exports = sayHello
```

app.js

```jsx
const sayHello = require('./hello.js');

sayHello('John');
sayHello('Peter');
sayHello('Rohit');
```

这种情况下文件Hello.js 可以成为module 每个module都有一个名为exports的对象 它应该包含你想从这个模块导出的内容 模块可以包含变量、函数、类、对象或可用于完成特定任务或一组任务的任何其他代码。



内置module

```jsx
const path = require("path");
//  built in module
var pathObj = path.parse(__filename);
console.log(pathObj);
```

1. `path.resolve(...)`: 将一个相对路径转换为绝对路径。
2. `path.join(...)`: 将多个路径片段合并为一个完整的路径。
3. `path.dirname(...)`: 获取一个路径的目录部分。
4. `path.extname(...)`: 获取一个路径的文件扩展名。
5. `path.basename(...)`: 获取一个路径的文件名部分。

