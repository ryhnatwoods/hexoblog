---
title: 跟着官方文档自学react_state_lifecycle
date: 2019-06-05 20:47:01
categories:
- web
tags:
- react
---
## 将函数转化成类
> 为什么要把函数转化成类？为了让组件拥有局部更新能力
> 类中状态的特点？状态是私有的，完全受控于当前的组件，定义为类的组件有些特性，局部状态就是如此。

## 有一个改写clock组件的例子
> 这个例子很详细，直接上(链接)[https://www.reactjscn.com/docs/state-and-lifecycle.html]

## 正确使用状态
> 这个知识点很关键的。
1. 要用setState方法更新state的状态，构造函数是唯一能够初始化state的地方
2. 当状态更新可能是异步的时候，需要接收的是一个函数而不是对象。函数可以异步调用的。
3. 状态更新合并，它可以分离的更新相应的状态里面的部分。这里的合并是浅合并，也就是说this.setState({comments})完整保留了this.state.posts，但完全替换了this.state.comments。
```
constructor(props) {
    super(props);
    this.state = {
      posts: [],
      comments: []
    };
  }

componentDidMount() {
    fetchPosts().then(response => {
      this.setState({
        posts: response.posts
      });
    });

    fetchComments().then(response => {
      this.setState({
        comments: response.comments
      });
    });
  }
```

## 数据自顶向下流动
> 父组件和子组件都不能知道某个组件是状态还是无状态，并且它也不应该关心某个组件被定义为一个类还是一个函数。
> 状态可以作为属性传递给子组件
> 这通常称之为自顶向下或是单向数据流，任何状态始终有某一个特定组件持有，从该状态导出的任何数据或是UI都只影响树中下方的组件。