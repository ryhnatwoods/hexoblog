---
title: 跟着官方文档自学advanced-react
date: 2019-06-06 12:20:55
categories:
- web
tags:
- react
---
## 深入JSX
> 本质上来讲，JSX只是为React.createElement(Component, props, ...children)提供的语法糖
> 指定react的元素类型
1. react必须声明
2. react可以用点表示法或取，某个组件中的子组件
3. 首字母大写，区别html原生标签
4. 在运行时选择类型，需要先将类型赋值给大写的变量，不支持表达式形式的标签名
> 属性
1. 使用js表达式
2. 字符串常量，当传递一个字符串常量时，该值会被解析为HTML非转义字符串。
3. 当没有给属性传值时，默认为true
4. 扩展属性
> JSX子代的表现形式
1. 字符串常量
2. JSX
3. js表达式
4. 函数
5. 布尔，null和undefined都是有效子代，但是不会被渲染
{% note warning %}
如果你想让类似 false、true、null 或 undefined 出现在输出中，你必须先把它转换成字符串
{% endnote %}

## 使用PropTypes进行类型检查
{% note warning %}
注意: React.PropTypes 自 React v15.5 起已弃用。请使用 prop-types 库代替。
{% endnote %}
> 具体参考https://www.reactjscn.com/docs/typechecking-with-proptypes.html

## 静态类型检查
> Flow针对js代码的静态类型检查器。
{% note warning %}
为了使用 Flow, 你需要：
将 Flow 添加到您的项目作为依赖项。
确保编译后的代码中去除了 Flow 语法。
添加了类型注释并运行 Flow 来检查它们。
{% endnote %}
1. 在一个项目中添加flow
```
npm install --save-dev flow-bin
npm run flow init
```
2. 从编译后的代码中剥离Flow
{% note summary %}
Create React App
如果你的项目是使用 Create React App 建立的，恭喜！ Flow 此时已经被默认剥离，所以在这一步你不需要做任何事情。
{% endnote %}
3. 配置Babel
```
npm install --save-dev babel-preset-flow
```
> 然后将 flow preset 加入你的 Babel 配置。比如，如果你通过 .babelrc 文件配置 Babel，它可能会如下所示
```
{
  "presets": [
    "flow",
    "react"
  ]
}
```
{% note summary %}
Flow 不需要 react preset，但他们经常在一起使用。 Flow 本身就理解 JSX 语法。
{% endnote %}
4. 运行flow
```
npm run flow
```
5. 添加Flow注释

> 配置TypeScript的过程差不多，文档很详细https://www.reactjscn.com/docs/static-type-checking.html

## Refs和DOM
> Refs提供了一种访问在render方法中创建的DOM和react元素的方式
1. 在典型数据流外强制修改子组件为react组件的实例
2. 在典型数据流外强制修改子组件为DOM元素
> 何时使用Refs
- 处理焦点，文本选择或媒体控制
- 触发强制动画
- 集成第三方DOM库
> 不要过度使用Refs，如果可以,状态提升是更适合的做法。
> 创建Refs
- React.createRef()创建refs，通过ref属性获得react元素
> 访问Refs
- 当一个ref属性被传递给一个render函数中的元素，可以使用ref中的current属性对节点引用进行访问
1. 当ref属性被用于普通html，React.createRef()将接收底层DOM元素作为它的current属性对节点的引用进行访问
2. 当ref属性被用于一个自定义类组件时，ref对象将接收该组件已挂载的实例作为它的current
3. 不能在函数式组件上使用ref属性，因为没有实例
{% note summary %}
为DOM元素添加Ref
```
class CustomTextInput extends React.Component {
  constructor(props) {
    super(props);
    // 创建 ref 用于存储 textInput DOM 元素
    this.textInput = React.createRef();
    this.focusTextInput = this.focusTextInput.bind(this);
  }

  focusTextInput() {
    // 直接使用原生 API 使 text 输入框获得焦点
    // 注意：通过 "current" 取得 DOM 节点
    this.textInput.current.focus();
  }

  render() {
    // 告诉 React 我们想把 <input> ref 关联到构造器里创建的 `textInput`变量上
    return (
      <div>
        <input
          type="text"
          ref={this.textInput} />

          
        <input
          type="button"
          value="Focus the text input"
          onClick={this.focusTextInput}
        />
      </div>
    );
  }
}
```
React会在组件加载时将DOM元素传入current属性，在卸载时则会改为null。ref的更新会发生在componentDidMount或componentDidUpdate生命周期之前。
也可以在函数式组件内部使用ref，只要其指向DOM或者自定义组件
```
function CustomTextInput(props) {
  // 这里必须声明 textInput，这样 ref 回调才可以引用它
  let textInput = null;

  function handleClick() {
    textInput.focus();
  }

  return (
    <div>
      <input
        type="text"
        ref={(input) => { textInput = input; }} />

      <input
        type="button"
        value="Focus the text input"
        onClick={handleClick}
      />
    </div>
  );  
}
```
{% endnote %}
> 对父组件暴露DOM节点
- 在极少数情况下你可能希望从父组件访问子节点的dom节点
处理的方案有以下几种
1. Ref 转发使组件可以像暴露自己的 ref 一样暴露子组件的 ref。
2. 将 ref 作为特殊名字的 prop 直接传递。
3. findDOMNode()，但是不推荐。
> 回调Refs
- 函数接受React组件的实例或是HTML DOM元素作为参数，用以存储和被访问
{% note warning %}
如果 ref 回调以内联函数的方式定义，在更新期间它会被调用两次，第一次参数是 null ，之后参数是 DOM 元素。这是因为在每次渲染中都会创建一个新的函数实例。因此，React 需要清理旧的 ref 并且设置新的。通过将 ref 的回调函数定义成类的绑定函数的方式可以避免上述问题，但是大多数情况下无关紧要。
{% endnote %}

## 性能优化
{% note warning %}
更新UI时，React在内部使用几种巧妙的技术来优化DOM操作数量，对应用来说，使用react不需要做太多的优化工作就可以快速创建用户界面。除此之外，还有一些优化react应用性能的办法。
{% endnote %}
> 使用生产版本
> 使用chrome performance归档组件
  - https://building.calibreapp.com/debugging-react-performance-with-react-16-and-chrome-devtools-c90698a522ad
> 避免重复渲染
  - React在渲染出的UI内部简历和维护了一个内层的实现方式，它包括了从组建返回的react元素。这一层实现就称为虚拟dom。
    当一个组件的props和state改变时，react通过新返回的元素和之前渲染的元素作比较来决定是否更新dom。在某些情况下，可以重写生命周期函数shouldComponentUpdate通过返回false直接跳过比较和渲染阶段从而提升速度。
    {% fullimage /images/should-component-update.png, 'scu', 'shouldComponentUpdate流程图' %}
    SCU表明了shouldComponentUpdate的返回内容，vDOMEq表明了待渲染的React元素与原始元素是否相等。
> 如果状态是对象类型，请创建一个新的对象包含变得内容，这样才能保证react可以正确比较和渲染。
  另外immutable.js是解决这个问题的另一种方法，它通过结构共享提供不可变的，持久的集合。
  - 不可突变:一旦创建，集合就不能在另一个时间点改变。
  - 持久性:可以使用原始集合和一个突变来创建新的集合。原始集合在新集合创建后仍然可用。
  - 结构共享:新集合尽可能多的使用原始集合的结构来创建，以便将复制操作降至最少从而提升性能。



