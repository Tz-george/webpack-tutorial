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