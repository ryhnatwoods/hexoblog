---
title: 跟着官方文档自学react-component-props
date: 2019-06-05 20:19:25
categories:
- web
tags:
- react
---
## 组件&props
> 组件可以将UI切割成独立可复用的部件。组件即函数，它接收任意的输入值，并返回需要展示的react元素
```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```
{% note warning %}
组件名必须大写，个人认为组件其实就是对象，对象名称一般都以大写开头，所以这里是要大写开头哦。
{% endnote%}

## 组合组件
> 就是多个子组件拼凑自由组合在一起。
{% note warning %}
组件返回值只有一个根元素
{% endnote%}

## 提取组件
> 对于大型应用，多场景的情况，越小的组件也代表越大的灵活性，这允许我们像乐高玩具那样拼搭成我们喜欢的样子。
> 而且这些小的组件还可以反复的利用。

## Props的只读性
> 所有的react都必须像纯函数那样使用它们的props, 也就是你无论输入多少次一模一样的参数，它返回的结果应该都是一样的。是不是感觉有点幂等性的意思