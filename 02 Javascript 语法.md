# 02 Javascript 语法

## 准备工作
- 方法1：将 Javascript 代码放到文档`<head>`标签中`<script>`的标签之间
- 方法2：将 Javascript 代码存为一个扩展名为`.js`的独立文件，并把`<script>`的`src属性`指向该文件。
- 把`<script>`标签放到HTML文档的最后，`</body>`标签之前，这样能使浏览器更快地加载页面。

## 语法

### 语句 Statement
- 如果把多条语句放在同一行，必须用**分号 ；**来分隔他们。`first statement; second statement;`
- 建议在每一条语句的末尾都加上分号，这是一种良好的编程习惯。

> 好习惯：在每条语句的末尾都加上分号

### 注释 Comment
- 单行注释：`// 自我提醒：有注释是好事`
- 多行注释：

```
/* 自我提醒：
   有注释是好事 */
```

- 也可以使用HTML风格的注释：`<!-- 这是HTML中的注释`, 这种用法等同于同单行注释，建议不要使用

### 变量 Variable

> 好习惯：提前声明变量是一种良好的编程习惯

- 变量声明 declare：`var mood;` ，也可以一条语句声明多个变量： `var mood, age;`
- 声明和负值一次完成：`var mood = "happy";`
- 一次声明并负值多个变量：`var mood = "happy", age = 33;`
- 变量和其他语法元素是 **区分大小写** 的
- 变量名中不允许包含空格或者标点符号（$除外）
- 变量名允许包含：字母、数字、$、下划线，但第一个字符不允许是数字
- 首选驼峰格式（camel case）：myMood

### 数据类型

- Javasript不需要进行类型声明，他是一种弱类型（weakly typed）语言，可以在任何阶段改变变量的数据类型
- 字符串：字符串必须包含在引号里，单引号或双引号都可以。转义字符（escaping），`\n`

> 好习惯：不管选择双引号还是单引号，请在整个脚本中保持一致

- 数值：不用限定他必须是一个整数，可以是浮点数、负数、负数浮点数
- 布尔值：true、false

### 数组 Array
- 数组 Array：变量的集合：
  - `var beatles = Array()`
  - `var beatles = Array(4)`
  - `var beatles = Array("John", "Paul", "George", "Ringo");`
  - `var beatles = [ "John", "Paul", "George", "Ringo" ]`
  - 添加元素（填充populating）：`array[index] = element;`
  - 可以把不同数据类型混在一起存入一个数组中
  - 数组中的元素element也可以是一个数组
- 关联数组：下标不是数字，`lenno["name"] = "John"`，不推荐使用

### 对象 Object
- 对象的每一个值都是对象的属性；
- 创建对方及访问属性：

```js
var lenno = Object();
lenno.name = "John";
lenno.year = 1940;
lenno.living = false;
```

- 简易方法：`var lennon = { name:"John", year:1940, living:false };`

## 操作
### 算数操作符
- +、-、*、/、++、--
- `var total = (1+4)*5;`
- 拼接（concatenation): 把数字和字符串拼接在一起，其结果将是一个更长的字符串；
- `+=`

### 比较操作符
- < 、> 、>= 、<= 、== 、=== (不仅比较值，还比较变量类型）、!= 、!==

### 逻辑操作符
- && 、|| 、！

## 条件语句 Condition Statment
- if 条件语句的语法

```js
if (condition) {
  statements;
} else {
  statements;
}
```

- if 语句中的花括号本身并不是必不可少的，如果if 语句中花括号部分只包含着一条语句的话，可以不适用花括号：`if (1 > 2) alert("The world has gone mad!");`

> 好习惯：在if语句中总是使用花括号是个好习惯

## 循环语句

### while 循环

```javascript
while (condition) {
  statements;
}
```

- do...while

```
do {
  statements;
} while (condition);
```

- for

```
for (initial condition; test condition; alter condition) {
  statements;
}
```

### 函数

```
function name(arguments) {
  statements;
}
```
- 变量的作用域
  - 全局变量：作用域为整个脚本
  - 局部变量：作用于声明他的那个函数内部
  
### 对象
- 包含属性和方法：`var jenny = new Person;`
- 内建对象：Math(), Array(), Date()
- 宿主对象：Form, Image, Element, document

## 小结
## ToDo List
- [ ] 找到作者[第一版的附录](http://www.ituring.com.cn/book/42)