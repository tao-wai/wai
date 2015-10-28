####部分控件无焦点
![](/16.png)<br/>
图16 部分控件无焦点【示例】<br/>
【问题描述】<br/>
控件无法滑动和触摸浏览， 或者控件只能触摸浏览；<br/>
【可能原因】<br/>
1、 没有给标准控件设置焦点；<br/>
2、 自定义的控件没有支持无障碍访问；<br/>
【修改建议】<br/>
android：<br/>
方案1： 在布局xml文件中设置；<br/>
在布局xml文件中把控件的android：focusable属性设置为true<br/>
方案2： 在java代码中设置；<br/>
在java代码中调用需要设置焦点的控件的setfocusable（）函数， 参数为true是获得焦点， 参数为false是不获得焦点;
方案3： 让自定义的控件支持无障碍访问；<br/>
ios：<br/>
让自定义的控件支持无障碍使用
（注： 下面的文字摘抄与《ios-accessibility-programming-guide-in-chinese》）
除了使用 Interface Builder，还可以通过两种编程方法让自定义独立视图支持无障碍使用。第一种方法是在初始化视图的时候
设置它的无障碍状态。如下面的代码片段所示：<br/>

```
@implementation MyCustomViewController
-(id)init
{
_view = [[[MyCustomView alloc] initWithFrame:CGRectZero] autorelease];
[_view setIsAccessibilityElement:YES];
/* Set attributes here. */
}```


另一种方法是实现
```
UIAccessibility协议的isAccessibilityElement方法。如下面的代码片段所示：<br/>
@implementation MyCustomView
/* Implement attribute methods here. */
-(BOOL)isAccessibilityElement
{
return YES;
}```

注意：在这两个代码片段中，都是用注释来代替真实的代码。<br/>
