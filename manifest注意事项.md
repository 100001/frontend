1. 通过修改注释 触发 applicationCache 的 updateready 事件
2. manifest需要把页面中所有资源都列出来。不在列表中的资源会请求失败！需要每次请求的资源放在NETWORK下
3. 清除manifest文件的缓存，需要给manifest文件改个名。