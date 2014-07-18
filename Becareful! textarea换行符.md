程序中，换行符通常是指 \r\n ， \r 代表回车， \n 代表换行。
不过，在 html 的 textarea 中输入回车换行后，通过 textarea.value 获取的换行符只有 \n 一个字符。
例如： 

    var str = 'aa\r\nbb';
    console.log(val.length);// 6
    textarea.value = str;
    console.log(textarea.value.length);// 5
    console.log(textarea.value.indexOf('\n'));// 2
    console.log(textarea.value.indexOf('\r\n'));// -1

从执行结果可以看出，回车换行被删减为 换行 \n 。

但是呢，如果页面是通过 form submit 数据到服务端，这时服务端获取到的textarea中的换行符就是 \r\n  两个字符。
以下是通过fiddler 抓包 form 中 textarea 对应的字段：

![](http://s2.sinaimg.cn/mw690/001YiQ09ty6FgVKujmN21&690)

这其中的

![](http://s13.sinaimg.cn/mw690/001YiQ09ty6FgVc2uRu7c&690)

对应的字符就是 \r\n 。

所以，开发过程中，在对textarea的输入值做字符数限制的时候，前后端需要考虑好用哪种形式提交数据。