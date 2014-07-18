1.在IE6里，如果给一个未添加到DOM树的img对象设置了width，而没设置height，
img的height不会等比例适配，当在页面中渲染时，图片比例会失调。
例子如下：

       window.onload = function() {
         var div = document.getElementById('test');
         var img = new Image();
         img.onload = function() {
                img.width = 600;
                div.appendChild(img);
         };
         img.src='http://img0.bdstatic.com/img/image/shouye/dengni41.jpg';
      };

2.动态创建style标签时，在IE6,7,8中需要声明style标签对象的type属性，code如下:

      var style = document.createElement('style');
      style.type = 'text/css';

另外，对于IE浏览器，要向style标签中赋值，需要code如下

      if(style.styleSheet){
        style.styleSheet.cssText = styleValue;
      }

以上赋值过程中，千万不能写成 

      style['styleSheet'].cssText = styleValue; 

这样的会无法赋值，只能通过 . 的方式访问style对象的属性
