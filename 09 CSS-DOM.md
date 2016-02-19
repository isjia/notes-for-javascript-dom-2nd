# 09 CSS-DOM

## 三位一体的网页

- 结构层 HTML
- 表示层 CSS
- 行为层 Javascript

## Style 属性

### 读取样式
- 语法：`element.style.property`
- style 返回的是一个对象（Object），而不是一个 String
- 返回颜色：`element.style.color`
- 返回font-family：`element.style.fontFamily`，注意不能出现连字符（-），使用驼峰命名法代替。
- style 属性只能返回内嵌样式，不能检索外部样式的属性

### 设置样式
- 语法：`element.style.property = value`
- value 是一个字符串
- 设置值会覆盖原来的属性值

## 何时应该用 DOM 脚本设置样式

### 给紧跟在 h1 元素后面的第一个元素添加属性：
HTML 文档如下：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Man bites dog</title>
</head>
<body>
  <h1>Hold the front page</h1>
  <p>This first paragraph leads you in.</p>
  <p>Now you get the nitty-gritty of the story.</p>
  <p>The most important information is delivered first.</p>
  <h1>Extra! Extra!</h1>
  <h3>Further developments are unfolding.</h3>
  <p>You can read all about it here.</p>

  <script src="scripts/addLoadEvent.js"></script>
  <script src="scripts/styleHeaderSiblings.js"></script>
</body>
</html>
```

函数如下：

```js
function styleHeaderSiblings(){
  if (!document.getElementsByTagName) return false;

  var header = document.getElementsByTagName("h1");
  var elem;
  for (var i = 0; i < header.length; i++) {
    elem = getNextElement(header[i].nextSibling);

    elem.style.fontWeight = "bold";
    elem.style.fontSize = "1.2em";
  }
}
function getNextElement(node){
  if(node.nodeType == 1) return node;
  if (node.nextSibling) {
    return getNextElement(node.nextSibling);
  }
  return null;
}
addLoadEvent(styleHeaderSiblings)
```

### 根据某种条件设置样式
设置表格的隔行背景色
HTML如下：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Cities</title>
  <link rel="stylesheet" href="styles/format.css">
</head>
<body>
  <table>
       <caption>Itinerary</caption>
       <thead>
         <tr>
           <th>When</th>
           <th>Where</th>
         </tr>
       </thead>
       <tbody>
         <tr>
           <td>June 9th</td>
           <td>Portland, <abbr title="Oregon">OR</abbr></td>
         </tr>
         <tr>
           <td>June 10th</td>
           <td>Seattle, <abbr title="Washington">WA</abbr></td>
         </tr>
         <tr>
           <td>June 12th</td>
           <td>Sacramento, <abbr title="California">CA</abbr></td>
         </tr>
       </tbody>
     </table>
</body>
</html>
```

CSS 如下：

```css
body {
  font-family: "Helvetica", "Arial", sans-serif;
  background-color: #fff;
  color: #000;
}
table {
  margin: auto;
  border: 1px solid #699;
}
caption {
  margin: auto;
  padding: .2em;
  font-size: 1.2em;
  font-weight: bold;
}
th {
  font-weight: normal;
  font-style: italic;
  text-align: left;
  border: 1px dotted #699;
  background-color: #9cc;
  color: #000;
}
th, td {
  width: 10em;
  padding: .5em;
}
```

可以通过 CSS3 属性设置隔行背景色：

```css
tr:nth-child(odd){
  background-color: #fcc;
}
tr:nth-child(even){
  background-color: #fff;
}
```

如果浏览器不支持 CSS3 就会有问题，通过 DOM 实现斑马线效果如下：

```js
function stripeTables(){
  if(!document.getElementsByTagName) return false;

  var tables = document.getElementsByTagName("table");
  var odd, rows;
  for (var i = 0; i < tables.length; i ++) {
    odd = false;
    rows = tables[i].getElementsByTagName("tr");
    for (var j = 0; j < rows.length; j++) {
      if (odd == true) {
        rows[j].style.backgroundColor = "#fcc";
        odd = false;
      } else {
        odd = true;
      }
    }
  }
}
addLoadEvent(stripeTables);
```

### 响应事件
当鼠标移到某一行时，改行字体变粗：

```js
function highlightRows(){
  if(!document.getElementsByTagName) return false;
  var rows = document.getElementsByTagName("tr");
  for (var i = 0; i < rows.length; i++){
    rows[i].onmouseover = function(){
      this.style.fontWeight = "bold";
    }
    rows[i].onmouseout = function(){
      this.style.fontWeight = "normal";
    }
  }
}
addLoadEvent(highlightRows)
```

如果想改变某个元素的呈现效果，使用 CSS；
如果想改变某个元素的行为，使用 DOM；
如果想根据某个元素的行为去改变他的呈现样式，请运用你的智慧，这里问题没有标准答案。

## className 属性
使用 DOM 去更新某个元素的 class 属性：`element.className = value`

```css
.intro {
  font-weight: bold;
  font-size: 1.4em;
}
```

js 修改：

```js
function styleHeaderSiblings(){
  if (!document.getElementsByTagName) return false;
  var header = document.getElementsByTagName("h1");
  var elem;
  for (var i = 0; i < header.length; i++) {
    elem = getNextElement(header[i].nextSibling);
    elem.className = "intro";
  }
}
```

增加 className：

```js
function addClassName(element, value){
  if (!element.className){
    element.className = value;
  } else {
    newClassName = element.className;
    newClassName+= " ";
    newClassName+= value;
    element.className = newClassName;
  }
}
```

### 对函数进行抽象
把一个非常具体的东西改进为一个较为通用的东西的过程叫做**抽象**（abstraction）。
> 好习惯：不论何时，发现可以对某个函数进行抽象，都应该马上去做，这总是一个好主意。

## 小结
