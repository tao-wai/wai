
####控件类型不能正常朗读

![](/24.png)<br/>
图24 空间类型不能正常朗读【示例】<br/>
【问题描述】<br/>
控件的类型不提示或者控件类型提示不正确， 用户不知道如何操作此控件， 这种情况主要出现在自定义控件上；<br/>
【可能原因】<br/>
自定义控件的无障碍支持不全面；<br/>
【修改建议】<br/>
android：<br/>
在任何一种情况下，为您的自定义视图类您应该执行下面的可访问性方法： <br/>

```
dispatchPopulateAccessibilityEvent() 
onPopulateAccessibilityEvent() 
onInitializeAccessibilityEvent() 
onInitializeAccessibilityNodeInfo()``` <br/>
通常是在onInitializeAccessibilityEvent() 方法中提供类名（控件类型）。<br/>

