# webpack 教程
## 起步
webpack 用于编译 JavaScript 模块。

## 基本安装
首先创建一个目录，初始化 npm，然后在本地安装 webpack，接着安装webpack-cli（此工具用于在命令行中运行 webpack）：
```bash
mkdir webpack-demo && cd webpack-demo
npm init -y
npm install webpack webpack-cli --save-dev
```

现在我们将创建以下目录结构、文件和内容：
**project**
```
  webpack-demo
  |- package.json
+ |- index.html
+ |- /src
+   |- index.js
```
**src/index.js**
```js
function component() {
    var element = document.createElement('div');
    
    // Lodash（目前通过一个 script 脚本引入）对于执行这一行是必需的
    element.innerHTML = _.join(['Hello', 'webpack', ' ']);

    return element;
}

document.body.appendChild(component());
```
**index.html**
```html
<!DOCTYPE html>
<html>

<head>
  <title>起步</title>
  <script src="https://unpkg.com/lodash@4.16.6"></script>
</head>

<body>
  <script src="./src/index.js"></script>
</body>

</html>
```

我们还需要调整 package.json 文件，以便确保我们安装包是私有的（private），并且移除main入口。这可以防止意外发布你的代码。

**package.json**
```json
  {
    "name": "webpack-demo",
    "version": "1.0.0",
    "description": "",
+   "private": true,
-   "main": "index.js",
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1"
    },
    "keywords": [],
    "author": "",
    "license": "ISC",
    "devDependencies": {
      "webpack": "^4.40.2",
      "webpack-cli": "^3.3.9"
    }
  }
```

在此示例中，`<script>` 标签之间存在隐式依赖关系。`index.js` 文件执行之前，还依赖于页面中引入的 `lodash`。之所以说是隐式的是因为 `index.js` 并未显式声明需要引入 `lodash`，只是假定推测已经存在一个全局变量 `_`。

使用这种方式去管理 JavaScript 项目会有一些问题：
* 无法立即提现，脚本的执行依赖于外部扩展库（external library）。
* 如果依赖不存在，或者引入顺序错误，应用程序将无法正常运行。
* 如果依赖被引入但是没有使用，浏览器将被迫下载无用代码。
