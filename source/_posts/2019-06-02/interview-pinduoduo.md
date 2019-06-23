---
title: 面试题
date: 2019-06-02 22:49:40
categories:
tags:
---

## 拼多多面试题
---------------------
1. 介绍自己
2. 介绍JET
3. 介绍LA
4. 在项目中做了什么，多少页面，做UI的有多少人
5. LA项目中的 viewmodel，uimodel，model是怎么划分的
6. Angular JS 双向绑定机制
7. 怎么优化Performance
8. 如果有极大量的数据和请求，浏览器会hang住很久，怎么优化。所有数据都是必须的
9. setTimeout setInterval 概念
10. 一小时倒计时器，用setInterval 实现，但是用户反馈不准确，有时差，为什么？怎么改进？
11. CSS 如何实现水平居中和垂直居中
12. CSS 选择器优先级
13. jQuery on 实现原理
14. based on 上一条，如果off是on的返回，怎么写
15. MVC的含义
16. CSS position 有哪些取值，作用是什么
17. CSS 伪类有哪些
18. 5个并发请求，怎么确保在他们都执行完之后，再做处理：Promise。面试官的意思还有别的答案
19. 怎么实现$.when
20. 跨域请求
21. Git 基础指令
22. 怎么一键切换网页显示模式：白天、夜晚

## VMWARE的面试题
----------------------
1. 介绍自己和项目
2. css: position 有哪些值及具体用法
    1. 怎么实现
3. css: z-index 具体用法（什么时候生效）
    1. <div><div style=“z-index:100;”></div><div><div style=“z-index: 20;”></div></div> 所有div都是绝对定位的，浏览器会怎么显示？
4. css选择器优先级
5. css伪类例举
    1. :first-child :first-line 的区别
6. 怎么实现垂直居中
7. 怎么隐藏一个html元素
    1. Display:none / visibility: hidden / html5 hidden 差别？
8. SASS / LESS，主要特点
9. 事件流
10. HTTP请求种类
    1. PUT vs POST
    2. PATCH
11. Promise
    1. 与普通的异步请求有什么不同
12. ES6 语法
    1. const obj = {a: 1}; obj.a = 2;   // 问a的值被改了么？
13. VUE: 父子component之间怎么传值？
    1. 为什么要用emit，而不允许子component直接修改props里的值
14. var a = 1; function test(b) { b = 2; }; test(a);  // 求a
15. var a = {key: 1}; function test(b) { b.key = 2; }; test(a); // 求a.key
16. var a = {key: 1}; function test(b) { b = {key: 2}; }; test(a); // 求a.key
17. 如何实现一个function add：使add(1)(2) 返回3
18. 有一个包含重复数字的array，如何去重
19. 斐波那契数列（1,2,3,5,8…）现实一个方法，输入n，得到数列里的第n个值

技术栈：Angular7

## 阿里口碑的面试题
----------------------------
{% note summary %}
面试官纠结于如何发布以及快速响应user发现的bug
特别强调自主研究能力，自学，自己做项目

原型链
响应式布局（面试官建议：PC Mobile 完全分开写）
webPack
事件冒泡和事件捕获
事件的浏览器兼容性

反转String
String.pritotype.replace 第二个参数能否是函数？具体用法
String 的 trim 不兼容的解决方案
用Array模拟栈：Array.prototype.push           & Array.prototype.pop
正则：贪婪、非贪婪
正则里的特殊字符及用法

CSS水平居中垂直居中
CSS 盒模型
Flex具体语法
Promise
5个并发请求，如何做到所有请求都完成之后，再做处理？（注：若一个请求失败了，其他请求还要继续）
ES6 async
HTTP请求的种类，Get 和 POST 的区别
HTTP请求返回301/302的指？重定向
安全漏洞及如何预防
{% endnote %}


## SAP面试题
----------------------------
{% note summary %}
Javascript deepcopy
0.1+0.2精度问题
原型链
ajax底层实现
Student.prototype === Student.__proto__
html5 新特性
jQuery底层实现
浏览器存储有哪些，及区别
跨域
knockoutjs 双向绑定原理
Vue 双向绑定原理
设计模式
各种后端 Database

英文面：阅读理解
{% endnote %}