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
       2.然后事件委托机制的原理就浮现了：(给ul下的li绑定事件)
               <script>
                    //以下代码执行顺序为：
                    //1.先找到ul元素
                    //2.然后找到ul下的li
                    //3.然后通过判断
                    /*$('ul > li').each(function(index, item){
                        //只有当条件成立时，才会执行传入的事件处理函数。
                        //这里的事件对象把它当成是父元素相应的事件处理函数的参数就行。也就是说，父元素的事件处理函数不执行任何功能性代码，只用于执行以下的判断条件
                        
                        if ( item === e.target ) {
                            handler(e);
                        }
                    })*/

                    ------------------------------------------------------------------
                    //以上注释代码用于逻辑推断，不适用于代码书写
                    $('ul').on('click','li',function(e){
                        console.log(e.target)
                    })
                    $('ul').on('click',function(e){
                        console.log(e.target);
                    })
                </script>
    ```
    
* 不知道你有没有注意到在事件绑定的几种方式中，一直有那么一个默默无闻的参数静静的徜徉在方括号中，无人问津。没有错的，那就是data。

    话不多说，看代码

    ```js
    //关于data的用法  事件对象.data = data 
    $('ul').on('click','li',{name:'zhangsan',age:10}, function(e){
        $('ul > li').each(function(index, item){
            //只有当条件成立时，才会执行传入的事件处理函数。
            if ( item === e.target ) {
                console.log(e.data);
                //Object {name: "zhangsan", age: 10}
            }
        })
    })
    ```
