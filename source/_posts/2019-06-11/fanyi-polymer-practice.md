---
title: Polymer 1.x企业级的实现经历(翻译)
date: 2019-06-11 09:27:51
categories:
- 翻译
tags:
- polymer
---
## Polymer 1.x企业级的实现经历(http://andrewstacy.com/blog/my-experience-with-polymer-1-at-enterprise-scale-introduction.html)

> 思考用户行业的特点
1. 大量的特许经营的商店，并且每位私营业主在食品选择和制作，价格的定制上会有很多自主权
2. 大量的产品变动和频繁的更新

> 需要做什么
1. 需要一个框架，这个框架必须要满足以下的要求
    - 可以即时响应客户需求
    - 通过减少工作量降低公司成本
    - 它可以使团队达到企业级的最佳实践和代码组织水平

2. 需要有很好的文档
    - 在公司快速成长的同时，好的文档是对员工快速适应最好的资源。

3. 需要有高度的模块化作为核心
    - 基于不同店家可以快速的大幅度的改变。

作者在选型时认为web components是未来的趋势，可能当下并不那么被看好。

## 那么Web Components到底为我们解决了什么问题？
1. 支持真个美国15000家加盟店
2. 支持每家店不同的菜单界面的配置
3. 支持超1w产品的支持
4. 支持为每家店设置不同的界面布局
5. 支持基于每餐（早，中，晚）的不同样式
6. 基于NTP协议下的图片和高亮文本的同步
7. 基于NTP协议下的菜单界面区域
8. 提供舒适的用户编辑界面
9. 3个月内验收

{% cq %}
"Shadow DOM removes the brittleness of building web apps. The brittleness comes from the global nature of HTML, CSS, and JS." (Bidelman) - 影子树去除了构建web应用中脆弱的东西，而这些脆弱的东西来自于html, css 和 js的天性。

"Shadow DOM fixes CSS and DOM. It introduces scoped styles to the web platform. Without tools or naming conventions, you can bundle CSS with markup, hide implementation details, and author self-contained components in vanilla JavaScript." (Bidelman) - 影子树完善了css和dom， 它将scoped的样式带入网页平台。不需要借助工具，命名规范，你就可以把css和标签融合在一起，隐藏实现的细节，通过原生js创作独立的组件。
{% endcq %}

我们可以把web components组件看作是乐高玩具中的一块，我们可以以最小的成本随意的拼装

以下是web components至关重要的几点：
1. HTML Templates
2. Shadow DOM
3. Custom elements
4. HTML imports

## 项目的结构
1. Base Components
    - 这个是应用中最小的部分，是最底层的一个单元，比如base-header,base-product-table, base-image-rotator等等
2. Region Components
    - 这些是由基础单元组成的组合组件，提供整个菜单页中某一个区域的可视化部分
3. Layout Components
    - 这些事控制区域组件需要在什么位置去展示的组件，它也是菜单页中的一部分
4. Master Components
    - 这个是一个入口的组件包含页面所有可视化的部分，它是基于设备来选择布局


