
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>Test</title>
    <script type="text/javascript">
        function test1(){
            var t = document.getElementByIdx_x('t1');
            var cls = t.className;
            if(cls.indexOf('same') == -1){
                t.className = cls + ' same';
            }else{
                t.className = 'test1';
            }
        }

        function test2(){
            var t = document.getElementByIdx_x('t2');
            var cls = t.className;
            if(cls.indexOf('same') == -1){
                t.className = cls + ' same';
            }else{
                t.className = 'test2';
            }
        }
    </script>
    <style type="text/css">
        .test1 {background:red;width:200px;height:100px;cursor:pointer;}
        .test1.same{background:blue;}
        .test2 {background:green;width:200px;height:100px;cursor:pointer;}
        .test2.same{background:black;}
    </style>
    </head>

    <body>
    <div id=t1 class='test1' onclick="test1();"></div>
    <div id=t2 class='test2' onclick="test2();"></div>
    </body>
    </html>


以上代码在ie6中执行时，点击t1后，t1的背景色并没有变为.test1.same 的blue,而是被附上了.test2.same 的样式。
解决翻案：将类选择器.test1.same 中.same 改名，与.test2.same区别开发，例如.test1.same1,这样就可以正确执行了。