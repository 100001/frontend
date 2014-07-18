1.查看iframe readyState状态：

    (iframe.contentDocument || iframe.contentWindow.document).readyState;

2.通过js在页面中插入iframe后，如果打算在iframe中写入（wirte）新的DOM，需要在iframe的on1oad事件后或者iframe 的 readyState 为 complete 状态后才能操作，不然当 iframe on1oad后，之前写入（wirte）新的DOM会被重置。换句话说，iframe 的readyState 为 complete 前 与 后iframe 的document对象被重置了。

3.页面中的iframe不能用document.write写入html，这样浏览器tab页会不停的loading。