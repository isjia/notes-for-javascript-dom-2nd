## 动画基础知识

### 位置
通常通过 CSS 来设置元素在网页上的位置，比如：

```css
element {
  position: absolute;
  top: 50px;
  left: 100px;
}
```

也可以用 DOM 实现同样的效果：

```js
element.style.position = "absolute";
element.style.top = "50px";
element.style.left = "100px";
```

position 属性的合法值有：
- static：默认值，出现在文档流中
- fixed：
- relative：脱离文档流
- absolute：相对于父容器的固定位置

### 时间

语法：`setTimeout("function", interval)`，让指定的函数经过某段时间（interval）之后才开始执行，单位为毫秒。
`variable = setTimeout("function", interval);`
取消等待执行的某个函数：`clearTimeout(variable)`
设置5秒后，移动，期间随时可以使用`clearTimeout(movement)`来取消移动。

```js
function positionMessage(){
  if (!document.getElementById) {return false};
  if (!document.getElementById("message")) {return false};

  var elem = document.getElementById("message");
  elem.style.position = "absolute";
  elem.style.top = "50px";
  elem.style.left = "100px";

  movement = setTimeout("moveMessage()", 5000); //未使用var声明，说明可以在函数以外的地方调用clearTimeout(movement)来取消移动。
}
function moveMessage(){
  if (!document.getElementById) {return false};
  if (!document.getElementById("message")) {return false};

  var elem = document.getElementById("message");
  elem.style.left = "200px";
}
addLoadEvent(positionMessage);
```

### 时间递增量

```js
function moveMessageEnhancement(){
  if (!document.getElementById) {return false};
  if (!document.getElementById("message")) {return false};

  var elem = document.getElementById("message");
  var xpos = parseInt(elem.style.left);
  var ypos = parseInt(elem.style.top);
  if (xpos == 200 && ypos == 50) return true;
  if (xpos < 200) {
    xpos++;
  }
  if (xpos > 200) {
    xpos--;
  }
  if (ypos < 50) {
    ypos++;
  }
  if (ypos > 50) {
    ypos--;
  }
  elem.style.top = ypos+"px";
  elem.style.left = xpos+"px";
  movement = setTimeout("moveMessageEnhancement()", 10);
}
```

### 抽象

```js
function moveMessageCommon(elemID, final_x, final_y, interval){
  if (!document.getElementById) {return false};
  if (!document.getElementById(elemID)) {return false};

  var elem = document.getElementById(elemID);
  var xpos = parseInt(elem.style.left);
  var ypos = parseInt(elem.style.top);
  if (xpos == final_x && ypos == final_y) return true;
  if (xpos < final_x) {
    xpos++;
  }
  if (xpos > final_x) {
    xpos--;
  }
  if (ypos < final_y) {
    ypos++;
  }
  if (ypos > final_y) {
    ypos--;
  }
  elem.style.top = ypos+"px";
  elem.style.left = xpos+"px";
  var repeat = "moveMessageCommon('"+elemID+"',"+final_x+","+final_y+","+interval+")";
  movement = setTimeout(repeat, interval);
}
```

## 实用的动画

### CSS overflow 属性
- visible：不裁剪溢出的内容
- hidden：隐藏溢出的内容
- scroll: 浏览器将溢出内容隐藏，但显示一个滚动条
- auto：浏览器只在确实发生溢出时才显示滚动条

```css
#slideshow {
   width: 100px;
   height: 100px;
   position: relative;
   overflow: hidden;
}
```

### 优化后最终

js与样式完全分离
js与HTML完全分离
增加安全检查

```js
function prepareSlideShow(){
  // 确保浏览器支持 DOM 方法
  if (!document.getElementsByTagName) return false;
  if (!document.getElementById) {return false};
  // 确保元素存在
  if (!document.getElementById("linklist")) {return false};
  // 添加元素
  var slideshow = document.createElement("div");
  slideshow.setAttribute("id", "slideshow");
  var preview = document.createElement("img");
  preview.setAttribute("id", "preview");
  preview.setAttribute("src", "images/topics.gif");
  preview.setAttribute("alt", "building blocks of web design");
  slideshow.appendChild(preview);
  var list = document.getElementById("linklist");
  insertAfter(slideshow, list);
  var links = list.getElementsByTagName("a");
  // 为 link 添加 onmouseover 事件
  links[0].onmouseover = function(){
    moveElement("preview", -100, 0, 10);
  }
  links[1].onmouseover = function(){
    moveElement("preview", -200, 0, 10);
  }
  links[2].onmouseover = function(){
    moveElement("preview", -300, 0, 10);
  }
}
addLoadEvent(prepareSlideShow);
```

## 小结