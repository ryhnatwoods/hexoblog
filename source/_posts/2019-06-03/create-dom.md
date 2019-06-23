---
title: 控制DOM的几种js方法
date: 2019-06-03 23:19:53
categories:
- javascript
tags:
- DOM
---
## 控制DOM的几种js方法[译](https://devinduct.com/blogpost/20/13-javascript-methods-useful-for-dom-manipulation)

{% note summary %} 
DOM, 亦可称之为文档对象模型，代表整个HTML文档，可以通过其来访问页面中的所有元素，每个载入浏览器的HTML文档都会成为document的对象。它使脚本访问HTML页面元素成为可能。
{% endnote %}

1. document.querySelector/document.querySelectorAll
> document.querySelector返回的是匹配的第一个元素
> document.querySelectorAll返回的是匹配的所有元素
```
//return an Element
const ul_first = document.querySelector('ul');
//return an array-like Elements 
const ul_list = document.querySelectorAll('ul');
```

2. document.creatElement
> 根据tag name创建一个元素。具体说明，请移步到[这里](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/createElement)

3. Node.appendChild
> 追加节点在当前节点中子节点的末尾。
```
let list = document.createElement('ul'); // creates a new list
['Paris', 'London', 'New York'].forEach(city => {
    let listItem = document.createElement('li');
    listItem.innerText = city;
    list.appendChild(listItem);
});
document.body.appendChild(list);
```

4. Node.insertBefore
> 插入新节点在当前子节点的前面
```
let list = document.querySelector('ul');
let firstCity = list.querySelector('ul > li'); // here we could use list.firstChild, but the purpose of this article is to show DOM API methods
let newCity = document.createElement('li');
newCity.textContent = 'San Francisco';
list.insertBefore(newCity, firstCity);
```

5. Node.removeChild
> 从一个指定的DOM树节点中移除其指定的子节点，返回一个被移除的那个节点
```
let list = document.querySelector('ul');
let firstItem = list.querySelector('li');
let removedItem = list.removeChild(firstItem);
```

6. Node.replaceChild
> 用一个新的节点或者存在的节点替换掉指定节点中的某一个节点,返回一个被替换掉的那个老节点
```
let list = document.querySelector('ul');
let oldItem = list.querySelector('li');
let newItem = document.createElement('li');
newItem.innerHTML = 'Las Vegas';
let replacedItem = list.replaceChild(newItem, oldItem);
```

7. Node.cloneNode
> 创建一个指定节点的副本，他有一个boolean的参数，是一个可选项，true代表克隆本身和其所有子节点，false代表只克隆自己，不包括子节点。建议是按需求指定这个boolean值。具体参见[MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/cloneNode)
```
let list = document.querySelector('ul');
let clone = list.cloneNode();
```

8. Element.getAttribute/Element.setAttribute
> 给指定元素节点设置属性和获取属性
```
let list = document.querySelector('ul');
list.setAttribute('id', 'my-list');
let id = list.getAttribute('id');
console.log(id); // outputs my-list
```

9. Element.hasAttribute/Element.removeAttribute
> 检查当前元素是否有这个属性和移除这个属性
```
let list = document.querySelector('ul');
if (list.hasAttribute('id')) {
    console.log('list has an id');
    list.removeAttribute('id');
};
```

10. Element.insertAdjacentHTML
> 插入指定的HTML片段到指定的位置，输入一个位置信息和html字符串。
> 这里需要注意的是，如果是客户端输入是需要转义的。如果只是插入文本节点最好是用node.textContent,因为这里需要HTML解释器的转换，具体参考[MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/insertAdjacentHTML)
```
<!-- beforebegin -->
<div>
  <!-- afterbegin -->
  <p>Hello World</p>
  <!-- beforeend -->
</div>
<!-- afterend -->

var list = document.querySelector('ul');
list.insertAdjacentHTML('afterbegin', '<li id="first-item">First</li>');
```