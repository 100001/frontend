例子：
```
    var Obj = function(){
        this.change = function(){
            console.log('changeSize');
        };
        this.handleEvent = function(e){
            console.log('handleEvent',e.type,e);
            this.change();
        }
    };
    window.addEventListener('resize', new Obj(), false);
```
标准浏览器中执行以上代码，在改变浏览器大小，会发现 handleEvent 方法被执行了，具体原因参考：
[w3c](http://www.w3.org/TR/DOM-Level-2-Events/events.html#Events-EventListener)

这样写代码有个好处，就是可以直接在handleEvent 方法中调用 Obj 对象的方法和属性。例如 例子中
hangleEvent调用了change方法。
