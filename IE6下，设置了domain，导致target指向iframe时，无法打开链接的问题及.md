 项目中测试出一个bug，就是在ie6下，下面的代码中的a标签，点击将没有任何反应：
    <a href="b.htm" target="frm">xxx</a>
    <script type="text/javascript">document.domain="beinet.cn";</script>
    <iframe name="frm"></iframe>

而非常奇怪的是，在公司的电脑中，有的IE6能正常打开链接，有的IE6不能打开链接，使用IETester模拟的IE6也不能打开链接，在IE7,IE8或Firefox等均可以打开链接

经过反复的测试，发现是domain设置的问题，删除domain的设置就正常了，但是这个domain的设置是为了跨多个子域，不能删除，
经过测试，找到了另一个解决方案：创建一个html，里面就一句：
```
    <script type="text/javascript">document.domain="beinet.cn";</script>
```
然后上面的iframe的src指向这个html，也能正常，但是如果iframe所在的页面如果没设置domain，或设置的不一样，也会造成target无效

估计不能下载的ie6是有什么特殊设置吧，问题也一直没有搞清楚到底是什么特殊设置造成的，而IETester没有设置也不能下载。

都知道在进行跨二级域的DOM操作时，document.domain必须设置。比如www.67ge.com页面中的含有一个wyz.67ge.com的子页面（iframe引用），要想对其进行操作通常设置

    document.domain="67ge.com";

现在有个问题，父页面中的含有一个同域的iframe，但是手工设置了

    document.domain=location.host;

这时在IE6/7/8/9下对IFRAME的操作也是报错的！这个问题并不常见，但也很容易发生。
也就是说对于IE而言，document.domain的设置其实有三种情况（拿www.67ge.com作为父页来说）：

不写document.domain，默认与location.host相同，也就是www.67ge.com
显示设置document.domain=location.host，或document.domain="www.67ge.com"
document.domain为上一级域名，即document.domain="67ge.com"
测试1（略，一切正常）：父子页面同域，都不显示定义document.domain
测试2（异常）：父子页面同域，显示设置了父页document.domain=location.hostname，不设置子页面内的document.domain

    document.domain=location.hostname;
    ifr = document.getElementById("ifr");
    try{
        ifr.contentWindow.document.write("success!");
        ifr.contentWindow.document.close();
    }catch(e){
        alert(e.message); //弹出“拒绝访问”
    }
既然这样，就设置子页面document.domain一直与父页面相同，但问题又来了：
测试3（异常）：父子页面同域，显示设置子页面内domain等于父页document.domain，但是不设置父页document.domain（默认为www.67ge.com）,

    document.write("<iframe id=\"ifr2\" src=\"javascript:void((function(){
        var d=document;
        d.open();
        d.domain='"+document.domain+"';
        d.write('');d.close()
    })())\"></iframe>");
    ifr = document.getElementById("ifr2");
    //使用setTimeout让iframe准备完成
    setTimeout(function(){
        try{
            ifr.contentWindow.document.write("success!");
        }catch(e){
            alert("test2:"+e.message); //弹出“拒绝访问
        }
    },0);
因为父页没定义document.domain，而子页面却定义了，虽然这时父子页面的document.domain是全等于的，但在IE下仍然拒绝访问。
解决办法就是父页也显示设置document.domain，让父子页面始终都有相同值的document.domain。
但是有些情况下是不能这么要求的，那现在我们不管父页面有没有设置document.domain来解决这个问题，矛盾就在于：

不能无条件的将iframe的domain设置为与父页相同；
无法使用“if(document.domain != location.hostname)”判断出父页是否显示的设置了document.domain。
我的解决办法是使用try...catch...

    document.write("<iframe id=\"ifr\"></iframe>");
    setTimeout(function(){
        try{
            //正常情况
            document.getElementById("ifr").contentWindow.document.write("success!");
        }catch(e){
            document.body.removeChild(document.getElementById("ifr"));
            //再创建一个设置domain的iframe
            var ifr = document.createElement("iframe");
            ifr.id="ifr";
            ifr.src="javascript:void((function(){var d=document;d.open();d.domain='"+
                document.domain + "';d.write('');d.close()})())";
            document.body.appendChild(ifr);
            setTimeout(function(){
                //给dom30毫秒的准备时间
                document.getElementById("ifr").contentWindow.
                    document.write("success!");
            },30);
        }
    },0)