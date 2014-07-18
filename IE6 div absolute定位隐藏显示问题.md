前置条件：
      IE6浏览器，在页面中有div A 和 div B，B是A的子节点，B的position:absolute;
代码流程：
       1.隐藏(display:none)A；
       2.隐藏(display:none)B；
       3.显示(display:block)A；
实际结果：
       A显示出来后，B也显示出来。
预期结果：
       只显示A。
解决方案：
       1.修改隐藏流程：先隐藏B，再隐藏A；
       2.修改B的隐藏方法：left:-9999px;