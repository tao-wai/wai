#### 1.1.2图片链接无目的文本
![](/2.png)<br/>
图2　 图片链接无目的文本【示例】<br/>
【问题描述】<br/>
　　链接的目的文本用以说明链接的目的导向。用户通过屏幕阅读器获取链接的目的文本，从而了解链接作用。<br/>
【可能原因】<br/>
【修改建议】<br/>
样例1：<br/>
图片链接，图片无意义，可为img元素添加alt属性来描述链接目的：<br/>
```
<a href="routes.html"> <img src="topo.gif"
alt="去到无障碍论坛的路线" /></a>```

样例2：<br/>
图片和文字链接，图片无意义：<br/>
```
<a href="routes.html">
<img src="topo.gif" alt="" />去到无障碍论坛的路线
</a>```

样例3：<br/>
图片和文字链接，图片有意义：<br/>
```
<a href="prod_123_feedback.htm">反馈
<img src="response.gif" width="15" height="15" 、
alt="收到响应图标" />
</a>```
