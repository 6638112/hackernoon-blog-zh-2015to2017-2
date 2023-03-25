# 掌握 ES6:箭头功能

> 原文：<https://medium.com/hackernoon/getting-to-grips-with-es6-arrow-functions-ebfa62c5c5d6>

![](img/63de466da92fbf101000db58b95892bf.png)

## 第二部分:理解箭头函数

[*点击这里查看第三部分:理解标准的、嵌入式的、多行的和带标签的模板文字。*](/@andrewjrhill/getting-to-grips-with-es6-template-literals-9a42e4389e1e#.5opel5frn)

## **前言**

这篇文章是为希望更好地理解 ES6 arrow 函数的初级到中级开发人员设计的入门读物。

作为我的“掌握 ES6”系列的一部分，我的目标是创建一个参考，其中包含简单明了的解释，以帮助我们理解这些概念，并将它们直接应用到我们当前的开发过程中。

由安德鲁·希尔撰写。
你可以在 [LinkedIn](http://www.linkedin.com/in/andrewjrhill) 、 [Twitter](https://twitter.com/andrewjrhill) 、 [Instagram](https://www.instagram.com/andrewshills/) 、 [GitHub](https://github.com/Sntax/) 上找到我。

# 箭头功能

箭头函数(通常称为胖箭头函数或 lambda 函数)是一种简洁的函数编写方式，它不会在其他函数中重新绑定上下文(`this`)。它们的简短语法由于能够在一行单一返回函数中隐式返回值而得到进一步增强。

箭头函数不能被命名，因此总是被认为是匿名函数。

## **传统功能定义**

到目前为止，JavaScript 已经对匿名函数使用了以下语法:

```
var double = function(a) {
  return a * 2;
}double(100);// Output: 200
```

有各种各样的语法可用于箭头函数；完整的名单可以在 EcmaScript.org 找到。为了简洁起见，本文中的例子将使用最常见的例子。

## **箭头功能定义**

通过引入箭头函数，我们可以将给出的示例重写如下:

```
const double = (a) => {
  return a * 2;
}double(100);// Output: 200
```

## **参数和括号**

带多个参数的箭头函数需要括号:

```
const add = (a, b) => {
  return a + b;
}add(100, 200);// Output: 300
```

在完全不包含任何参数的箭头函数中也需要括号:

```
const fullName = () => {
  return 'Andrew Hill';
}name();// Output: Andrew Hill
```

包含单个[参数](https://hackernoon.com/tagged/parameter)的函数允许我们一起省略[函数](https://hackernoon.com/tagged/function)定义中的括号:

```
const double = a => {
  return a * 2;
}double(100);// Output: 200
```

## **隐式返回**

我们的例子是一个简单的单行函数，它立即返回一个值。在这样的用例中，我们被允许省略函数花括号，以便*隐式返回*它的结果:

```
const double5 = a => a * 2;double5(100);// Output: 200
```

## 隐式返回对象文本

传统上，如果我们想返回一个对象文字，我们应该这样写我们的函数:

```
var animal = function(type, name) {
  return {
    type: type,
    name: name,
  }
}animal('dog', 'Damon');// Output: Object {type: "dog", name: "Damon"}
```

切换到箭头函数并试图隐式返回对象将导致错误，因为引擎无法判断花括号是属于对象还是功能块:

```
const animal = (type, name) => { type: type, name: name };animal('dog', 'Damon');// Output: [SyntaxError] Unexpected token :
```

为了解决这个问题，我们可以告诉 arrow 函数，我们通过将对象放在一组附加的括号中来隐式返回对象:

```
const animal = (type, name) => ({ type: type, name: name });animal('dog', 'Damon');// Output: Object {type: "dog", name: "Damon"}
```

顺便提一下，在 ES6 中共享一个名称的键和值可以用如下简写:

```
const animal2 = (type, name) => ({ type, name });animal2('dog', 'Damon');// Output: Object {type: "dog", name: "Damon"}
```

*好美！*

## 语境

让我们来看看传统函数处理上下文的方式，将事件监听器绑定到按钮，并在单击时记录`this`:

```
var button = document.getElementById('contextButton');button.addEventListener('click', function(){
  console.log(this);
});// Output on click: <button id="contextButton">...</button> 
```

在这个例子中，传统函数将`this`的值绑定到事件监听器被分配到的元素。

请考虑以下使用箭头函数的示例:

```
const button = document.getElementById('contextButton');button.addEventListener('click', () => {
  console.log(this);
});// Output on click: Window { ... }
```

这里我们说明了 arrow 函数如何利用词法绑定从父上下文中继承`this`的值。由于这段代码存在于全局范围内，它的父对象(以及`this`的结果)是`Window {}`对象。

## 细微差别和最终想法

要考虑的最后一个细微差别是`arguments`对象对箭头函数不可用。

在下面的例子中，我们利用一个传统的函数，使用`arguments`对象返回一个“参数值”数组:

```
var test = function(a, b) {
  return arguments;
}test(100, 200);// Output: [100, 200]
```

使用 arrow 函数尝试同样的事情会导致错误:

```
const test = (a, b) => arguments;test(100, 200);// Output: [Uncaught ReferenceError] arguments is not defined
```

最后，重要的是要认识到，即使箭头函数是美丽的、简短的和简洁的，它们也不能代替传统的函数。他们对词法绑定的使用意味着有明确的用例，我们应该和不应该使用箭头函数。

感谢阅读。如果您喜欢这篇文章，请考虑推荐它来支持本系列的未来安装。👏

[*点击这里查看第三部分:理解标准的、嵌入式的、多行的和带标签的模板文字。*](/@andrewjrhill/getting-to-grips-with-es6-template-literals-9a42e4389e1e#.5opel5frn)