IE8下a标签innerHTML内有"xxx@xxx"字符串时（x可替换）,再设置a标签href属性时，a标签显示href属性内容（实际应该显示 "xxx@xxx" ）。

解决方案
1.设置href属性时，开头加个空格。
2.给a标签innerHTML赋值时，把字符串内容外套一个span标签。
3.先设置href属性，再改变innerHTML。