# 不要遗忘的事

## 样式恢复

每次样式修改后，要看看是否需要`恢复到初始状态`，添加的样式类名必要的话是要移除的

```js
innerHTML = ""
from.reset()
```

## 封装函数

对于重复的框架结构不同的内容显示，要想到`封装函数`

# 方便的运算符

逻辑断 `&&` 

逻辑与 `||`

`三元运算符` 

可选链操作符`?.`



# 对象上常用的操作

`动态获取`对象属性值 obj[k] k为属性名

# 渲染

## 法一

> 对原始数组渲染为HTML页面 而不是直接对HTML标签渲染
>
> 说白了就是你拿到一组匹配的数据，这是一组数组，你要将它展示到页面上对吧，那你就需要利用map先将其修改为一个个的html语句，然后再用join拼接成字符串 ，最后赋值给对应的的盒子元素。

```js
function render() {
  const str = 对象数组列表.map((item, index) => {
	return `html样式`;
}).join("");
document.quserlector("元素名").innerHTML = str;
}
render();
```

1. 当点击多个列表中的一列，利用`事件委托`给tbody

   ```js
   document.queryselector(".list").addEventLister("click", (e) => {
   	//e.target.tagname 就是当前点击标签
   })
   ```

2. 当所有数据对象的`类名`和`标签名`一致时，用`Object.keys()`获取全部属性(返回值为数组), 再用 `forEach`进行遍历

   ```js
   const ObjAllAttribute = Objects.keys(对象数组)
   // forEach 中的 k 为 属性名
   ObjAllAttribut.forEach(k =>{
     document.quserySelector(`${k}`).value = 对象数组[k]
   })
   ```

## 法二

**遍历数据对象的属性 映射到页面元素上**

```js
const dataObj = {
  channel_id: result.data.channel_id,
  title: result.data.title,
  rounded: result.data.cover.images[0],
  content: result.data.content,
  id: result.data.id,
};      

Object.keys(dataObj).forEach((key) => {
  // 这里的key就是 属性名 dataObj[key]是属性值
  // 如果是图片
  if (key === "rounded") {
    document.querySelector(".rounded").src = dataObj[key];
    document.querySelector(".rounded").classList.add("show");
    document.querySelector(".place").classList.add("hide");
  } else if (key === "content") {
    // 如果是富文本编辑器
    editor.setHtml(dataObj[key]);
  } else {
    // 属性选择器 用[]⭐⭐⭐⭐⭐
    document.querySelector(`[name = ${key}]`).value = dataObj[key];
  }
});
```

# 输出错误

```js
console.dir()
```

# 如何判断点击的按钮

利用classList.contains()

# 自定义属性

使用：在外部调用函数内部的对象的属性值时 可以设置自定义属性等于该属性值

> data-id = `${}`

```js
{
const str = result.data
      .map((element) => {
        return `
      <li class="city-item" data-code = ${element.code}>${element.name}</li>
      `;
      })
      .join("");
}

{
  const cityCode = e.target.dataset.code;
}
```


12. 当你想要获取标签的内容 模板如下

    首先获取该标签

    document.querySelector("")

    然后获取标签名后面的属性名 .属性名

    以获取img标签的src属性为例

    ```html
    <img src = "xxx">
    
    <script>
    	coonst imgURL = document.querySelector("img").src
    </script>
    ```

13. 重置表单 可以用reset() form.reset()

14. 在 JavaScript 中,有几种常见的取整方式:
    1. **Math.ceil(number)** - 向上取整
       - 这个方法会将给定的数字向上取整为最接近的整数。
       - 比如 `Math.ceil(3.14)` 会返回 `4`。
    2. **Math.floor(number)** - 向下取整
       - 这个方法会将给定的数字向下取整为最接近的整数。
       - 比如 `Math.floor(3.14)` 会返回 `3`。
    3. **Math.round(number)** - 四舍五入
       - 这个方法会将给定的数字四舍五入为最接近的整数。
       - 比如 `Math.round(3.14)` 会返回 `3`。
    4. **parseInt(string, radix)** - 字符串转整数
       - 这个方法会将给定的字符串解析为整数。
       - 可以指定转换时使用的基数,比如 2 进制、10 进制等。
       - 比如 `parseInt('3.14', 10)` 会返回 `3`。
    5. **Math.trunc(number)** - 截断小数部分
       - 这个方法会将给定的数字的小数部分截断,只保留整数部分。
       - 比如 `Math.trunc(3.14)` 会返回 `3`。

15. 对于html标签内容的修改 什么时候用innerHTML 什么时候用value

    如果您需要修改 `<div>`、`<p>`、`<h1>`等块级元素的内容,通常使用 `innerHTML` 是最合适的。

    对于 `<input>`、`<textarea>`、`<select>` 等表单元素,使用 `value` 属性来设置或获取它们的值是更合适的。

16. 对于二级分类需要再次遍历的可再次嵌套

    

# 事件：click 还是 change 

对于什么时候使用change事件什么时候使用click事件？

用户更改 <input>、<select> 和 <textarea> img上传 元素的值时，change 事件在这些元素上触发。和 input 事件不同的是，并不是每次元素的 value 改变时都会触发 change 事件。

> 在你点击有下拉菜单的select框时 你需要先点击一遍select框再点击option标签。
>
> 这里进行了两次click 固然用click是不可取的 所以对于这种就应该使用change 当value值改变时才监测到该事件

# 测试方便小Tip

可以提前给表单中的账号和密码标签设置value属性 这样每次运行测试就不用额外输入了

# 页面跳转

```js
location.href("url")
```

# 插件合集

## form-serialize插件

快速收`集表当元素的值`，转变为一个`对象`

> ==**易错**==只能收集到表单元素的信息，如： <input> <select> <option> <button> <textarea> 等, 像 <img>这种标签元素的信息就会自动略过，无法收集
>
> ==Tips==:这种时候可以自己额外添加属性
>
> ```js
> // 前提: data 使我们利用serialize收集到的信息对象
> // 通过自己添加属性来完善缺失的img标签的信息
> data.img = "..." 
> ```

**使用前提**：

1. 引入代码


```html
<script src="form-serialize.js"></script>
```

2. 表单元素需要设置`name属性` name: username 

```js
// 1. 获取表单元素
const form = document.queryselector(".example-form")
// 2. serialize(获取到的表单元素, {hash: true, empty: true}) hash 和 empty 一般都为true
const formInfo = serialize(form, {hash:ture, empty: true})
```

## [富文本编辑器](https://www.wangeditor.com/v5/getting-started.html)

可以使用textarea快速收集富文本内容

```js
// 富文本编辑器
// 创建编辑器函数，创建工具栏函数
// 解构赋值
const { createEditor, createToolbar } = window.wangEditor;

// 编辑器的配置对象
const editorConfig = {
  placeholder: "发布文章内容", // 占位提示文字
  // 编辑器内容 选取变化时的回调函数
  onChange(editor) {
    const html = editor.getHtml();
    console.log("editor content", html);
    // 也可以同步到 <textarea>
    // 🔴为了后续快速收集整个表单内容做铺垫
    document.querySelector(".publish-content").value = html;
  },
};

const editor = createEditor({
  // 创建位置
  selector: "#editor-container",
  html: "<p><br></p>",
  // 配置项
  config: editorConfig,
  //   配置集成的模式
  mode: "default", // or 'simple'
});
// 工具栏配置项 可自行添加或删除工具栏的内容
const toolbarConfig = {};

// 为指定编辑器创建工具栏
const toolbar = createToolbar({
  editor,
  selector: "#toolbar-container",
  config: toolbarConfig,
  mode: "default", // or 'simple'
});

```

### 重置富文本编辑器

```js
editor.setHtml("");
```

## [Bootstrap](https://getbootstrap.com/)

## [lodash](https://lodash.com/)

```javascript
import _ from "lodash"
```

## [classnames优化类名](https://www.npmjs.com/package/classnames)控制

```jsx
import classNames from "classnames";
//原先
 className={`nac-item ${type === item.type && "ative"}`)}></span>
//插件优化
<span className={classNames("nav-item", {active: type === item.type,})}></span>
```



# 具体功能模块

## 登录

```js
/**
 * 目标1：验证码登录
 * 1.1 在 utils/request.js 配置 axios 请求基地址
 * 1.2 收集手机号和验证码数据
 * 1.3 基于 axios 调用验证码登录接口
 * 1.4 使用 Bootstrap 的 Alert 警告框反馈结果给用户
 */

// 1.2 收集手机号和验证码数据
document.querySelector(".btn").addEventListener("click", async () => {
  const form = document.querySelector(".login-form");
  const data = serialize(form, { hash: true, empty: true });
  try {
    const result = await axios({
      url: "/v1_0/authorizations",
      method: "POST",
      data,
    });
    myAlert(true, "登录成功");
    console.log(result);

    // 登录成功后，保存 token 令牌字符串到本地，并跳转到内容列表页面
    localStorage.setItem("token", result.data.token);
    setTimeout(() => {
      location.href = "../content/index.html";
      //   延时跳转 让alert警告框停留一会儿
    }, 1500);
  } catch (error) {
    myAlert(false, error.response.data.message);
    console.dir(error.response.data.message);
  }
});
```

## 验证

1.  判断无 token 令牌字符串，则强制跳转到登录页

```js
//auth.js
const token = localStorage.getItem("token");
if (!token) {
  location.href = "../login/index.html";
}
```

2. ajax 请求拦截器判断token

```js
// request.js
axios.interceptors.request.use(function (config) {
  // 在发送请求之前做些什么
  // 同意携带 token 令牌字符串在请求头上
  const token = localStorage.getItem("token");
  token && (config.headers.Authorization = `Bearer ${token}`);
  return config;
});
```

3. 登录成功后请求个人信息渲染到页面

```js
axios({
  url: "/v1_0/user/profile",
}).then((result) => {
  // console.log(result);
  //🔴此时的result是在request.js中响应拦截器配置好的const result = response.data;
  const username = result.data.name;
  document.querySelector(".nick-name").innerHTML = username;
});
```

## 退出登录



```js
//1. 绑定点击事件
//2. 清空本地缓存，跳转到登录页面
document.querySelector(".quit").addEventListener("click", () => {
  localStorage.clear();
  location.href = "../login/index.html";
});
```

## [提示框函数](https://getbootstrap.com/docs/5.3/components/alerts/#javascript-behavior)

使用了bootstrap插件

```js
// 弹窗插件
// 使用该插件需要 成功时添加类名：alert-success 失败时添加类名：alert-danger
// 需要先准备 alert 样式相关的 DOM
/**
 * BS 的 Alert 警告框函数，2秒后自动消失
 * @param {*} isSuccess 成功 true，失败 false
 * @param {*} msg 提示消息
 */
function myAlert(isSuccess, msg) {
  const myAlert = document.querySelector(".alert");
  myAlert.classList.add(isSuccess ? "alert-success" : "alert-danger");
  myAlert.innerHTML = msg;
  myAlert.classList.add("show");

  setTimeout(() => {
    myAlert.classList.remove(isSuccess ? "alert-success" : "alert-danger");
    myAlert.innerHTML = "";
    myAlert.classList.remove("show");
  }, 2000);
}
```

## 重新上传图片(模拟点击)

> 不需要写在之前上传图片代码的内部 因为之后再次点开页面 图片已经存在 这个时候就是直接的想换图片 就是一个直接的事件

img 绑定点击事件后模拟点击了.img-file input标签 即可

```jS
document.querySelector(".rounded").addEventListener("click", () => {
  document.querySelector(".img-file").click();
});
```

## 发布表单数据到服务器

1. 基于 form-serialize 插件收集表单数据对象

   针对非表单元素信息无法通过插件收集，如按钮和按钮，这个时候就要手动添加属性到对象上

2. 基于 axios 提交到服务器保存

3. 调用 Alert 警告框反馈结果给用户

4. 重置表单并跳转到列表页

   使用form.reset()清空表单

```js
document.querySelector(".btn").addEventListener("click", async (e) => {
  if (e.target.innerHTML !== "发布") return;
  const form = document.querySelector(".art-form");
  const data = serialize(form, { hash: true, empty: true });
  // console.log(data);
  // 发布文章的时候不需要id属性 可以删除id属性 id属性是为了后边编辑文章使用
  delete data.id;
  // 自己添加cover的信息
  data.cover = {
    type: 1, //封面类型
    images: [document.querySelector(".rounded").src],
  };
  try {
    const result = await axios({
      url: "/v1_0/mp/articles",
      method: "POST",
      data,
    });
    // 调用之前封装的elert函数
    myAlert(true, "发布成功");
    // 清空表单并跳转
    form.reset();
    // 封面需要手动重置
    const imgUrl = result.data.url;
    document.querySelector(".rounded").src = "";
    document.querySelector(".rounded").classList.remove("show");
    document.querySelector(".place").classList.remove("hide");
    // 富文本编辑器重置
    editor.setHtml("");
    setTimeout(() => {
      location.href = "../content/index.html";
    }, 1500);
  } catch (error) {
    myAlert(false, error.response.data.message);
  }
});
```

## 回显文章

1. 页面跳转传参（URL 查询参数方式）

   ```js
   if (e.target.classList.contains("edit")) {
       const editId = e.target.parentNode.dataset.id;
       console.log(editId);
   
       //🔴 跳转到指定id的回写页面
       location.href = `../publish/index.html?id=${editId}`;
     }
   ```

   ```js
   //接收参数并转换成对象  
   const paramsStr = location.search;
   const paramsObj = new URLSearchParams(paramsStr);
   ```

2. 发布文章页面接收参数判断（共用同一套表单）

   ```js
   // 在发布文章时是地址对象没有id参数的 这种条件就可以通过if被屏蔽
   if (key === "id")
   ```

3. 修改标题和按钮文字

4. 获取文章详情数据并回显表单

   传输指定文章id到服务器，接收后自定义一个新的适配回显的对象

   ```js
         // 获取文章详情
         const result = await axios({
           url: `/v1_0/mp/articles/${value}`,
         });
         console.log(result);
         // 组织我仅仅需要的数据对象 为后续遍历返回到页面上铺垫
         const dataObj = {
           channel_id: result.data.channel_id,
           title: result.data.title,
           rounded: result.data.cover.images[0],
           content: result.data.content,
           id: result.data.id,
         };
   			//遍历数据对象的属性 映射到页面元素上
   			      Object.keys(dataObj).forEach((key) => {
           // 这里的key就是 属性名 dataObj[key]是属性值
           // 如果是图片
           if (key === "rounded") {
             document.querySelector(".rounded").src = dataObj[key];
             document.querySelector(".rounded").classList.add("show");
             document.querySelector(".place").classList.add("hide");
           } else if (key === "content") {
             // 如果是富文本编辑器
             editor.setHtml(dataObj[key]);
           } else {
             // 属性选择器 用[]⭐⭐⭐⭐⭐
             document.querySelector(`[name = ${key}]`).value = dataObj[key];
           }
         });
   ```

## 分页功能

1. 保存并设置文章总条数

2. 点击下一页，做临界值判断，并切换页码参数并请求最新数据

3. 点击上一页，做临界值判断，并切换页码参数并请求最新数据

```js
let totalCount = 0; //文章总条数
// 点击下一页，做临界值判断，并切换页码参数并请求最新数据
document.querySelector(".next").addEventListener("click", () => {
  // 当前页码小于最大页码数
  if (queryObj.page < Math.ceil(totalCount / queryObj.per_page)) {
    queryObj.page++;
    setArtTitleList(); //渲染列表函数
    document.querySelector(".page-now").innerHTML = `第${queryObj.page}页`;
  }
});
// 点击上一页，做临界值判断，并切换页码参数并请求最新数据
document.querySelector(".last").addEventListener("click", () => {
  if (queryObj.page > 1) {
    queryObj.page--;
    setArtTitleList();//渲染列表函数
    document.querySelector(".page-now").innerHTML = `第${queryObj.page}页`;
  }
});
```

## 删除功能

> 1. 如何做到程序能判断点击图标就是删除图标呢？
>
>    <img src="imgFiles\image-20240808170454623.png" alt="image-20240808170454623.png" style="zoom:33%;"> alt="image-20240808170454623" style="zoom:25%;" />
>
>    利用类名判断是否包含del类名
>
>    ```js
>    if (e.target.classList.contains("del"){}
>    ```
>
> 2. 对于多条数据，如何做到点击对删除图标，则该对于数据删除
>
>    <img src="imgFiles\image-20240808170709841.png" alt="image-20240808170709841.png" style="zoom:33%;"> alt="image-20240808170709841" style="zoom: 25%;" />
>
>    每一个数据对象都有一个属性 `id`,则在对应的html中的<tr>标签添加自定义属性 `data-id`
>
>    ```html
>    <td data-id = "${item.id}">
>      <i class="bi bi-pencil-square edit"></i>            
>      <i class="bi bi-trash3 del"></i>
>    </td>
>    ```
>
>    当前点击的是删除图标，所以e.target 就是类名为del `<td>`, 它父节点就是`<tr>`
>
>    ```js
>    const delId = e.target.parentNode.dataset.id;
>    ```
>
> 3. 当该页面只剩一条数据时，需要满足点击则向前反转一面 且总页数减一

```js
/**
 * 目标4：删除功能
 *  4.1 关联文章 id 到删除图标🔴
 *         <td data-id = "${item.id}">
 *             <i class="bi bi-pencil-square edit"></i>
 *             <i class="bi bi-trash3 del"></i>
 *         </td>
 *  4.2 点击删除时，获取文章 id
 *      🔴利用事件委托 绑定在原本就存在的tbody 上 而不是后来渲染的tr上
 *      🔴artucleId = e.target.parentNode.dataset.id 父节点上的id号
 *  4.3 调用删除接口，传递文章 id 到服务器
 *  4.4 重新获取文章列表，并覆盖展示
 *  4.5 删除最后一页的最后一条，需要自动向前翻页
 */
document.querySelector(".art-list").addEventListener("click", async (e) => {
  if (e.target.classList.contains("del")) {
    // console.log(e.target.parentNode.dataset.id);
    const delId = e.target.parentNode.dataset.id;
    await axios({
      url: `/v1_0/mp/articles/${delId}`,
      method: "DELETE",
    });
    // 4.5 删除最后一页的最后一条，需要自动向前翻页
    // 🔴判断当前tr标签中有几个子节点 如果只有一个子节点就自动翻页
    const childern = document.querySelector(".art-list").children;
    if (childern.length === 1 && queryObj.page !== 1) {
      queryObj.page--;
      document.querySelector(".page-now").innerHTML = `第${queryObj.page}页`;
    }
    setArtTitleList();
  }
  if (e.target.classList.contains("edit")) {
    const editId = e.target.parentNode.dataset.id;
    console.log(editId);

    // 跨页面跳转传参⭐⭐⭐⭐
    //🔴 跳转到指定id的回写页面
    location.href = `../publish/index.html?id=${editId}`;
  }
});
```

## 计算总价

利用reduce函数计算书本的总价

```javascript
const TotalPayments = books.reduce((prceive, current) => {
  return prceive + current.count * current.price
}, 0);
```
