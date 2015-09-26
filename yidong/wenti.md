
# （三）移动端常见无障碍问题



## 1.常见控件的无障碍问题



## 1.1按钮/图形按钮


### 1.1.1按钮无焦点

【问题描述】<br/>
按钮无法滑动和触摸浏览， 或者按钮只能触摸浏览；<br/>
【可能原因】<br/>
1.没有给标准控件按钮设置焦点；<br/>
2.自定义的按钮没有支持无障碍访问；<br/>
【修改建议】<br/>
android：<br/>
方案1： <br/>
在布局xml文件中设置；<br/>
在布局xml文件中把控件的android：focusable属性设置为true， 此控件就能获得焦点。<br/>
方案2： <br/>
在java代码中设置；<br/>
在java代码中调用需要设置焦点的控件的setfocusable（）函数， 参数为true是获得焦点， 参数为false是不获得焦点；<br/>
方案3：<br/>
让自定义的按钮控件支持无障碍访问， 主要也是设置android：focusable的值<br/>
ios：<br/>
让自定义的按钮支持无障碍使用：<br/>
（注： 下面的文字摘抄与《ios-accessibility-programming-guide-in-chinese》）<br/>
除了使用 Interface Builder，还可以通过两种编程方法让自定义独立视图支持无障碍使用。第一种方法是在初始化视图的时候设置它的无障碍状态。如下面的代码片段所示： <br/>
```
@implementation MyCustomViewController 
-(id)init 
{ 
_view = [[[MyCustomView alloc] initWithFrame:CGRectZero] 
autorelease]; 
[_view setIsAccessibilityElement:YES]; 
/* Set attributes here. */ 
}```
　　另一种方法是实现UIAccessibility协议的isAccessibilityElement方法。如下面的代码片段所示： <br/>
```
@implementation MyCustomView 
/* Implement attribute methods here. */ 
-(BOOL)isAccessibilityElement 
{ 
return YES; 
}```
　　注意：在这两个代码片段中，都是用注释来代替真实的代码。

### 1.1.2按钮无提示文本、目的文本


【问题描述】<br/>
当按钮获得焦点的时候按钮不朗读或者朗读无意义；<br/>
【可能原因】<br/>
1.没有给按钮添加文本；<br/>
2.没有给图形按钮添加替代文本；<br/><br/>
【修改建议】<br/>
android：<br/>
方案1：<br/>
给按钮添加文本；<br/>
(1)在xml布局文件中添加文本；<br/>
```<Button android:layout_width="wrap_content" android:layout_height="wrap_content" android:text="确定"/>```<br/>
(2)在java代码中添加文本；<br/>
```Button button = (Button) findViewById(button);
button.setText("确定");```<br/>
方案2： <br/>
给图形按钮等没有文字的按钮添加替代文本；<br/>
(1)在xml布局文件中设置替代文本， 此种方法试用与此按钮在运行过程中功能不会改变
把按钮的contentdescription属性设置为适当的值, 例如，下面的ImageButton设置的add_note字符串资源，可以作为一个中文界面的“添加注释”定义为加号按钮，代码内容描述： <br/>
```<ImageButton
android:id=”@+id/add_note_button”
android:src=”@drawable/add_note”
android:contentDescription=”@string/add_note" />```
<br/>
(2) 用java代码设置替代文本，此种方法适用于按钮在运行中功能会改变或开关状态等播放按钮在歌曲没有播放的时候功能是播放歌曲，图标也是播放的图标， 可以这样设置替代文本：<br/>
button.setContentDescription("播放");<br/>
当歌曲播放的时候按钮的功能是暂停， 图标变成了暂停的图标， 可以这样设置替代文本：<br/>
button.setContentDescription("暂停");<br/>
ios：<br/>
所有的控件的标签属性都赋予适当的值， 有必要的时候给提示属性赋值。<br/>


### 1.1.3按钮不可操作


【问题描述】<br/>
在开着屏幕阅读器的情况下， 按钮点击后没有响应；<br/>
【可能原因】<br/>
自定义按钮没有处理定向控制器的点击事件；<br/>
【修改建议】<br/>
在多数的设备,单击视图利用定向控制器发送一个带有KEYCODE_DPAD_CENTER的按键事件到当前具有焦点的视图。所有标准的Android的视图已经适当地处理KEYCODE_DPAD_CENTER。当构建一个定制的视图控件,确保这个事件的产生的效果跟触摸触摸屏上的视图的效果一样。你的自定义控件处理 KEYCODE_ENTER事件时应该和处理 KEYCODE_DPAD_CENTER一样。这种方法更便于与一个使用全键盘的用户进行交互操作。 <br/>

### 1.1.4控件类型朗读不正确


【问题描述】<br/>
自定义的按钮不朗读控件类型或者朗读错误；<br/>
【可能原因】<br/>
自定义按钮的无障碍支持不够全面；<br/>
【修改建议】<br/>
android：<br/>
在任何一种情况下,为您的自定义视图类您应该执行下面的可访问性方法： <br/>
```dispatchPopulateAccessibilityEvent() 
    onPopulateAccessibilityEvent() 
    onInitializeAccessibilityEvent() 
    onInitializeAccessibilityNodeInfo() ```
通常是在onInitializeAccessibilityEvent()方法中提供类名（控件类型）；


## 1.2复选框



### 1.2.1复选框无焦点


【问题描述】<br/>
复选框无法滑动和触摸浏览，或者复选框只能触摸浏览；<br/>
【可能原因】<br/>
1.没有给标准控件复选框设置焦点；<br/>
2.自定义的复选框没有支持无障碍访问；<br/>
【修改建议】<br/>
android：<br/>
方案1：<br/>
在布局xml文件中设置；<br/>
在布局xml文件中把控件的android：focusable属性设置为true；<br/>
方案2： <br/>
在java代码中设置；<br/>
在java代码中调用需要设置焦点的控件的setfocusable（）函数，参数为true是获得焦点， 参数为false是不获得焦点；<br/>
方案3： <br/>
让自定义的复选框控件支持无障碍访问；<br/>
ios：<br/>
让自定义的复选框支持无障碍使用；
（注： 下面的文字摘抄与《ios-accessibility-programming-guide-in-chinese》）<br/>
除了使用 Interface Builder，还可以通过两种编程方法让自定义独立视图支持无障碍使用。第一种方法是在初始化视图的时候；设置它的无障碍状态。如下面的代码片段所示；<br/>
```
@implementation MyCustomViewController 
-(id)init 
{ 
_view = [[[MyCustomView alloc] initWithFrame:CGRectZero] 
autorelease]; 
[_view setIsAccessibilityElement:YES]; 
/* Set attributes here. */ 
}```
　　另一种方法是实现 ：UIAccessibility协议的isAccessibilityElement方法。如下面的代码片段所示： 
```
@implementation MyCustomView 
/* Implement attribute methods here. */
-(BOOL)isAccessibilityElement 
{
return YES; 
}```
注意：在这两个代码片段中，都是用注释来代替真实的代码；

### 1.2.2复选框无法操作


【问题描述】<br/>
在屏幕阅读器开着的情况下点击复选框无法改变复选框的状态；<br/>
【可能原因】<br/>
自定义复选框没有处理定向控制器的点击事件；<br/>
【修改建议】<br/>
　　在多数的设备,单击视图利用定向控制器发送一个带有KEYCODE_DPAD_CENTER的按键事件到当前具有焦点的视图。所有标准的Android的视图已经适当地处理KEYCODE_DPAD_CENTER。当构建一个定制的视图控件,确保这个事件的产生的效果跟触摸触摸屏上的视图的效果一样。你的自定义控件处理 KEYCODE_ENTER事件时应该和处理KEYCODE_DPAD_CENTER一样。这种方法更便于与一个使用全键盘的用户进行交互操作。 <br/>
<br/>
### 1.2.3复选框没有标签

【问题描述】<br/>
复选框没有提示文本， 不知道此复选框是选择什么的；<br/>
【可能原因】<br/>
1.复选框没有给标签赋值；<br/>
2.复选框的图形没有替代文本；<br/>
3.自定义的复选框的文本无法被屏幕阅读器识别；<br/>
【修改建议】<br/>
1.给复选框的标签赋予适当的值；<br/>
2.给复选框添加contentdescription属性并赋予适当的值；<br/>
3.在任何一种情况下,为您的自定义视图类您应该执行下面的可访问性方法： （android)
```
dispatchPopulateAccessibilityEvent()
onPopulateAccessibilityEvent() 
onInitializeAccessibilityEvent()
onInitializeAccessibilityNodeInfo() ```
　　使用onPopulateAccessibilityEvent()函数输出accessibilityEvent的文本；<br/>
　　注意:在该方法中修改文本之外的附加属性可能会以其他方式覆盖属性的设置。所以,虽然你可以使用此方法修改可访问性事件的属性,但您应该只限制这些更改只作用于文本内容和仅使用由onInitializeAccessibilityEvent()方法来修改事件的其他属性。<br/>
```
@Override
public void onPopulateAccessibilityEvent(View host, 
AccessibilityEvent event) {
    super.onPopulateAccessibilityEvent(host, event);
    // We call the super implementation to populate its text fo
    the
    // event. Then we add our text not present in a super class.
    // Very often you only need to add the text for the custom 
    view.
    CharSequence text = getText();
    if (!TextUtils.isEmpty(text)) {
        event.getText().add(text);
    }
}```

### 1.2.4聚焦时，不朗读选中状态

【问题描述】<br/>
复选框聚焦的时候无法正确朗读出当前选中状态；<br/>
【可能原因】<br/>
自定义的复选框对无障碍支持不全面；<br/>
【修改建议】<br/>
android：<br/>
在任何一种情况下,为您的自定义视图类您应该执行下面的可访问性方法：<br/>
```
dispatchPopulateAccessibilityEvent()
onPopulateAccessibilityEvent() 
onInitializeAccessibilityEvent()
onInitializeAccessibilityNodeInfo() ```
　　利用onInitializeAccessibilityEvent() 修改状态属性<br/>
```
@Override
public void onInitializeAccessibilityEvent(View host, 
AccessibilityEvent event) {
    super.onInitializeAccessibilityEvent(host, event);
    // We call the super implementation to let super classes
    // set appropriate event properties. Then we add the new 
    property
    // (checked) which is not supported by a super class.
    event.setChecked(isChecked());
}```

### 1.2.5改变状态后，焦点未在当前控件
【问题描述】<br/>
复选框改变其选中状态后，聚焦的控件不是此复选框了，而是变成了其他控件，焦点不在当前控件；<br/>
【可能原因】<br/>
【修改建议】<br/>

### 1.2.6改变选中状态，不能及时朗读状态


    【问题描述】
    点击一个复选框改变其当前选中状态后不能马上提示出改变后的状态；
    【可能原因】
    自定义复选框对无障碍支持不够全面；
    【修改建议】
    android：
    当自定义的复选框的状态改变后用sendAccessibilityEvent()发送可访问性事件， 参数通常为type_view_checked，并重写相应的可访问性事件.

### 1.2.7控件类型朗读不正确


    【问题描述】
    自定义复选框的类型不朗读或朗读不正确；
    【可能原因】
    自定义复选框的无障碍支持不够全面；
    【修改建议】
    android：
    在任何一种情况下,为您的自定义视图类您应该执行下面的可访问性方法： 
```
dispatchPopulateAccessibilityEvent() 
onPopulateAccessibilityEvent() 
onInitializeAccessibilityEvent() 
onInitializeAccessibilityNodeInfo() ```
    通常是在onInitializeAccessibilityEvent()方法中提供类名（控件类型）。

## 1.3单选框


### 1.3.1单选框无焦点


    【问题描述】
    触摸和滑动都找不到该单选框。
    【可能原因】
    【修改建议】

### 1.3.2双击无法改变当前状态


    【问题描述】
    双击该单选框，无法改变单选框的选中状态。
    【可能原因】
    【修改建议】

### 1.3.3单选框没有标签


    【问题描述】
    触摸到该单选框，不会正确朗读出这是什么单选框，因为这个单选框没有标签。
    【可能原因】
    【修改建议】

### 1.3.4聚焦时，不朗读选中状态


    【问题描述】
    触摸或滑动到单选框，没有办法及时朗读单选框的选中状态，要状态改变后，才能朗读单选框的选中状态。
    【可能原因】
    【修改建议】

### 1.3.5改变状态后，焦点未在当前控件


    【问题描述】
    单选框状态改变后，焦点没有停留到单选框上，可能会跑焦点。
    【可能原因】
    【修改建议】
   
###  1.3.6改变选中状态，不能及时朗读状态


    【问题描述】
    双击单选框改变状态的时候，不会及时朗读出单选框的选中状态。
    【可能原因】
    【修改建议】

### 1.3.7控件类型朗读不正确


    【问题描述】
    触摸或滑动到单选框，控件类型朗读错误，可能朗读成复选框或按钮等。
    【可能原因】
    【修改建议】

## 1.4编辑框



### 1.4.1双击无法弹出键盘


    【问题描述】
    双击该编辑框，输入法键盘无法自动弹出。
    【可能原因】
    【修改建议】

### 1.4.2无正确文本提示

    【问题描述】
    触摸到该编辑框，没有提示这是什么编辑框；
    【可能原因】
    编辑框没有label；
    【修改建议】
    可以给编辑框增加label。

### 1.4.3输入字符无法删


    【问题描述】
    在该编辑框输入好文字后，不能删除已输入的文字。
    【可能原因】
    【修改建议】

### 1.4.4输入字符不朗读


    【问题描述】
    在该编辑框上输入文字，不会朗读输入的是什么东西。
    【可能原因】
    【修改建议】

### 1.4.5输入光标无法移动


    【问题描述】
    在该编辑框下，光标不能动，导致不能在编辑框中移动。
    【可能原因】
    【修改建议】

### 1.4.6移动编辑光标所在字朗读错误


    【问题描述】
    在该编辑框下，移动光标，朗读的不是光标停留所在的字符。
    【可能原因】
    【修改建议】

### 1.4.7控件类型朗读不正确


    【问题描述】
    滑动或触摸找到编辑框后，控件类型朗读错误，例如朗读成组合框。
    【可能原因】
    【修改建议】

## 1.5 Tableview（ios）



### 1.5.1双击左滑无法弹出


    【问题描述】
    双击左滑后，无法弹出Tableview；
    【可能原因】
    【修改建议】

### 1.5.2弹出菜单后，删除以外的无法使用标准手势


    【问题描述】
    除了删除以外，其他都无法使用转子。
    【可能原因】
    【修改建议】

### 1.5.3双击后执行与描述不符


    【问题描述】
    例如找到删除，双击以后，却点的是其他东西；
    【可能原因】
    【修改建议】


## 1.6滑块



### 1.6.1标签错误，标签不朗读


    【问题描述】
    焦点聚焦当前滑块时，无法朗读出滑块的名称；
    【可能原因】
    ios，未给控件添加适当的label信息；
    android，未给设备添加适当的android:contentDescription信息；
    【修改建议】

### 1.6.2控件类型朗读不正确


    【问题描述】
    聚焦该控件后无法正确朗读出控件的类型；
    【可能原因】
    当该控件属于自定义控件时，未提供其到标准控件的名称映射，导致聚焦后无法正确朗读控件的类型；
    【修改建议】

### 1.6.3改变百分比不能及时朗读

    【问题描述】
    当利用手势对滑块进行调整时，无法及时朗读出当时所调整的数值；
    【可能原因】
    【修改建议】

## 1.7翻页控件（ios）



### 1.7.1翻页控件不可聚焦


    【问题描述】
    触摸翻页控件时，导致焦点无法focus到该控件；
    【可能原因】
    【修改建议】

## 1.7.2不支持标准手势


    【问题描述】
    这里的标准手势指的是单指上下扫动可调整翻页控件。具体操作方式如下，触摸该控件后，单指上下扫动，可调整该翻页控件。
    【可能原因】
    【修改建议】

## 1.7.3翻页控件朗读不正确


    
    【问题描述】
    触摸该翻页控件后，焦点可顺利聚焦，但无法正确朗读出该控件；
    【可能原因】
    【修改建议】



## 1.8项目选择器（ios）


    该问题主要出现在android平台，以下序数内容以android平台为准：

### 1.8.1加减控件无法朗读

    
    【问题描述】
    触摸该控件，焦点可顺利聚焦，但语音无法朗读；
    【可能原因】
    【修改建议】

### 1.8.2双指无法滚动


    【问题描述】
    通常情况下，希望支持双指手势来调节该控件；
    【可能原因】
    【修改建议】

## 1.9列表



### 1.9.1列表不支持手势翻页



    【问题描述】
    通常情况下，一个包含众多元素的列表应能支持辅助功能手势的翻页，android的手势为双指上下滑动，ios的手势为三指上下滑动；
    【可能原因】
    【修改建议】



### 1.9.2一个焦点覆盖所有的子项目


    【问题描述】
    触摸列表中的任意项目，均无法聚焦，焦点只能聚焦整个列表；
    【可能原因】
    【修改建议】

### 1.9.3子项目无焦点


    【问题描述】
    列表内的一个或多个项目无焦点；
    【可能原因】
    【修改建议】

### 1.9.4列表项没有名称


    【问题描述】
    列表内项目有焦点，但无法正确朗读；
    【可能原因】
    【修改建议】

## 1.10组合框



### 1.10.1焦点无法进入组合框


    【问题描述】
    触摸组合框，焦点无法聚焦；
    【可能原因】
    【修改建议】

### 1.10.2已选中项未提示选中状态


    【问题描述】
    触摸该组合框，应可朗读出名称、类型及当前所选中的元素；
    【可能原因】
    【修改建议】

### 1.10.3下拉列表项目提示不正确


    【问题描述】
    触摸下拉列表内的任意项目，均无法正确朗读；
    【可能原因】
    【修改建议】

### 1.10.4控件类型朗读不正确


    【问题描述】
    触摸组合框，可成功聚焦，但没有朗读正确控件类型；
    【可能原因】
    【修改建议】

## 1.11树视图



### 1.11.1展开折叠状态无提示


    【问题描述】
    双击树视图某项目，不朗读展开还是折叠。
    【可能原因】
    【修改建议】

### 1.11.2树视图无焦点


    【问题描述】
    触摸和滑动都找不到树视图，树视图没有焦点。
    【可能原因】
    【修改建议】

### 1.11.3树视图无法朗读


    【问题描述】
    滑动焦点停留在树视图，无法朗读树视图的名字和项目。
    【可能原因】
    【修改建议】

### 1.11.4展开折叠状态改变后，无法及时朗读状态


    【问题描述】
    当树视图状态改变后，焦点停留到树视图项目上，无法朗读状态，要双击重新改变状态，才会朗读。
    【可能原因】
    【修改建议】

### 1.11.5控件类型朗读不正确


    【问题描述】
    树视图控件朗读不正确，可能会朗读成列表或其他控件类型。
    【可能原因】
    【修改建议】

## 1.12 tab标签


### 1.12.1选中状态不朗读


    【问题描述】
    当滑动或触摸浏览到tab标签后无法朗读出此tab标签是否选中；
    【可能原因】
    自定义控件的无障碍支持不够全面；
    【修改建议】
    android：
    在任何一种情况下，为您的自定义视图类您应该执行下面的可访问性方法： 
```
dispatchPopulateAccessibilityEvent()
onPopulateAccessibilityEvent() 
onInitializeAccessibilityEvent()
onInitializeAccessibilityNodeInfo() ```
通常是在onInitializeAccessibilityEvent() 方法中修改控件的状态。

### 1.12.2Tab标签名称不朗读


    【问题描述】
    触摸或滑动到tab卡下的tab标签， tab标签的名称不能朗读出；
    【可能原因】
    1、 没有给标签赋值；
    2、 tab标签的图形没有替代文本；
    【修改建议】
    1、 给tab标签赋予适当的值；
    2、 给tab标签添加contentDescription属性并赋予适当的值。

# 2.常见功能的无障碍问题



## 2.1焦点



### 2.1.1一个焦点覆盖到多个元素


    【问题描述】
    一个焦点覆盖多个元素， 当触摸或滑动到这个焦点的时候会把这个焦点覆盖的所有元素朗读出来， 触摸到这个界面的空白部分也朗读这个覆盖多个元素的焦点。
    【可能原因】
    【修改建议】

### 2.1.2焦点区域大小不适当


    【问题描述】
    焦点区域过大或者过小， 影响低视力的人群获取界面信息。 焦点区域过小是指焦点区域小鱼展示的内容， 例如： 一个textview上的文字高25dip、宽20dip， 儿焦点区域才高12dip，宽10dip。 焦点区域过大是焦点区域大于展示的内容。
    【可能原因】
    【修改建议】

### 2.1.3焦点顺序不符合逻辑


    【问题描述】
    在界面上滑动浏览时，对象获得焦点的顺序与实际显示的顺序不一致， 例如界面上从左到右依次有一个编辑框、一个确定按钮、一个取消按钮， 当焦点在编辑框上时向右滑动一次取消按钮获得焦点就是不符合实际的逻辑顺序， 正确的焦点顺序应该是： 当编辑框聚焦的时候向右滑动一次是确定按钮聚焦，再向右滑动一次取消按钮聚焦。
    【可能原因】
    android:
    1、 在布局xml文件中配置的焦点顺序出错；
    2、 在java代码中设置焦点顺序时出错；
    【修改建议】
    android：
    1、 在xml布局文件中用nextFocusDown(向下的下一个焦点）、nextFocusRight(向右的下一个焦点)、nextFocusLeft(向左的下一个焦点)、nextFocusUp(向上的下一个焦点)这四个属性来设置控件的焦点顺序
    2、 在java代码中可以用setNextFocusDown(向下的下一个焦点)、setNextFocusUp(向上的下一个焦点)、setNextFocusRight(向右的下一个焦点)、setNextFocusLeft(向左的下一个焦点)这四个函数来设置控件的焦点顺序

### 2.1.4部分控件无焦点


    【问题描述】
    控件无法滑动和触摸浏览， 或者控件只能触摸浏览；
    【可能原因】
    1、 没有给标准控件设置焦点；
    2、 自定义的控件没有支持无障碍访问；
    【修改建议】
    android：
    方案1： 在布局xml文件中设置；
    在布局xml文件中把控件的android：focusable属性设置为true
    方案2： 在java代码中设置；
    在java代码中调用需要设置焦点的控件的setfocusable（）函数， 参数为true是获得焦点， 参数为false是不获得焦点
    方案3： 让自定义的控件支持无障碍访问；
    ios：
    让自定义的控件支持无障碍使用
    （注： 下面的文字摘抄与《ios-accessibility-programming-guide-in-chinese》）
    除了使用 Interface Builder，还可以通过两种编程方法让自定义独立视图支持无障碍使用。第一种方法是在初始化视图的时候
    设置它的无障碍状态。如下面的代码片段所示： 
```
@implementation MyCustomViewController 
-(id)init 
{ 
_view = [[[MyCustomView alloc] initWithFrame:CGRectZero] autorelease]; 
[_view setIsAccessibilityElement:YES]; 
/* Set attributes here. */ 
}```

    另一种方法是实现 UIAccessibility协议的isAccessibilityElement方法。如下面的代码片段所示： 
```
@implementation MyCustomView 
/* Implement attribute methods here. */ 
-(BOOL)isAccessibilityElement 
{ 
return YES; 
}```
    注意：在这两个代码片段中，都是用注释来代替真实的代码

### 2.1.5定时刷新导致焦点丢失

    
    【问题描述】
    界面的局部或者整体定时进行刷新， 界面刷新之后焦点离开了刷新之前的位置， 刷新频率不快的时候会影响用户的使用效率。 刷新频率快的时候会导致用户无法正常操作此界面刷新区域的元素。
    【可能原因】
    【修改建议】

### 2.1.6焦点响应错乱


    【问题描述】
    滑动或触摸浏览到一个焦点后点击， 点击后响应的结果与此焦点的提示文本所描述的目的不相符。
    【可能原因】
    1、 控件的定向处理事件代码链接错误；
    如访问官网的事件处理程序的代码链接到意见反馈。
    【修改建议】

## 2.2浮窗



### 2.2.1浮窗不能滑动浏览


    【问题描述】
    当一个浮窗弹出后，不能滑动浏览进入浮窗内； 在浮窗内不能滑动浏览浮窗内的控件；
    【可能原因】
    2、 PopupWindow内的控件没有设置焦点；
    1、 PopupWindow没有获得焦点；
    【修改建议】
    android：
    1、 把PopupWindow内的所有控件设置焦点；
    2、 给PopupWindow设置焦点；
    方法1： PopupWindow初始化的时候第四个参数设置为true；
    方法2： 用setFocusable()函数设置PopupWindow获得焦点， 参数是true是获得焦点，参数是false是不获得焦点。

### 2.2.2不能屏蔽底层的焦点


    【问题描述】
    当浮窗弹出后用单指在界面上滑动浏览， 朗读的是浮窗底的控件没有朗读浮窗内的控件；
    【修改建议】
    android：
     给PopupWindow设置焦点：
    方法1： PopupWindow初始化的时候第四个参数设置为true
    方法2： 用setFocusable()函数设置PopupWindow获得焦点， 参数是true是获得焦点，参数是false是不获得焦点。

### 2.2.3浮窗无法关闭


    【问题描述】
    在屏幕阅读器开启的情况下， 浮窗弹出后， 没有提供任何一种方式关闭浮窗。
    【可能原因】
    【修改建议】

### 2.2.4浮窗弹出后自动朗读所有控件


    【问题描述】
    浮窗弹出后会自动把浮窗内的所有元素按顺序朗读一遍；
    【可能原因】
    没有给PopupWindow设置背景；
    【修改建议】
    android：
    使用setBackgroundDrawable（）函数设置背景， 为了不改变视觉效果可以使用下面的两种方式：
    setBackgroundDrawable(new BitmapDrawable());
    setBackgroundDrawab
    
    
    ew ColorDrawable(0x00000000))。

## 2.3提示文本



### 2.3.1控件类型不能正常朗读


    【问题描述】
    控件的类型不提示或者控件类型提示不正确， 用户不知道如何操作此控件， 这种情况主要出现在自定义控件上；
    【可能原因】
    自定义控件的无障碍支持不全面；
    【修改建议】
    android：
    在任何一种情况下,为您的自定义视图类您应该执行下面的可访问性方法： 
    dispatchPopulateAccessibilityEvent() 
    onPopulateAccessibilityEvent() onInitializeAccessib

### 2.3.2提示文本有冗余信息、 提示文本错误ityEvent() 


    onInitializeAccessibilityNodeInfo() 
    通常是在onInitializeAccessibilityEvent() 方法中提供类名（控件类型）。

### 2.3.2提示文本有冗余信息、 提示文本错误


    【问题描述】
    控件的提示文本有冗余； 控件的提示文本与控件的实际目的不相符；
    【可能原因】
    1.给控件提供提示文本或替代文本时文本不够精炼准；
    2.提供了一些不必要的信；
    【修改建议】
    1给控件提供文本或者替代文本时要精炼准确；
    2去掉这些不必要的信息。