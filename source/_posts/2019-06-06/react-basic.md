---
title: 跟着官方文档自学react-basic
date: 2019-06-06 09:27:10
categories:
- web
tags:
- react
---
## 条件渲染
> 在react中，你可以通过状态的变化选择显示不同的组件。使用js的if或是条件运算符来完成。
> 具体的例子可以参考文档中提到的https://www.reactjscn.com/docs/conditional-rendering.html
> 逻辑与运算符(&&)和三目运算符
> 通过在render函数中返回null来阻止渲染。它不会影响组件生命周期的回调。

## 列表与keys
> 渲染多个组件，可以通过{}在jsx内构建一个元素集合。
> 基础列表组件，在出现有多个相同react元素时，react内部通过特殊属性key来识别哪个元素发生变化
> 元素key只有它和它的兄弟节点对比时才有意义，并且这个是唯一的。
> key这个特殊属性无法传递给组件，需要将传递给那些可被传递的属性。
> JSX允许{}中嵌入任何表达式。

## 表单
> react负责渲染表单的组件仍然控制用户后续输入说发生的变化。相应的，其值由react控制的输入表单元素称为受控组件。
{% note default %}
说白了，就是react创建的这个form表单，它会去控制状态，更新输入输出值，然后再传递给子组件，这种情况下子组件就是受控组件，是不是有点束手束脚的感觉？
{% endnote %}
> 常见的一个内置的受控组件有input,textarea,select etc, 但这里有个特殊情况是当input的type="file",他是react中的一个非受控组件https://reactjs.org/docs/uncontrolled-components.html#the-file-input-tag。
> 多个输入的解决办法是通过给每一个元素添加name属性来实现
```
class Reservation extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isGoing: true,
      numberOfGuests: 2
    };

    this.handleInputChange = this.handleInputChange.bind(this);
  }

  handleInputChange(event) {
    const target = event.target;
    const value = target.type === 'checkbox' ? target.checked : target.value;
    const name = target.name;

    this.setState({
      [name]: value
    });
  }

  render() {
    return (
      <form>
        <label>
          Is going:
          <input
            name="isGoing"
            type="checkbox"
            checked={this.state.isGoing}
            onChange={this.handleInputChange} />
        </label>
        <br />
        <label>
          Number of guests:
          <input
            name="numberOfGuests"
            type="number"
            value={this.state.numberOfGuests}
            onChange={this.handleInputChange} />
        </label>
      </form>
    );
  }
}
```
> 当您将预先存在的代码库转换为React或将React应用程序与非React库集成时，这可能变得特别烦人。在以上情况下，你或许应该看看非受控组件，这是一种表单的替代技术。

## 状态提升
> 有时候遇到需要几个组件共享状态数据的情况，这个时候就需要将状态从子组件中剥离出来提升至他们最近的父组件中进行管理。
```
class Calculator extends React.Component {
  constructor(props) {
    super(props);
    this.handleCelsiusChange = this.handleCelsiusChange.bind(this);
    this.handleFahrenheitChange = this.handleFahrenheitChange.bind(this);
    this.state = {temperature: '', scale: 'c'};
  }

  handleCelsiusChange(temperature) {
    this.setState({scale: 'c', temperature});
  }

  handleFahrenheitChange(temperature) {
    this.setState({scale: 'f', temperature});
  }

  render() {
    const scale = this.state.scale;
    const temperature = this.state.temperature;
    const celsius = scale === 'f' ? tryConvert(temperature, toCelsius) : temperature;
    const fahrenheit = scale === 'c' ? tryConvert(temperature, toFahrenheit) : temperature;

    return (
      <div>
        <TemperatureInput
          scale="c"
          temperature={celsius}
          onTemperatureChange={this.handleCelsiusChange} />

        <TemperatureInput
          scale="f"
          temperature={fahrenheit}
          onTemperatureChange={this.handleFahrenheitChange} />

        <BoilingVerdict
          celsius={parseFloat(celsius)} />

      </div>
    );
  }
}
```
> 编辑输入框所发生的基本流程
1. React在DOM原生组件input上调用指定的onChange函数。在本例中，指的是TemperatureInput组件上的handleChange函数。
2. TemperatureInput组件的handleChange函数会在值发生变化时调用this.props.onTemperatureChange()函数。这些props属性，像onTemperatureChange都是由父组件Calculator提供的。
3. 当最开始渲染时，Calculator组件把内部的handleCelsiusChange方法指定给摄氏输入组件TemperatureInput的onTemperatureChange方法，并且把handleFahrenheitChange方法指定给华氏输入组件TemperatureInput的onTemperatureChange。两个Calculator内部的方法都会在相应输入框被编辑时被调用。
4. 在这些方法内部，Calculator组件会让React使用编辑输入的新值和当前输入框的温标来调用this.setState()方法来重渲染自身。
5. React会调用Calculator组件的render方法来识别UI界面的样子。基于当前温度和温标，两个输入框的值会被重新计算。温度转换就是在这里被执行的。
6. 接着React会使用Calculator指定的新props来分别调用TemperatureInput组件，React也会识别出子组件的UI界面。
7. React DOM 会更新DOM来匹配对应的值。我们编辑的输入框获取新值，而另一个输入框则更新经过转换的温度值。
> 需要注意的几点：
1. 始终保持自上而下的数据流，当自组件的状态需要被其他兄弟组件获得，那么你就需要把控制权交出来给临近的父节点，如果是夸了好几个父节点的话，目前的话，你就必须把状态控制权一直往提交。在我看来并不是一个很好的设计思想，因为有的状态可能只是给少数几个组件，只不过组件之间跨越了不同层级关系。
2. 状态提升比双向绑定方式要写更多的“模版代码”，但带来的好处是，你也可以更快地寻找和定位bug的工作。因为哪个组件保有状态数据，也只有它自己能够操作这些数据，发生bug的范围就被大大地减小了。此外，你也可以使用自定义逻辑来拒绝或者更改用户的输入。
3. 如果某些数据可以由props或者state提供，那么它很有可能不应该在state中出现。举个例子，我们仅仅保存最新的编辑过的temperature和scale值，而不是同时保存 celsiusValue 和 fahrenheitValue 。另一个输入框中的值总是可以在 render() 函数中由这些保存的数据计算出来。这样我们可以根据同一个用户输入精准计算出两个需要使用的数据。
4. 当你在开发UI界面遇到问题时，你可以使用 React 开发者工具来检查props属性，并且可以点击查看组件树，直到你找到负责目前状态更新的组件。这能让你到追踪到产生 bug 的源头。

## 组合vs继承
> React具有强大的组合模型，建议多使用组合而不是继承
> 包含关系，一些组件不能提前预知子组件是什么的情况下可以使用
```
function SplitPane(props) {
  return (
    <div className="SplitPane">
      <div className="SplitPane-left">
        {props.left}
      </div>
      <div className="SplitPane-right">
        {props.right}
      </div>
    </div>
  );
}
//这里我们可以看到react元素本身也可以作为props传递给子组件
function App() {
  return (
    <SplitPane
      left={
        <Contacts />
      }
      right={
        <Chat />
      } />
  );
}
```
> 至于继承？
{% note summary %}
在 Facebook 网站上，我们的 React 使用了数以千计的组件，然而却还未发现任何需要推荐你使用继承的情况。

属性和组合为你提供了以清晰和安全的方式自定义组件的样式和行为所需的所有灵活性。请记住，组件可以接受任意元素，包括基本数据类型、React 元素或函数。

如果要在组件之间复用 UI 无关的功能，我们建议将其提取到单独的 JavaScript 模块中。这样可以在不对组件进行扩展的前提下导入并使用该函数、对象或类。
{% endnote %}

## React理念
> react的初衷是想使用js创建大型且快速响应的web应用
> 如何快速创建react UI
1. 把 UI 划分出组件层级
2. 用 React 创建一个静态版本
3. 定义 UI 状态的表示
4. 确定你的 State 应该位于哪里
找出哪一个是 state。每个数据只要考虑三个问题：
{% note summary %}
它是通过 props 从父级传来的吗？如果是，他可能不是 state。
它随着时间推移不变吗？如果是，它可能不是 state。
你能够根据组件中任何其他的 state 或 props 把它计算出来吗？如果是，它不是 state。
{% endnote %}
5. 添加反向数据流