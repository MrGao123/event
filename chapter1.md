## 1.原生js的事件（[在之前的兼容里有详细介绍](http://example.net/)）

## 2.jQuery的事件 

> 简单事件绑定 >> bind >> delegate >> on

* 2.1 bind事件绑定
    + $(selector).bind(eventType,handler)
    
    优点：可以绑定多个事件，即eventType可以是：'click mousemove';
    
    缺点：不能为**动态创建**出来的元素添加事件。
* 2.2 delegate事件绑定
    + $(parentElement).delegate(subElement, eventType, handler);
    
    可以为动态创建出来的元素绑定事件（原理：事件的冒泡机制）
* 2.3 on事件绑定
    + $(selector).on(eventType[,subElement],handler[,isCapture])
 
