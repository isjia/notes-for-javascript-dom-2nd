## 文档：DOM中的“D”

D = document

## 对象：DOM中的“O”

Javascript语言里可以分为三种类型的对象：
- 用户定义对象（user-defined object）：由程序员自行创建的对象。
- 内建对象（native object）：内建在Javascript语言里的对象，如Array，Math，Date等
- 宿主对象（host object）：由浏览器提供的对象，通常称为BOM（浏览器对象模型）

本书主要关注浏览器窗口内的网页内容，document对象主要处理网页内容。

## 模型：DOM中的“M”

M = Module 模型

DOM把一份文档表示为一棵树（类似家谱树），这是我们理解和御用这一模型的关键。

## 节点：Node

文档是由节点构成的集合。

### 元素节点（element node）
- 标签的名字就是元素的名字：`<p>`, `<body>`, `<ul>`
- 元素可以包含其他元素。

### 文本节点（text node）
- `<p>`元素中包含着的文本就是一个文本节点
- 文本节点总是被包含在元素节点内部。
- 但并非所有的元素节点都包含文本节点。

### 属性节点（attribue node）
- 属性节点用来对元素做出更具体的描述，例如几乎所有的元素都有一个`"title"`属性，我们可以利用这个属性对包含在蒜素里的东西做出准确的描述
- 属性元素总是被放在起始标签里

### CSS
- class
- id
- 继承

### 获取元素
有3种DOM方法可以获取元素节点：
- `document.getElementById(id)`：通过id属性获得元素
- `document.getElementsByTagName(tag)`：通过标签名称获取元素，返回一个对象数组，每个对象分别对应着文档里有着给定标签的一个元素，可以使用 `“*”` 作为通配符参数传入。
- 可以将 `getElementByTagName` 与 `getElementByID` 结合起来使用，例如：

```js
var shopping = document.getElementById("purchases");
var items = document.getElementsByTagName("*"); // items 数组将只包含id属性值是purchase的无序清单里的元素。
```

- `getElementsByClassName(class)`，返回具有相同类型的元素的数组。类名的顺序不重要，还带有更多类名也没关系。

### 盘点知识点
- 文档中每一个元素节点都是一个对象

## 获取属性和设置属性

### getAttribute
- `object.getAttribute(attribute)`，`getAttribute(attribute)`方法不属于document，只能通过元素节点对象调用。

### setAttribute
- `object.setAttribute(attribute, value)`

## 小结
- DOM的5个方法