---
title: 跟着官方文档自学react-jsx
date: 2019-06-05 18:07:29
categories:
tags:
---
## JSX简介
> 首先强调一下JSX不是HTML，它是一种javascript的语法扩展，这种语法的好处是可以和js无缝对接，你可以赋值给变量，你也可以直接在里面通过{}包裹去执行js表达式。不过文中特别提到为了增加代码的可读性，最好是在JSX代码外面包裹一层()。
> JSX支持标签的嵌套，允许表达式值的属性，属性通过小驼峰命名来定义
> JSX能有效防止xss攻击，因为在渲染前，它会将所有内容转换成字符串。
> JSX代表Object，BABEL转译器会把JSX转换成一个名为React.createElement()的方法调用，最终会返回一个react对象
```
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world'
  }
};
```