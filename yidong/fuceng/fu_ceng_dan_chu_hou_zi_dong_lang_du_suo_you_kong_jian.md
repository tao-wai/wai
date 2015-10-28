#### 浮层弹出后自动朗读所有控件
![](/21.png)<br/>
图21 浮层弹出后自动朗读所有控件【示例】<br/>
【问题描述】<br/>
浮层弹出后会自动把浮层内的所有元素按顺序朗读一遍；<br/>
【可能原因】<br/>
没有给PopupWindow设置背景；<br/>
【修改建议】<br/>
android：<br/>
使用setBackgroundDrawable（）函数设置背景，为了不改变视觉效果可以使用下面的两种方式：<br/>
setBackgroundDrawable(new BitmapDrawable());<br/>
setBackgroundDrawable(new ColorDrawable(0x00000000))。<br/>

