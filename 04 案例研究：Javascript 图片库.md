## 标记

编写一个HTML page 如下：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Image Gallery</title>
</head>
<body>
  <h1>Snapshots</h1>
   <ul>
     <li><a href="images/fireworks.jpg" title="A fireworks display">Fireworks</a></li>
     <li><a href="images/coffee.jpg" title="A cup of black coffee">Coffee</a></li>
     <li><a href="images/rose.jpg" title="A red, red rose">Rose</a></li>
     <li><a href="images/bigben.jpg" title="The famous clock">Big Ben</a></li>
   </ul>
   <img src="images/placeholder.gif" alt="my image gallery" id="placeholder">
</body>
</html>

```

## Javascript

### 非 DOM 解决方案
略

### 最终的函数代码清单

showPic.js 如下：

```js
function showPic(whichpic) {
  var source = whichpic.getAttribute("href");
  var placeholder = document.getElementById("placeholder");
  placeholder.setAttribute("src", source);
}
```

## 应用这个 Javascript 函数
在 `gallery.html` 的 `</body>` 标签前增加：

```js
<script src="scripts/showPic.js" type="text/javascript"></script>
```

### 事件处理
- 使用 `this` 关键字代表当前元素节点这个对象
- 添加事件处理函数的语法：`event = "Javascript statement(s)"` ，注意代码包含在一对引号之间，可以把任意数量的Javascript语句放在这对引号之间，各语句之间用分号隔开；例如：`onclick = "showPic(this)";`
- 阻止默认事件发生：添加 `onclick` 事件，并返回 `false`, 这样onclick的默认事件就不会发生，比如：`<a href="images/fireworks.jpg" title="A fireworks display" onclick="return false;">Fireworks</a>`

在 HTML 中添加 `onclick` 事件：

```html
<a href="images/fireworks.jpg" title="A fireworks display" onclick="showPic(this); return false;">Fireworks</a>
```

## 对这个函数进行扩展

实现在显示图片的同时显示不同的文本(text)。

### childNodes 属性
在一棵节点数上，childNodes 属性可以用来获取任何一个元素的所有子元素，他是一个包含这个元素全部子元素的数组：`element.childNodes`，由 childNodes 属性返回的数组包含所有类型的节点，而不仅仅是元素节点，例如：

```js
function countBodyChildren(){
  var body_element = document.getElementsByTagName("body")[0];
  alert (body_element.childNodes.length);
}
```

### nodeType 属性
- 每一个节点都有 nodeType 属性
- 获取节点的 nodeType 属性：`node.noteType`
- nodeType 的值是一个数字，而不是字符串
- nodeType 属性总共有 12 种可取数值，其中仅有 3 种具有使用价值：
  - 元素节点：1
  - 属性节点：2
  - 文本节点：3

### 在 HTML 中增加文本的占位符：

```html
<p id="description">Choose an image.</p>
```

### 用javascript 获取这段text

```js
function showPic(whichpic) {
  var source = whichpic.getAttribute("href");
  var placeholder = document.getElementById("placeholder");
  placeholder.setAttribute("src", source);
  var text = whichpic.getAttribute("title");
  var description = document.getElementById("description");
}
```

### nodeValue 属性
- 用来得到和设置一个节点的值：`node.nodeValue`
- `description.childNodes[0].nodeValue` // 获取 `<p>` 元素中text value

### firstChild 和 lastChild 属性
- node.firstChild 等价于 node.childNodes[0]
- node.lastChild 代表 childNode 数组的最后一个元素，等价于 node.childNodes[node.childNode.length-1]

### 利用 nodeValue 属性刷新描述
更新后的js函数：

```js
function showPic(whichpic) {
  var source = whichpic.getAttribute("href");
  var placeholder = document.getElementById("placeholder");
  placeholder.setAttribute("src", source);
  var text = whichpic.getAttribute("title");
  var description = document.getElementById("description");
  description.firstChild.nodeValue = text;
}
```

### 增加一些样式
styles/layou.css

```css
body {
  font-family: "Helvetica", "Arial", serif;
  color: #333;
  background-color: #ccc;
  margin: 1em 10%;
}
h1 {
  color: #333;
  background-color: transparent;
}
a {
  color: #c60;
  background-color: transparent;
  font-weight: bold;
  text-decoration: none;
}
ul {
  padding: 0;
}
li {
  float: left;
  padding: 1em;
  list-style: none;
}
img {
  display: block;
  clear: both;
}
```

## 小结
- childNodes
- nodeType
- nodeValue
- firstChild
- lastChild