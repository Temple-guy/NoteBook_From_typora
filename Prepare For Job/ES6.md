# [require和import](https://www.cnblogs.com/goloving/p/15110728.html)

　在 es6 之前 JS 一直没有自己的模块语法，为了解决这种尴尬就有了require.js等AMD或CMD方式的出现。在 es6 发布之后 JS 引入了 import 的概念

## require的基本语法

核心概念：在导出的文件中定义 module.export，导出的对象的类型不予限定（可以是任何类型，字符串，变量，对象，方法），在引入的文件中调用 require() 方法引入对象即可。

```jsx
//a.js中
module.export = {
    a: function(){
     console.log(666)
  }
}

//b.js中
var obj = require('../a.js')
obj.a()  //666
```

## import的基本语法	

核心概念：导出的对象必须与模块中的值一一对应，换一种说法就是**导出的对象与整个模块进行解构赋值**。抓住重点，解构赋值！

```jsx
//a.js中
// 最常使用的方法，加入default关键字代表在import时可以使用任意变量名且不需要花括号{}
export default {
     a: function(){
         console.log(666)
   }
}
export function(){  //导出函数
}
export {newA as a ,b,c}  //  解构赋值语法(as关键字在这里表示将newA作为a的数据接口暴露给外部，外部不能直接访问a)
 
//b.js中
import  a  from  '...'  //import常用语法（需要export中带有default关键字）可以任意指定import的名称

import {...} from '...'  // 基本方式，导入的对象需要与export对象进行解构赋值。
 
import a as biu from '...'  //使用as关键字，表示将a代表biu引入（当变量名称有冲突时可以使用这种方式解决冲突）

import {a as biubiubiu,b,c}  //as关键字的其他使用方法
```

# 变量声明的现代化

将 `var` 修改为 `let` 或 `const` 的过程，我们通常称之为 **变量声明的现代化** 或 **ES6 声明规范的改进**。这是从旧的 JavaScript 规范（ES5）向现代 ES6+ 规范过渡的重要一步。
