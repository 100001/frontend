1.在IE中使用attachEvent()与使用DOM0级方法的主要区别在于事件处理程序的作用域。DOM0级的事件处理程序会在其所属元素的作用域内运行，attachEvent()会在全局作用域运行，因此this等于window。
例：

     var btn = document.getElementById('btn');
     btn.attachEvent('onclick',function(){
       alert(this === window);//true;
     });

2.通过attachEvent()为同一个元素添加两个方法，其执行顺序是先添加后执行。以下例子的执行顺序是先2后1
例：

     var btn = document.getElementById('btn');
     btn.attachEvent('onclick',function(){
       alert(1);
     });
     btn.attachEvent('onclick',function(){
       alert(2);
     });