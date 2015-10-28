#### 2.2.1浮层不能滑动浏览
![](/18.png)<br/>
图18 浮窗不能滑动浏览【示例】<br/>
【问题描述】<br/>
当一个浮层弹出后，不能滑动浏览进入浮层内； 在浮层内不能滑动浏览浮层内的控件；<br/>
【可能原因】<br/>
2、 PopupWindow内的控件没有设置焦点；<br/>
1、 PopupWindow没有获得焦点；<br/>
【修改建议】<br/>
android：<br/>
1、 把PopupWindow内的所有控件设置焦点；<br/>
2、 给PopupWindow设置焦点；<br/>
方法1： PopupWindow初始化的时候第四个参数设置为true；<br/>
方法2： 用setFocusable()函数设置PopupWindow获得焦点， 参数是true是获得焦点，参数是false是不获得焦点。<br/>

