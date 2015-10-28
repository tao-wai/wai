#### 2.2.2不能屏蔽底层的焦点
![](/19.png)<br/>
图19 不能屏蔽底层的焦点【示例】<br/>
【问题描述】<br/>
当浮层弹出后用单指在界面上滑动浏览， 朗读的是浮层底的控件没有朗读浮层内的控件；<br/>
【可能原因】<br/>
【修改建议】<br/>
android：<br/>
 给PopupWindow设置焦点：<br/>
方法1： PopupWindow初始化的时候第四个参数设置为true<br/>
方法2： 用setFocusable()函数设置PopupWindow获得焦点， 参数是true是获得焦点，参数是false是不获得焦点。<br/>
