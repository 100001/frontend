移动web开发过程中，手机连接 PC启动的wifi后，通过设置手机端代理IP（PC的IP）和端口（fiddler监听的8888）后，可以通过fiddler抓包。但是，通过手机上的chrome访问网页，却抓不到对应网页的包，仔细查看fiddler记录发现很多类似下面这个包：

>http://r9---sn-nx57yn7r.c.pack.google.com/crx/blobs/QwAAAHF3InbmK-wFIemaY3I3BCMqOfjjbz3ZPr0OdvcXp8cUu10k48t_h-qsRfYvKPciETPh6ZMAQTV8WL-Rx-lfADpBbs0T0xmHzDv3tYNK4R4eAMZSmuX1YAUWVQlL6kSI-xpS-vSmdvbuQg/extension_0_1_0_12919.crx?cms_redirect=yes&expire=1400936836&ip=222.129.235.70&ipbits=0&ms=au&mt=1400922344&mv=m&mws=yes&sparams=expire,ip,ipbits&signature=16271A0E4783850E7879CB03D9B8E6C6A3539F23.0CFF19C66574A651CCCDA80AEC329CB5614B1D79&key=cms1

原来，在chrome-->设置-->带宽管理-->减少流量消耗  的设置项，这个项是开启的情况下，所有chrome的请求会发送到Google服务器对其进行压缩后再响应给用户，所以抓的包就如上例所见。只需要把该项关闭，就可以通过fiddler抓到正常的包了