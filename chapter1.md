## 1.原生js的事件（[在之前的兼容里有详细介绍](http://example.net/)）

## 2.jQuery的事件 

> 简单事件绑定 >> bind >> delegate >> on

* 2.1 bind事件绑定
    + $(selector).bind(eventType[,data],handler)
    
    优点：可以绑定多个事件，即eventType可以是：'click mousemove';
    
    缺点：不能为**动态创建**出来的元素添加事件。
* 2.2 delegate事件绑定
    + $(parentElement).delegate(subElement, eventType[,data], handler);
    
    可以为动态创建出来的元素绑定事件（原理：事件的冒泡机制）
* 2.3 on事件绑定：将事件绑定做了一个统一。
    + $(selector).on(eventType[,subElement],[data],handler);     
* jQuery的事件委托
    ### 不使用事件委托的缺点：
    + 1.大量的事件绑定，性能消耗，而且还需要解绑。
    + 2.绑定的元素必须要存在。
    + 3.后期生成的元素会没有事件绑定，需要重新绑定。
    + 4.语法过于繁杂。
    + 5.委托机制的原理：

    ```
       1.首先我们得知道：事件对象中有个target属性：即e.target--->指的是当前触发事件的目标元素。 
       2.然后事件委托机制的原理就浮现了：
       <!doctype html>
        <html lang="en">
            <head>
                 <meta charset="UTF-8">
                 <title>Document</title>
                 <style>
                     * {
                         margin: 0;
                         padding: 0;
                       }
                    ul {
                         list-style: none;
                       }
                    li {
                         line-height: 30px;
                         background-color: red;
                         margin: 30px;
                        }
                 </style>
            </head>
            <body>
                <ul>
                    <li>1</li>
                    <li>2</li>
                    <li>3</li>
                    <li>4</li>
                    <li>5</li>
                </ul>
                <script src="./jquery-1.12.4.js"></script>
                <script>
                    //以下代码执行顺序为：
                    //1.先找到ul元素
                    //2.然后找到ul下的li
                    //3.然后通过判断
                    /*$('ul > li').each(function(index, item){
                        //只有当条件成立时，才会执行传入的事件处理函数。
                        if ( item === e.target ) {
                            handler(e);
                        }
                    })*/

                    ------------------------------------------------------------------
                    //以上代码用于逻辑推断，不适用于代码书写
                    $('ul').on('click','li',function(e){
                        console.log(e.target)
                    })
                    $('ul').on('click',function(e){
                        console.log(e.target);
                    })
                </script>
            </body>
        </html>    
    ```
    

