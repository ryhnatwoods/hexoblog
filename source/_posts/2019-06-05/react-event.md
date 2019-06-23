---
title: 跟着官方文档自学react_event
date: 2019-06-05 21:45:07
categories:
- web
tags:
- react
---
## 事件处理
> react元素的事件处理和dom元素处理事件有一点语法不同
1. react绑定属性的命名采用驼峰式写法
2. 如果是JSX的语法，你需要传入的是函数而不是字符串
3. 在react中必须显示使用preventDefault函数去阻止默认的行为
4. 为一个元素初始渲染时提供一个监听器
5. 需要谨慎对待回调函数的this指向。通常情况下，如果你没有在方法后面添加 () ，例如 onClick={this.handleClick}，你应该为这个方法绑定 this。如果你没有使用属性初始化器语法，你可以在回调函数中使用箭头函数。

## 向事件处理函数传递参数
> 分别通过 arrow functions 和 Function.prototype.bind 来为事件处理函数传递参数
> 通过 bind 方式向监听函数传参，在类组件中定义的监听函数，事件对象 e 要排在所传递参数的后面

