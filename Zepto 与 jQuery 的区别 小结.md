1. Zepto 对象 不能自定义事件
  例如执行： 
    $({}).bind('cust', function(){});
  结果： 
    TypeError: Object has no method 'addEventListener'
  
  解决办法是创建一个脱离文档流的节点作为事件对象：
  例如： 
    $('<div>').bind('cust', function(){});

2. Zepto 的选择器表达式: [name=value]  中value 必须用 双引号 "  or 单引号 ' 括起来
  例如执行：
    $('[data-userid=123123123]')
  结果：
    Error: SyntaxError: DOM Exception 12
  解决办法： 
    $('[data-userid="123123123]"');
    //or
    $("[data-userid='123123123']");

3.Zepto 是根据标准浏览器写的，所以对于节点尺寸的方法只提供 width() 和 height()，省去了 innerWidth(), innerHeight(),outerWidth(),outerHeight()

4.Zepto 的each 方法只能遍历 数组，不能遍历JSON对象

5.Zepto 的animate 方法参数说明 ：
例如：
    $("data-userid='123123123'").animate({ opacity : 0},{duration:'slow'});
其中的duration : 'slow' 是无效的，需要修改为 duration : 600
