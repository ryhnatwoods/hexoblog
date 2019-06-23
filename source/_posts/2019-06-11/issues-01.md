---
title: removeEventListener不工作了
date: 2019-06-11 18:28:56
categories:
- bug
tags:
- js
---
## 今天在看一道[练习题](https://github.com/zhangxinxu/quiz/issues/27)
> 然后发现有不少伙伴解题思路很好。
模仿了下，发现有个监听事件始终无法被remove。
奇怪了，代码里明明remove了那个监听，还是可以被触发。
```
let _handleMove = (evt) => {
                        var evt = evt.touches&&evt.touches[0] || evt;
                        if (!this.start.length) {
                            this.start = [evt.pageX, evt.pageY];
                        }
                        let boxes = document.querySelectorAll('.box');
                        boxes.forEach((el)=>{
                            if(_isCovered(evt,el))
                                el.classList.add('active');
                            else
                                el.classList.remove('active');
                        });
                    };

let _handleUp = (ev) => {
                        if (this.start.length) {
                            this.start.length = 0;
                        } else {
                            if (!ev.target.className.includes('box')) {
                                clear();
                            }
                        }
                        window.getSelection().removeAllRanges();//清除选中区域
                        document.removeEventListener(this.currEvent.move, _handleMove.bind(this));
                    };
```
后面发现是因为bind(this),导致移除的回调函数和之前的不一样所致。
```
let _handleMove = ((evt) => {
                        var evt = evt.touches&&evt.touches[0] || evt;
                        if (!this.start.length) {
                            this.start = [evt.pageX, evt.pageY];
                        }
                        let boxes = document.querySelectorAll('.box');
                        boxes.forEach((el)=>{
                            if(_isCovered(evt,el))
                                el.classList.add('active');
                            else
                                el.classList.remove('active');
                        });
                    }).bind(this);
```
这种细节的东西还是太容易忽视了

https://jsfiddle.net/ryhnatwoods/6dz4psr3/2/