---
title: 跟着官方文档自学react-元素渲染
date: 2019-06-05 19:59:01
categories:
- web
tags:
- react
---
## 元素渲染
> 在react中，元素被当作react应用的最小单元，小到它可以是一个静态的div对象，大到它可以由许许多多小的组件汇聚而成。
> 一般而言，如果一开始就是使用react开发的页面，那只会有一个react的容器去包裹。但是如果你是在其他项目中部分的引入react的组件，那么就可能会有多个容器存在。
> 从更新元素渲染的角度，react元素在没有设置状态的情况下是不可变的，他就好像是过去某一个时间节点一样，你没法回到过去，不是? 但是确实react留下了把开启时间之门的钥匙，只不过是另一种方式的获取。
```
//在这例子中，定时器每隔1s都会重新渲染整个react元素并添加到浏览器的dom树中。是不是感觉很累，就好像每次写错一个单词，老师都得让你罚抄整篇课文，好不爽。
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(element, document.getElementById('root'));
}

setInterval(tick, 1000);
```
> react dom,一个可以开启时间钥匙之门的神，它会帮我们只更新那些需要更新的内容，为我们节约了成本和时间