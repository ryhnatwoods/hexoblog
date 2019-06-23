---
title: 跟着官方文档自学react
date: 2019-06-05 16:00:50
categories:
- web前端
tags:
- react
---
## 跟着react官方文档自学_01
{% cq %} On nous apprend à vivre quand la vie est passée. - Michel De Montaigne  {% endcq %}

{% note summary %} 当舒适的生活远离我们而去的时候，我们真的需要重新审视下自己，学习去适应新的生活。{% endnote %}

## 点击进入[react中文网首页](https://www.reactjscn.com/)
React支持IE9和IE9+，和其他版本的浏览器。只不过需要polyfills
> 三个关键字很亮眼。
1. 声明式：按照我的理解是我看到这个标签就知道这个标签作用在页面上的结果，很直观和简洁。不是很明白来自官网的解释“可以让你的代码更加可靠，且方便调试。”
2. 组件化：创建好用有各自状态的组件，页面由一个一个组建搭配而成，感觉和乐高有点类似，很喜欢这种风格。
3. 一次学习，随处编写：无论你现在正在用什么技术栈，你都可以随时引入react开发新特性。这个解释说实在我现在还有点懵

> 首页分享了分享了4个实例，感觉还不错。
1. 组件：react组件使用render()函数构造组建显示的内容，输入的数据通过this.props传入render函数。
```
//这里首先构造一个HelloMessage的component对象，他接收name的属性对应的数据去返回一个react元素
class HelloMessage extends React.Component {
  render() {
    return (
      <div>
        Hello {this.props.name}
      </div>
    );
  }
}
//ReactDOM作为一个最外层的接口，将helloMessage元素渲染好添加到指定dom的容器中，并返回这个组件的引用。
//其实它还有个可选的参数callback，可以在渲染更新后执行，具体可以看[render](https://www.reactjscn.com/docs/react-dom.html#render)
ReactDOM.render(
  <HelloMessage name="Taylor" />,
  mountNode
);
```

## 有状态的组建
> 除了使用外部传入的数据以外，组件还可以拥有其内部使用的状态数据，这个是通过this.state访问状态数据的，当组件状态发生改变时，会调用render方法重新渲染。
```
//这个看名字是个计时器组件，在构造它时有个初始化的状态对象，0秒。它有一个读秒的方法，这个方法每调用一次会改变组件当前的状态，也就是+1秒。
//这里你会发现组件中出现了两个生命周期的钩子函数，具体生命周期，可以看下[掘金这篇](https://juejin.im/post/5a062fb551882535cd4a4ce3).我先了解这个例子里的两个。
//componentDidMount：组件已经渲染到页面后触发，此时页面中有了真正的DOM元素，可以进行DOM相关的操作
//componentWillUnmount：组件销毁时被处罚，这里我们可以做一些清理的工作
class Timer extends React.Component {
  constructor(props) {
    super(props);
    this.state = { seconds: 0 };
  }

  tick() {
    this.setState(prevState => ({
      seconds: prevState.seconds + 1
    }));
  }

  componentDidMount() {
    //这里设置了一个定时器，每隔1是自动调用tick函数更新组件状态
    this.interval = setInterval(() => this.tick(), 1000);
  }

  componentWillUnmount() {
    //组件销毁时，清理掉定时器
    clearInterval(this.interval);
  }

  render() {
    return (
      <div>
        Seconds: {this.state.seconds}
      </div>
    );
  }
}

ReactDOM.render(<Timer />, mountNode);
```

## 简单的TODO应用
> 这里简单的混合使用了props和state去创建了一个todo的应用
```
//这里还是构造了一个todo的react组件，在构造过程中我们发现，继承了父类构造函数，初始化组件状态，此组件有两个可变状态，待办事项列表也就是那个items，另一个是用户输入的文本内容，也就是text。这里还初始化了两个针对这个组件的用户行为，一个是绑定在onchange事件上的handleChange回调，另外一个是绑定在onSubmit时间上的handleSubmit回调。
class TodoApp extends React.Component {
  constructor(props) {
    super(props);
    this.state = { items: [], text: '' };
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  render() {
    return (
      <div>
        <h3>TODO</h3>
        <TodoList items={this.state.items} />
        <form onSubmit={this.handleSubmit}>
          <input
            onChange={this.handleChange}
            value={this.state.text}
          />
          <button>
            Add #{this.state.items.length + 1}
          </button>
        </form>
      </div>
    );
  }

  handleChange(e) {
    this.setState({ text: e.target.value });
  }

  handleSubmit(e) {
    e.preventDefault();
    if (!this.state.text.length) {
      return;
    }
    const newItem = {
      text: this.state.text,
      id: Date.now()
    };
    this.setState(prevState => ({
      items: prevState.items.concat(newItem),
      text: ''
    }));
  }
}
//创建了一个显示所有待办事项的列表组件
class TodoList extends React.Component {
  render() {
    return (
      <ul>
        {this.props.items.map(item => (
          <li key={item.id}>{item.text}</li>
        ))}
      </ul>
    );
  }
}

ReactDOM.render(<TodoApp />, mountNode);
```

## 在组件中使用第三方的库
> 这个是利用第三方的库(Remarkable)实现一个markdown的编辑器
```
class MarkdownEditor extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = { value: 'Type some *markdown* here!' };
  }

  handleChange(e) {
    this.setState({ value: e.target.value });
  }

  getRawMarkup() {
    const md = new Remarkable();
    return { __html: md.render(this.state.value) };
  }

  render() {
    return (
      <div className="MarkdownEditor">
        <h3>Input</h3>
        <textarea
          onChange={this.handleChange}
          defaultValue={this.state.value}
        />
        <h3>Output</h3>
        <div
          className="content"
          //这个属性是react dom自有的，用来替换innerHTML,详情请看[官网文档](https://www.reactjscn.com/docs/dom-elements.html)
          dangerouslySetInnerHTML={this.getRawMarkup()}
        />
      </div>
    );
  }
}

ReactDOM.render(<MarkdownEditor />, mountNode);
```

## 总结
> 中文react官网的第一页看完了，让我们继续深入探索react吧