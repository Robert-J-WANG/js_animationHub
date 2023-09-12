## 普通js中使用tailwind.css + daisyUI

### 1. 安装tailwind.css

#### Tailwind CSS 的使用和 Bootstrap 这类 CSS 框架的使用方式有点区别。仅靠引入一个 CSS 文件并不能正常使用。原因是 Tailwind CSS 在 `class` 属性定义中使用了一些非标准的写法。除此之外，Tailwind 的一些高级特性也不是原始 `class` 属性语法能够支撑的。所以在使用 Tailwind CSS 之前，需要先安装好 Node.js 环境。

#### Step 1：使用 `npm` 命令安装 Tailwind CSS：

```bash
npm install -D tailwindcss
```

#### Step 2：然后初始化一个配置文件:

```bash
npx tailwindcss init
```



#### Step 3：命令执行完后，就会在当前目录下创建一个 *tailwind.config.js* 文件。在这个配置文件中的 `content` 属性下配置好 HTML 模板目录信息:

```javascript
module.exports = {
    content: ["./*.html"],
    theme: {
        extend: {},
    },
    plugins: [],
}
```

##### 之所以要配置 HTML 模板目录，是因为 Tailwind CSS 能根据需要只输出使用了的 class 样式代码，减小最终 CSS 文件的大小。



#### Step 4：创建一个 CSS 文件，命名为 *style.css*，并引入 Tailwind CSS 的样式定义。文件代码如下:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

#### Step 5：接下来创建一个测试用的 HTML 文件，命名为 *index.html*，代码如下：

```html
<!doctype html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link href="public/style.css" rel="stylesheet">
</head>
<body>
    <h1 class="h-screen w-screen table-cell align-middle text-center text-3xl font-bold underline">
        Hello zzxworld!
    </h1>
</body>
</html>
```

#### Step 6：注意 `link` 标签的 `href` 属性，引用的是目前还不存在的 CSS 文件。这个文件需要使用下面的命令来生成：

```bash
npx tailwindcss -i ./style.css -o ./public/style.css --watch
```

##### 后面加了 `--watch` 参数，命令执行后会一直监视当前目录下的 `style.css` 文件，以及 *tailwind.config.js* 文件中配置的模板文件改动。

#### Step 7：在浏览器中访问这个 HTML 文件,测试使用引入成功



### 2. 引入daisyUI

#### 使用daisyUI前，必须已经安装了node和tailwind.css， 因为daisyUI组件就是基于tailwind.css编写的

#### Step 1：安装daisyUI

```bash
npm i -D daisyui@latest
```

##### 

#### Step 2：将daisyUI引入到tailwind.css中。 打开已经创建的tailwind.config.js配置文件，添加daisyU到插件列表中

```json
module.exports = {
  //...
  plugins: [require("daisyui")],
}
```

#### Step 3：重新监视当前目录下的 `style.css` 文件，以及 *tailwind.config.js* 文件中配置的模板文件改动

```bash
npx tailwindcss -i ./style.css -o ./public/style.css --watch
```

#### Step 4：index.html文件中添加button组件，测试是否引入成功

```html
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link href="public/style.css" rel="stylesheet">
</head>
<body>
  <button class="btn btn-info">Info</button>
  <button class="btn btn-success">Success</button>
  <button class="btn btn-warning">Warning</button>
  <button class="btn btn-error">Error</button>
  <h1 class="table-cell w-screen h-screen text-3xl font-bold text-center text-red-700 underline align-middle">
    Hello zzxworld!
  </h1>
</body>
</html>
```

