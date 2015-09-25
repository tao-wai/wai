
# （二）Web端常见应用的无障碍问题


    该部分参考资料内容来自Web Content Accessibility Guidelines (WCAG)
2.0（http://www.w3.org/Translations/WCAG20-zh/）、How to Meet WCAG 2.0（http://www.w3.org/WAI/WCAG20/quickref/#qr-text-equiv-all）、WAI-ARIA 1.0 Authoring Practices（http://www.w3.org/TR/wai-aria-practices/）。

## 2.1日期控件



### 2.1.1日期控件无法聚焦


    【问题描述】
    自绘的日期控件无法用tab键浏览到；
    【可能原因】
    自绘日期控件没有添加tabindex属性；
    【修改建议】
    给自绘的日期控件添加tabindex="0"；

### 2.1.2日期控件无法用键盘选择日期


    【问题描述】
    自绘的日期控件弹出选择日期后，无法获得焦点，无法用键盘进行选择日期控件的日期；
    【可能原因】
    日期控件弹出选择日期后选择日期的部分没有自动聚焦； 没有对键盘选择日期做支持；
    【修改建议】

### 2.1.3日期控件键盘回车操作无响应


    【问题描述】
    当日期控件未展开的时候无法用enter键展开日期控件；   当日期控件展开时使用方向键在日期控件中移动，按“enter”无法把选中的信息送入编辑框。
    【可能原因】
    自绘的日期控件对enter键的支持不够全面；
    【修改建议】

### 2.1.4展开折叠状态无提示


    【问题描述】
    自绘的日期控件展开后没有展开折叠提示， 用户无法知道日期控件已经展开；
    【可能原因】
    没有任何一种提示方式让用户知道日期控件已经展开；
    【修改建议】
    当日期控件展开后展开的日期控件的第一个元素自动获得焦点， 这样用户就知道日期控件展开了。

### 2.1.5展开的日期控件的项目不能朗读

    
    【问题描述】
    当自绘的日期控件展开后上下光标在日期选项之间移动，但是日期选项不能被朗读出；
    【可能原因】
    【修改建议】

### 2.1.6日期选择后无法删除

    
    【问题描述】
    当使用日期控件把某个日期信息添加到编辑框后，焦点处于日期编辑框内无法按“backplace键”删除已经录入的日期信息。
    【可能原因】
    【修改建议】
  
##   参考资料


   
###  1.在某个UI元素内的键盘导航


    对于复合元素，确保在所包含的元素之间的内部导航正确，这一点很重要。对于复合元素，可以采用多种方式实现内部导航。
    复合元素可以管理其当前活动子元素以降低使所有子元素可聚焦的开销。采用 Tab 键顺序将这样的复合元素包括在内，且该元素会处理键盘导航事件。复合元素使用 aria-activedescendant 属性暴露有关当前活动子元素的信息。
    可以参看以下例子：
```
<!-- 自定义树视图元素。 -->
<div id="folders" class="tree" role="tree" aria-label="文件夹" tabindex="0"
        aria-activedescendant="n-0"><!--文件组-->
    <div id="n-0" class="selected" role="treeitem" aria-expanded="true" 
            onclick="alert('点击了库。');">
        库</div>
    <div role="group">
        <div id="n-0-1" role="treeitem" aria-expanded="false" onclick="alert('点击了无障碍文档。');">文档</div>
        <div id="n-0-2" role="treeitem" aria-expanded="false" onclick="alert('点击了无障碍音频');">音乐</div>
        <div id="n-0-3" role="treeitem" aria-expanded="false" onclick="alert('点击了无障碍图片。');">图片</div>
    </div>
</div>
<script>
    var folders = document.getElementById("forlders");
    // 确保使用方向键可进行键盘导航操作。
// 添加对keydown事件的监听
    folders.addEventListener('keydown', function(e) {
        var itm = e.srcElement; // 获取触发Keydown事件的元素对象。
        if (e.keyCode === Win.Utilities.Key.upArrow) // 当按下的键是上方向键
        {
            // 位上一个节点ID更新aria-activedescendant the previous node id.
            // 更新class属性来标记选中的元素节点。
        } else if (e.keyCode === Win.Utilities.Key.downArrow) // 当在元素上按下了下方向键
        {
            // Update aria-activedescendant with the next node id.
            // 通过class属性来标记选中的元素节点。
        }
    });
</script>```
    替代方法是动态管理节点的 tabindex属性。此方法以提供“漫游索引”而著称。
```
<!-- 自定义树视图元素。 -->
<div id="文件夹组" role="tree" aria-label="文件夹" >
<!--视图元素-->
    <div id="n-0" role="treeitem" aria-expanded="true（真）" tabindex="0">库</div>
    <div role="group" >
        <!-- Child tree items: Documents, Music, Pictures ... -->
        <div id="n-0-1" role="treeitem" aria-expanded="false" tabindex="-1">无障碍文档</div>
        <div id="n-0-2" role="treeitem" aria-expanded="false" tabindex="-1">无障碍音频</div>
        <div id="n-0-3" role="treeitem" aria-expanded="false" tabindex="-1">无障碍图片</div>
    </div>
</div>
<script>
    // 获取文件夹树视图元素节点对象。
    var folders = document.getElementById('文件组');
    // Ensure keyboard navigation/operation with arrow keys.
    folders.addEventListener('keydown', function(e) {
        var itm = e.srcElement;
        if (e.keyCode === Win.Utilities.Key.upArrow) {
            // Update tabindex attributes.
        } else if (e.keyCode === Win.Utilities.Key.downArrow) {
            // Update tabindex attributes.
        }
    });
</script>```
    如前面两个示例所示，建议将箭头键用作在子元素之间导航的键盘快捷方式。如果树状视图节点有单独的子元素，用于处理展开–折叠和节点激活，则应使用左右箭头键提供键盘展开–折叠功能。

### 2.为静态html元素添加键盘访问行为


    这个技巧是怎样给用户界面控件添加键盘可访问事件，这些控件是由静态HTML元素来实现的，如div或span。这个技巧通过设置tabindex属性保证元素是可聚焦的，并保证行为可以通过键盘触发，通过提供onkeyup或onkeypress处理器而不是onclick处理器。
    当tabindex属性值为0，元素是可以通过键盘聚焦，并且被包含在document中的tab顺序中。当tabindex属性值为-1时，tab不能tab进入，焦点也可以编程确定，使用element。Focus（）。
    因为静态html元素没有与他们相关联的行为，它不可能提供替代实现和在JS不能使用的环境下进行解释。该技术应可以以来JS脚本的客户端环境中使用。
    注意：使用这个技巧不要再使用role、name、状态信息；
    为div元素添加JS行为：
    网页上的div赋予一个唯一的ID属性，并将tabindex值设为0.脚本通过使用DOM通过id找到div元素，添加onclick处理器和onkeyup事件。Onkeyup事件响应enter点击。注意div元素必须被加载到DOM中才可以被找到和修改。这通常是通过body元素的onload事件调用脚本来实现的。用户代理支持且启用了JS脚本，加入事件处理器的脚本才能够执行。
```
...
<script type="text/javascript">
 // this is the function to perform the action. This simple example toggles a message.
 function doSomething(event) {
   var msg=document.getElementById("message");
   msg.style.display = msg.style.display=="none" ? "" : "none";
   //return false from the function to make certain that the href of the link does not get invoked
   return false;
 }
 // this is the function to perform the action when the Enter key has been pressed.  
 function doSomethingOnEnter(event) {
   var key = 0;
   // Determine the key pressed, depending on whether window.event or the event object is in use
   if (window.event) {
     key = window.event.keyCode;
   } else if (event) {
     key = event.keyCode;
   }
   // Was the Enter key pressed?
   if (key == 13) {
     return doSomething(event);
   } 
   // The event has not been handled, so return true
   return true;
 }
 // This setUpActions() function must be called to set the onclick and onkeyup event handlers onto the existing 
 // div element. This function must be called after the div element with id="active" has been loaded into the DOM.
 // In this example the setUpActions() function is called from the onload event for the body element.
 function setUpActions() {
   // get the div object
   var active=document.getElementById("active");
   // assign the onclick handler to the object.
   // It is important to return false from the onclick handler to prevent the href attribute
   // from being followed after the function returns.
   active.onclick=doSomething;
   // assign the onkeyup handler to the object.
   active.onkeyup=doSomethingOnEnter;
 }
 </script>

 <body onload="setUpActions();">
 <p>Here is the link to modify with a javascript action:</p>
 <div>
  <span id="active" tabindex="0">Do Something</span>
 </div>
 <div id="message">Hello, world!</div>```



## 2.2验证码



### 2.2.1感知方式只有一种，未提供多种反馈


    【问题描述】
    网站设计者只提供一种验证码方式。例如只有图形验证码，没有语音、短信等多种反馈；
    【可能原因】
    开发者不具备提供多种验证码的能力，或成本过高开发者放弃提供多种验证码校验方式；
    【修改建议】
    提供一种任何人群都可以使用的验证码类型， 或者使用多种验证码类型让任何人群都可以使用。

### 2.2.2无法用键盘输入验证码



    【问题描述】
    某些验证码为FLASH内容，无法用键盘输入，屏幕阅读器用户无法使用，例如：12306的登录验证码。
    【可能原因】
    【修改建议】

### 2.2.3无法感知验证码已刷新

    
    【问题描述】
    验证码自动刷新，当刷新验证码后，没有提供使多种人群可感知的方式提示验证码已经刷新；
    【可能原因】
    设置自动刷新验证码且只能从验证码图形的改变来感知验证码已经刷新；
    【修改建议】
    1、 提供手动刷新验证码的机制；
    2、 验证码刷新后提供多种感知方式让多种人群感知到验证码已经刷新。


## 参考资料



### Managing Dynamic Changes管理动态改变


    1.管理内容和显示改变
    管理内容和显示信息的一般规则：
    1）元素的role一旦被设置不要改变。如果要改变对象的role，首先应该将元素从DOM树删除，然后添加具有新role的元素到DOM树。
    2）为了支持浏览器，连接CSS属性选择器到wai-aria属性来降低脚本（浏览器刷新问题）
    3）连接CSS显示属性到wai-aria隐藏状态。这对于直接与用户代理DOM交流的辅助技术和用户歹意支持的平台无障碍API来说都很重要。也可以将CSS visibility:hidden 或者visibility:collapse连接到wai-aria隐藏状态，但是visibility:hidden的使用会影响内容的布局将继续流向访问内容，及时访问内容不可见。
    如果是异步刷新，需要指定实时区域，以下部分解释如何实现实时区域以及何时默认使用被认为“live”部分的role，包括警报、状态和登陆。
    2.实现实时区域
    实时区域是开发者希望网页内改变的内容。实时区域的样例包括动态刷新表格（体育统计、股票信息），新内容添加日志（聊天记录日志），通知区域（状态、警报）等等。
    实时区域激活辅助技术，比如读屏软件被通知更新，而不会丢失用户区域。实时区域设置提供hints给辅助技术怎样去处理刷新。需要注意的是辅助技术负责处理这些更新信息，并使用户获得这些提示。
    这节是关于实时区域属性和怎么使用这些属性来提供详细信息。这个过程将会帮助RIA开发者来设置实时区域设置，这些设置会为哪些具有少量配置的辅助技术用户提供更好的用户体验。当使用这些实时区域属性时，推荐只是用户测试。如果辅助技术支持实施区域的响应脚本，开发者可能会自定义响应，比如通过网页的屏幕阅读器。
    1）识别实时区域
    实时区域是通过客户端脚本动态更新的网页上的任何区域。注意网页上的实时区域；
    2）查看是否任何特殊情况实时区域都能满足需求
    wai-aria提供了很多特殊情况的实时区域role值，这些roles值的实时区域的属性是事先定义好的，且会被用到的。如果这些实时区域roles能够满足需求只需要在实时区域应用特定的role。
    3）决定每一个实时区域的优先级
    当实时区域改变，用户需要被告知改变吗？通知应该也包括读屏用户的声音反馈。改变的间隔越短，信息越不重要。用户需要去听到每个改变越不可能。一个简单的例子是时间改变不应该被听到，每一秒的声音将会很讨厌。
    如果用户应该听到改变，改变应该立即告知，越快越好，或者只有当用户空闲的时候才通知。立即告知改变会扰乱用户，应该尽量少做。大多数的更新可能在用户空闲的时候告知。
    决定每个实时区域的优先级之后，决定实时区域的属性值：
    从未说过话，那么aria-live=“off”
    当用户处于空闲状态，然后aria-live="polite"
    尽快讲什么，然后aria-live="assertive"
    欲了解更多细节，请参见实时区域属性。
    4）每个更新需要的文本多少
    当实时区域改变时，多少文本需要用来理解改变。用户是否需要听到整个实时区域，或者仅仅是改变自己？
    如果用户需要听到整个实时区域，使用aria-atomic="true"标记整个实时区域.
    5）决定什么类型的改变与实时区域相关
    三种改变类型是：附加、删除和文字。附加是新节点加入到DOM树中；删除是从DOM树中删除节点，文本是只与文本相关的改变。用户应该听到全部类型的改变还是一部分？
    用户默认可以听到附加和文本类型的改变。如果希望去详细的定义改变类型，需要去设置relevant="THE_TYPES_OF_CHANGES"。如果多种改变相关联，类型用空格隔开。例如，定义附加和删除相关但是没有文本，应该设置relevant="additions removals"。
    3.实时区域属性和怎样使用
    实施区域最重要的一个概念是礼貌（politeness）。礼貌指明了每个实时区域的优先级。使用aria-live来指明politeness的值有：off、polite、assertive。
    aria-live="off"
    这是默认属性。实时区域的任何改变都不必通知用户；live="off"应该是个明智的选择，当一个区域太频繁的刷新时，例如移动车辆的GPS坐标更新。
    aria-live="polite"
    实时区域的任何更新应该当用户空闲的时候通知用户。live="polite"应该用在大多数包含呈现信息的实时区域的时，比如更新新闻标题。
    aria-live="assertive"
    这个实时区域的任何更新都很重要，需要尽快告知用户，但是没有必要立即中断用户。live="assertive"必须用在用户必须马上知道信息的时候，例如，当飞行表单的警告信息。
    当一个区域更新时，辅助技术需要时间来呈现更新。因为这个需要使用aria-busy（状态）属性。
    aria-busy(state)="true"
    当实时区域停止更新或者一系列急速改变完成时呈现改变，设置aria-busy（state）="true"，并且到实时区域完成时清楚该属性。当状态为busy时，辅助技术会追踪和收集改变。当实时区域的状态不为busy的时候，将会读出这些改变。
    当实时区域被更新，更新常常自动告知更新，且是有意义的。例如，如果添加了新的标题，简单的告知标题是有意义的。但是，某些情况下，全部实时区域必须读出来给用户足够的上下文来了解更新。例如，只给用户当前股票的状态而不说是哪个股票，是没有意义的。 atomic设置给辅助技术一个关于哪个事件有更新。
    aria-atomic="false"
    这是默认设置。当该实时区域发生改变时，改变会自己单独呈现；辅助技术不会呈现全部的区域。atomic="false"是一个好的想法，因为这只会通知用户改变的部分不会让用户重复听那些没有改变的信息。但是，web开发者应该密切关注改变信息，当信息单独呈现时，这些信息应该是可理解且符合用户情景的。
    aria-atomic="true"
    把atomic设置为true，这一位置该区域的所有信息整体呈现。当发生改变，辅助技术应该给出整体情况，不只是改变信息。atomic="true"让用户难以获得改变信息，因为改变信息不是单独呈现的。atomic="true"也会给用户造成困扰，因为会让用户听没有改变的重复信息。但是，atomic="true"适合那些改变信息单独呈现但不容易理解和不符合用户情景的情况。注意当atomic="true"，如果一个实时区域发生很多改变时，辅助技术应该一次性的说完所有改变，说的内容为还没有说过的信息。
    不是所有的实时区域的更新都是相关的。比如说，一个标题列表里的旧标题删除，新标题加入，删除的旧标题对用户来说可能就不那么重要，不需要告知用户。但是，在一个聊天应用中，当用户离开聊天，他们用户名字就会从用户列表里面移出，这个移出可能就是重要的信息去告知。有关的设置会提供一个关于哪些类型的改变是相关应该被告知的提示。不相关的任何改变都被当做该实时区域有live="off"来处理。很多类型可以被列为相关，类型用空格分开。如果默认适合应用程序，就不许需要显示提供有关属性。
    aria-relevant="additions"
    实时区域的插入节点应该考虑相关。
    aria-relevant="removals"
    实时区域节点的删除应该考虑相关。经常，删除是不相关的，因为节点的删除是为了给新信息腾出控件。例如，一个日志实现，日志表最上面的条目会删除。但是，在一个类似朋友列表的情况下，朋友删除应该是相关的。没有必要要求屏幕阅读器读出删除，但是它应该通知屏幕阅读器。使用aria-relevant="removals" 或者 aria-relevant="all"应该谨慎。 当内容被删除时辅助技术的通知告知用户可能会引起无数的改变。
    aria-relevant="text"
    在实时区域已经存在的节点文本内容的改变应该考虑相关。文本内容包含等价文本，比如图像的alt属性。
    样例：样例中展示了两个实时区域，如果两个区域都即时竖线，A实时区域应该被先讲因为它的优先级高于B。
```
<div id="liveRegionA" aria-live="assertive">         
</div>         
<div id="liveRegionB" aria-live="polite>         
</div>```
    4.特殊事件实时区域之间的选择
    开发者可能会希望使用特殊实时区域role，而不是使用实时区域属性。wai-aria包含很多标准roles，这些roles默认为网页内的live部分。知道什么时候去使用什么时候去创建一个自定义的实时区域是很重要的。这里有一些经验法则：
    alert
    必须使用alert作为一次性的通知，这些通知显示一段事件然后消失，旨在提醒用户已经发生的事情。辅助技术应该被用户代理通知有警报出现，如果操作系统支持这个事件通知类型。当选择去使用警报应该使用警报对话框role而不是警报内的某些内容来接收焦点。alert和alertdialog会弹出来获得用户的注意。
    status
    当你想要标记定期刷新区域和提供web应用状态的时候常规状态的时候使用status。状态的改变辅助技术不会自动通知。但是，配置一些辅助技术也是可能的，比如脚本屏幕阅读器，监听状态栏的改变并予以通知。当用户常常检查不同网页上的状态改变部分时使用status role很重要。很多应用提供状态小程序，这些小程序是易发现可见，在应用地步，且包含很多小程序来传递状态。状态的使用不会保证辅助技术会怎样响应这个改变。开发者可以live="off" 或 live="assertive"来影响辅助技术的响应。
    timer
    当想要标记从起点想要经过的时间量或剩余的时间的时候，必须使用timer role。封装在timer中的文本指明当前时间的量，并更新当前数值的改变。但是，timer值不一定是机器可解析的。文本内容必须定时刷新，除了timer暂停或者到达重点。
    marquee
    当想要标记滚动区域的时候必须使用marquee，比如股票航行。滚动区域的最新文本必须在DOM中可获得。一个marquee的行为想一个实时区域，它的默认aria-live属性是polite。
    log
    当有一个实时区域有新信息添加时需要使用log，项滚动聊天文本日志。不像其他区域，隐含语义指明新条目到达的事件和阅读顺序。log应该包含有意义的序列，且新信息被添加到log的最后，不是在任意点。如果有一个聊天文本输入区域，应该指明它控制aria的log，例如：
```
<div contenteditable="true" role="log" id="chatlog">
</div>
<label id="gettext">Send Text</label>
<div aria-controls="chatlog" 
     role="textbox" 
     contenteditable="true" 
     aria-labelledby="gettext">
</div>```
live region
    如果有一些其他实时区域使用案例，wai-aria允许使用aria-live属性标记该区域。这与属性的收集是相关联的，这些属性支持实时属性允许去创建自定义实时区域在网页上。更多信息请见实时区域章节。
    实时区域role被应用于很强本土语义元素与平台无障碍API映射不一致。建议开发者将实时区域使用在div或者span元素中。
    样例：
```
<!-- Live region 'log' role used with TABLE element:  the 'log' role is not consistently mapped to platform AAPI. -->
<!-- Do not use. -->
<table role="log" … >
  …
</table>
<!-- Wrap the TABLE element in a DIV with role 'log' instead: -->
<div role="log" … >
  <table … >
    …
  </table>
</div>```

## 2.3浮层



### 2.3.1不知道有浮层弹出


    【问题描述】
    由于网页浮层弹出时，焦点没有及时聚焦到浮层元素内，键盘使用者无法获知有浮层的存在；
    【可能原因】
    1、弹出的浮层没有table index属性，焦点无法跟在触发控件后面，
    2、浮层内容缺少文本描述，例如登录对话框，建议添加title属性来描述。
    【修改建议】

### 2.3.2焦点不在触发控件之后


    【问题描述】
    按tab移动网页焦点到触发浮层控件，激活后，焦点没有及时进入浮层内容，下一个焦点不在浮层内；
    【可能原因】
    可能是弹出的浮层子元素没有添加tabindex，或是javascript直接追加元素非紧跟当前焦点插入元素。
    【修改建议】
    样例1：
    给浮层内的子元素增加tabindex属性。
    样例2：
    获取当前焦点并紧跟其后插入控件元素：
```
<script type="text/javascript">
function createInput(divid){
	var btn = document.activeElement;
	var did = document.getElementById(divid);
	var inp = document.createElement("input");
	inp.type="text";
	inp.name="username";
	inp.value="我跟着"+btn.id;
//	divid.appendChild(inp);
	did.insertBefore(inp,btn.nextSibling);
}
</script>
<div id="divid">
<input name="but1" id="but1" type="button" onclick="createInput('divid');" value="新增输入框1" /><br />
<input name="but2" id="but2" type="button" onclick="createInput('divid');" value="新增输入框2" /><br />
<input name="but3" id="but3" type="button" onclick="createInput('divid');" value="新增输入框3" /><br />
</div>```


### 2.3.3不能使用键盘关闭浮层

    
    【问题描述】
    浮层中的关闭按钮为图片，或自定义控件，导致焦点无法聚焦到关闭控件。
    【可能原因】
    自定义控件为图片链接，没有给图片链接添加alt或title属性，或自定义控件导致的没有焦点。
    【修改建议】
    样例1：
```
<img src="img0.jpg" alt="关闭" tabindex="0" role="button" />```

### 2.3.4用键盘操作，焦点无法进入浮层


    【问题描述】
    使用键盘，无法遍历到浮层内元素；
    【可能原因】
    可能浮层内有阻止焦点进入的代码，或者自定义控件没考虑键盘操作；
    【修改建议】

## 参考资料



### 1.使用onclick/onkeypress事件弹出div形式


    当用户想使用非悬浮的窗口，可以使用onclick/onkeypress事件弹出div的形式，该div覆盖在网页内容上，关闭时直接关闭div。
    无障碍要求：
    1)通过触发link或button控件的onclick/onkeypress事件来加载窗口。
    2)这个窗口的tab顺序紧跟在触发事件之后，该窗口可见。
    3)该窗口的HTML应该与其他内容有同样的无障碍标准.
    关键代码：
    ```
    <button type="button" onclick="TogglePopup(event,true)" name="pop0001">Options</button>```
    全部代码：
    
  ```  
  <button type="button" onclick="TogglePopup(event,true)" name="pop0001">Options</button>
//onclick事件，弹出的div代码
<div class="popover" id="pop0001">
<h3>编辑顺序内容</h3>
<form action="default.htm" onsubmit="this.parentNode.style.display='none'; return false;" onreset="this.parentNode.style.display='none'; return false;">
<fieldset>
<legend>搜索顺序</legend> 
<input type="radio" name="order" id="order_alpha" />
<label for="order_alpha">按字母排序</label>
<input type="radio" name="order" id="order_default" checked="true" />
<label for="order_default">默认</label>
</fieldset>
<div class="buttons">
<input type="submit" value="OK" />
<input type="reset" value="Cancel" />
</div>
</form>
</div>```

### 2.wai-aria模态对话框


    WAI-ARIA提供了两种对话框role：对话框和警告框。当开发者在网页上激发对话框时，常常会将交互模式限制为鼠标。不同于台式计算机上的图形用户界面对话框，用户在键盘导航的时候会偶然的导航到对话框以外使导航变的混乱。这会发生在用户tab进对话框的时候。模态对话框阻止用户聚焦到对话框外的焦点，直到对话框被关闭。鼠标点击对话框外的区域是被忽略的，且用户不能自主的tab进入和移出对话框。所有wai-aria有效对话框都应该是有模态。
    鼠标点击对话框以外的区域可以通过创建一个适口大小的CSS位置元素追加为主体元素的子元素来阻止。设置这个元素的CSS z-index属性，这样就可以使对话框元素在网页所有元素的上面。将底层所有元素的tabindex设为-1来阻止通过键盘事件和鼠标点击来获得焦点。可以通说降低底层元素的透明度来强调对话框本身是模态且有焦点。
    根据对话框执的行目的，对话框弹出之前的聚焦对象的焦点应该被保留。这允许在对话框关闭之后将焦点返回给这个对象。当对话框打开时，焦点应该被设置在对话框的第一个tab可聚焦元素。如果在对话框内容里面没有tab可聚焦元素，将焦点设置在取消或关闭条目上。在对话框里面必须有一些元素可以接受焦点，当对话框打开的时候，读屏软件读出对话框名称和信息。为了组织键盘焦点离开对话框，定义好对话框内的第一个和最后一个焦点元素，并且在网页document中追踪键盘事件。
    搜索对话框容器的内容找到第一个和最后一个tab可聚焦的元素。这个可以通过遍历对话框容器的DOM树来实现，可以发现所有视觉的激活的锚元素、输入元素和其他tabindex大于等于0的元素。tabindex大于等于0的元素都会出现在tab顺序中，并在所有其他tabindex升序的可聚焦元素之前。在变量中存储第一个和最后一个tab焦点条目，在对话框代码的范围中。
    在对话框显示之前，创建和显示对话框底图。连接一个onkeypress事件处理器到 DOM document.documentElement中。这将捕获对话框document中的所有按键，并允许在对话框内捕获键盘焦点。在底图之上的视口内规划对话框的大小和位置，让对话框可见并将焦点设置到对话框内的第一个tab可聚焦元素。
    1.捕获焦点
    onkeypress处理器将捕捉document内容所有按键点击。这个onkeypress处理器应该在对话框代码的范围内，这样才能获得对话框的第一个和最后一个tab可聚焦元素。此外，确定在对话框中只存在一个可获得焦点的项。在这种情况下，第一个tab导航对象将等同于最后一个tab导航对象。如果对话框内的键盘点击可以创建、销毁、启用、禁用或更改可聚焦元素的可见性，则每次接收到点击后，都需要确定第一个和最后一个tab可聚焦元素。基于事件目的，键盘点击应采取以下行动：
    如果按键是Shift + Tab键，按键目标是第一个tab导航对象，然后将焦点设置到最后一个tab导航对象和停止按键事件。如果只有一个tab焦点项，焦点可以不用设置，但按键事件必须停止。如果该按键是一个Tab键，按键目标是最后一个tab导航对象，然后将焦点设置到第一个tab导航对象和停止按键事件。如果只有一个选项卡成为焦点的项目，焦点不必设置，但按键事件必须停止。
    如果按键是退出键，目标节点是的对话框容器节点，然后关闭该对话框，隐藏或销毁对话框底图。
    确定该按键的目标节点是在对话框容器中。这可以通过使用while loop遍历目标节点的父节点，直到找到对话框容器节点。除了以上所述，该对话框内的所有按键应该被允许执行，使得用户可以和对话框中的控件进行交互。
    如果目标节点不是对话框内，documentElement的所有按键和按键事件都应该被停止，除非它是Tab键按下。如果由于某种原因对话框丢失焦点，允许Tab键按下将焦点返回到对话框中。这种情况可能会发生在时间事件中，当对话框第一次加载且焦点不在对话框中的第一个tab焦点元素。
    对话框本身应包含按钮或其他机制以取消该对话框或执行该对话框中的功能和关闭对话框。
    下面是一个模式对话框的onkeypress事件处理程序伪代码。伪代码用于集中在处理程序中，而不是在浏览器事件处理的差异的动作。假设事件对象已归浏览器和辅助对象之间是理浏览器的差异函数图书馆处。该键对象是一组键定义变量。对话框是对话框对象，它具有以取消对话框的功能。
```
_onKey: function(/*Normalized Event*/ evt){
// summary:
// Handles the keyboard events for accessibility reasons
if(evt.charOrCode){
var node = evt.target; // get the target node of the keypress event
if (evt.charOrCode === keys.TAB){
// find the first and last tab focusable items in the hierarchy of the dialog container node
// do this every time if the items may be added / removed from the the dialog may change visibility or state
var focusItemsArray = helper.getFocusItems(dialogContainerNode); 
dialog.firstFocusItem = focusItemsArray[0];
dialog.lastFocusItem = focusItemsArray[focusItemsArray.length-1];
}
// assumes firstFocusItem and lastFocusItem maintained by dialog object
var singleFocusItem = (dialog.firstFocusItem == 
dialog.lastFocusItem);
// see if we are shift-tabbing from first focusable item on dialog
if(node == dialog.firstFocusItem && evt.shiftKey && 
evt.charOrCode === keys.TAB){
if(!singleFocusItem){
dialog.lastFocusItem.focus(); // send focus to last item in dialog
}
helper.stopEvent(evt); //stop the tab keypress event
}
// see if we are tabbing from the last focusable item
else if(node == dialog.lastFocusItem && evt.charOrCode === 
keys.TAB && !evt.shiftKey){
if (!singleFocusItem){
dialog.firstFocusItem).focus(); // send focus to first item in dialog
}
helper.stopEvent(evt); //stop the tab keypress event
}
else{
// see if the key is for the dialog
while(node){
if(node == dialogContainerNode){ // if this is the container node of the dialog
if(evt.charOrCode == keys.ESCAPE){ // and the escape key was pressed
dialog.cancel(); // cancel the dialog
}else{
return; // just let it go
}
}
node = node.parentNode;
}
// this key is for the document window
if(evt.charOrCode !== keys.TAB){ // allow tabbing into the dialog 
helper.stopEvent(evt); //stop the event if not a tab keypress 
}
} // end of if evt.charOrCode
} // end of function```

## 2.4表单



### 2.4.1方向键访问顺序有问题


    【问题描述】
    使用屏幕阅读器浏览网页，用上下方向键访问到的元素，与实际视觉布局不符的；
    【可能原因】
    造成不同步的主要问题是html代码顺序问题，屏幕阅读器是按照代码顺序来截取信息，造成与视觉不匹配，例如，一个搜索框后面应该跟着是搜索按钮，如果先写了搜索按钮，在写编辑框，利用CSS把搜索按钮移动到编辑框右侧，这种情况，屏幕阅读器依然按照代码书写顺序获取，导致视觉与方向键访问的顺序不一致性。
    【修改建议】

### 2.4.2必填区域不可获得

    
    【问题描述】
    用键盘操作，焦点进入表单，没有一种方式提醒屏幕阅读器用户，哪些信息是必填项目；
    【可能原因】
    必填项目的编辑框，没有添加（aria-required ="true"）；
    【修改建议】

### 2.4.3错误提示无法访问


    【问题描述】
    某些表单信息是否填写正确均为一个图片，屏幕阅读器用户无法获知图片的含义；
    【可能原因】
    错误信息没有焦点，或错误信息为图片，例如图片显示的是一个“叉叉”或是一个“勾勾”；
    【修改建议】

### 2.4.4Tab逻辑顺序有问题


    【问题描述】
    按TAB键移动焦点访问的顺序，与视觉顺序不一致，例如：验证码编辑框后面不是验证码图片或不是验证码换一张的链接。
    【可能原因】
    某些表单内元素使用了tabindex来干扰访问顺序；
    【修改建议】


## 参考资料



### 1.如果输入错误能够被自动发现，错误类型应能被标识，并且用文本描述给用户


    (1)提供给用户文本描述来确认必填却没有完成的部分；
    1)当用户试图去提交一个表单，忽略几个输入或者选择项，使用客户端验证检测弹出一个警告哪些部分没有完成，这些有完成部分的label标签突出显示，方便用户查看填写。
    2)当用户试图去提交一个表单，忽略几个输入或者选择项，使用客户端验证检测，表单和文本描述信息在页面顶端显示，每一个忽略的区域的label信息需要突出显示，用户不需要去重新查找。
    3)如果一个表单里面包含强制性的区域，如果忽略，报错。必填类。
    (2)使用Aria-Invalid来特使错误区域
    适用于错误描述不需要编程式确定错误区域；错误区域的显示不能被某些用户获得，例如使用错误图标或者渲染颜色来告知用户错误，不依靠颜色和视觉的用户无法获得错误信息；开发者通常喜欢编程式的将错误描述和错误区域联系在一起，但有时候会因为框架的设计不允许这样做。在这些情况下，开发者可以编程式的将aria-invalid设置为true，在非法输入的区域。这被辅助技术所喜欢，如读屏软件和屏幕放大器。当一个区域的有aria-invalid且被设置为真，当获得焦点时，voiceover会读“无效数据”，JAWS和NVDA会指明错误为“无效输入”；ARIA属性必须编程式设置，提交前不应该将ARIA-Invalid设置为true，，设置为false相当于没设置该属性。当编程式确定可见文本来确认错误区域，或者传达其他错误信息的时候，可以不将ARIA-Invalid设置为true，但是设置了还是会为用户提供有效信息。
    样例1：
    ARIA-Invalid使用在必填区域却没有输入的情况下。当表单需要传达信息提交按钮需要做到以下：（是JQUERY程序和html表单）
    关键代码：
```
if ($('#first').val() === '') //如果fisrt的值为空
{ 
$('#first').attr("aria-invalid", "true"); //将first的aria-invalid设置为真；
$("label[for='first']").addClass('failed'); //first的label添加failed样式；
} ```
    全部代码：

```
<code> <script> ... ... 
if ($('#first').val() === '') //如果fisrt的值为空
{ 
$('#first').attr("aria-invalid", "true"); //将first的aria-invalid设置为真；
$("label[for='first']").addClass('failed'); //first的label添加failed样式；
} 
if ($('#last').val() === '') //last的值为空
{ 
$('#last').attr("aria-invalid", "true"); //将last的aria-invalid设置为真；
$("label[for='last']").addClass('failed'); //last的label添加failed样式；
} 
if ($('#email').val() === '') //email的值为空；
{ 
$('#email').attr("aria-invalid", "true"); //将email的aria-invalid设置为真；
$("label[for='email']").addClass('failed'); //email的label添加failed样式；
} ... ... 
</script> 
<style type="text/css"> 
label.failed { border: red thin solid; } //failed样式；
</style> 
<form name="signup" id="signup" method="post" action="#"> 
<p> 
<label for="first">名(必填)</label>
<br> 
<input type="text" name="first" id="first"> 
</p> 
<p> 
<label for="last">姓 (必填)</label>
<br> 
<input type="text" name="last" id="last"> 
</p> 
<p> 
<label for="email">邮件(必填)</label>
<br> 
<input type="text" name="email" id="email"> 
</p> 
<p> 
<input type="submit" name="button" id="button" value="提交"> 
</p> 
</form> </code>```
    样例2：确定数据格式错误
    在确认用户身份证号码、邮件地址、开始结束日期的格式错误的时候，Aria-invalid和aria-describedby是合起来用的。错误信息需要使用aria-describedby与区域联系起来，aria-invalid将使错误区域更易编程式获得。
    当无效的邮件地址输入时，没有@，html代码为：
```
<div class="control"> 
<p>
<label for="email">邮件地址: [*]</label> 
<input type="text" name="email" id="email" class="error" aria-invalid="true" aria-describedBy="err_1" />
</p> 
<span class="errtext" id="err_1">错误：错误输入</span>
</div>```
    当没有数据输入是，html代码为：
```
<div class="control"> 
<p>
<label for="email">邮件地址: [*]</label> 
<input type="text" name="email" id="email" class="error" aria-invalid="true" aria-describedby="err_2" />
</p> 
<span class="errtext" id="err_2">错误：数据为空</span> </div>```
    JQUERY代码：JQUERY用来添加aria-invalid或者aria-describedby属性作为class属性和添加错误文本，这是一段将代码，用来插入aria-invalid和error class，但是没有将错误信息与控件编程式联系起来：
```$(errFld).attr("aria-invalid", "true").attr("class", "error");//将errFld的aria-invalid设置为true，class设置为error
// Suffix error text: $(errFld).parent().append('<span class="errtext">Error: Incorrect data</span>');
CSS代码为：
input.error { border: red thin solid;} 
span.errtext { 
margin-bottom: 1em; 
padding: .25em 1.4em .25em .25em; 
border: red thin solid; 
background-color: #EEEEFF; 
background-image:url('images/iconError.gif'); 
background-repeat:no-repeat; background-position:right;	 
}```
    (3)提供客户端验证与警报
    此技巧用来在客户端验证用户输入数据的正确性，通过客户端脚本。如果找到错误，警告窗口会弹出，告知用户错误的地方，一旦用户关闭警告窗口，使用JS将焦点定位到错误区域。
    样例1：
    使用事件处理器来检查单独的控件：
```
<label for="date">日期:</label>
<input type="text" name="date" id="date" 
onchange="if(isNaN(Date.parse(this.value))) 
alert('这不是一个有效的数据. 请重新输入.');" />
//onchange用来检查数据格式；```

    样例2：
    当用户提交表单时检查多个控件；
    下面的例子展示了一个表单的多个控件，表单控件使用onsubmit属性来执行检查脚本当用户提交表单的时候。如果检查成功，将会返回true，且表单继续提交，如果发现错误，将会显示出错误信息，返回false来取消提交，让用户修改错误；
    
    注：这个例子为了简化，只展示了警告。更加有用的告知应该是错误控件高亮，将错误信息添加到网页，还有告知怎样导航到错误区域；这个例子使用onsubmit属性来检查，正常的情况是创建一个submit事件监听器当网页被加载时；
    脚本代码：
```
function validate() {
	// 定义错误信息
	var msg = "";
	
	//有效名字
	var pattern = /^[a-zA-Z\s]+$/;
	var el = document.getElementById("name");
	if (!pattern.test(el.value))  msg += "名称只能有字母和空格. ";
	
	// 有效的电话号码
	var pattern = /^[\d\-+\.\s]+$/;
	var el = document.getElementById("tel");
	if (!pattern.test(el.value))  msg += "电话号码只能有数字和分隔符. ";
	
	if (msg != "") {
		alert(msg);
		return false;
	} else return true;
}```
html代码：
```
<form action="multiple-controls.html" onsubmit="return validate()">
	<p>
		<label for="name">名字: </label>
		<input type="text" name="name" id="name" />
	</p>
	<p>
		<label for="tel">电话号码: </label>
		<input type="text" name="tel" id="tel" />				
	</p>
	<p>
		<input type="submit" />
	</p>
</form>```
    （4）使用aria-alertdialog确认错误
    使用role="alertdialog"来创建一个通知，这个通知应该与以下行为联合使用：aria-label或aria-labelledby属性应该给alertdialog一个无障碍的名字；aria-labelledby为警告的文本提供一个参考；alertdialog包含至少一个焦点，当alertdialog被打开时应该自动获得焦点；tab顺序应该限制在alertdialog内，当alertdialog打开时；将窗口关闭时，如果可能的话应该返回原位置；
    注意：alertdialog应该不被辅助技术识别，除非它被需要。需要做的是不要在静态html中包含alertdialog，而是将它通过脚本插入到DOM中，当错误信息被触发的时候。
    
    样例1：弹出窗口
```
<div role="alertdialog" aria-labelledby="alertHeading" aria-describedby="alertText">
<h1 id="alertHeading">错误</h1>
<div id="alertText">员工的出生日期是他们雇佣日期之后。出生日期请核实和聘请日期。</div>
<button>保存继续</button>
<button>返回修改错误</button>
</div>```
    （5）使用ARIA role=alert或者即时区来显示错误
    这个技巧的目的是当错误输入发生时，辅助技术可以识别。aria-live属性使辅助技术可以被告知当即时区域容器有错误信息注入时。aria-live区域的内容将会被辅助技术自动阅读，而不是需要将文本放在焦点区域；
    样例1:
    将错误信息注入到含有role=alert且已经在DOM中显示的容器中。
    这个例子中role=alert相当于aria-live=assertive
    关键代码：
```
$(document).ready(function(e) {
	$('#signup').submit(function() {此处省略```
    全部代码：
```
<script src="http://code.jquery.com/jquery.js"></script>
<script>
$(document).ready(function(e) {
	$('#signup').submit(function() {
		$('#errors').html('');
		if ($('#first').val() === '') {
			$('#errors').append('<p>请输入你的名.</p>');
		}
		if ($('#last').val() === '') {
			$('#errors').append('<p>请输入你的姓.</p>');
		} 
		if ($('#email').val() === '') {
			$('#errors').append('<p>请输入你的邮件地址.</p>');
		} 
		return false;
	});
});
</script>
<form name="signup" id="signup" method="post" action="">
  <p id="errors" role="alert" aria-atomic="true"></p>//错误文本，JQUERY将错误信息添加到该区域
  <p>
    <label for="first">名（必填）</label><br>
    <input type="text" name="first" id="first">
  </p>
  <p>
    <label for="last">姓（必填）</label><br>
    <input type="text" name="last" id="last">
  </p>
  <p>
    <label for="email">邮件（必填）</label><br>
    <input type="text" name="email" id="email">
  </p>
  <p>
    <input type="submit" name="button" id="button" value="Submit">
  </p>
</form>```
    (6)当用户用户提供的信息不在允许的列表值里面，提供一个文本描述。当输入值必须是合法的预设值里面的一个，文本描述应该告知用户，预设值列表应尽可能包含所有可能的值，或者建议输入的值应该与合法值非常类似；
    样例1：
    当用户输入非法值时，在用户提交表单之前，警告窗口应该出现并描述错误以便用户修改；
    样例2：
    用户输入非法值且提交了表单，服务器返回了表单，用户输入的数据依然存在，在网页顶部给出输入错误描述。文本描述错误的本质，而且容易导航到问题区域。
    (7)当用户输入错误格式和错误值时，需要提供一个说明；需要做到以下几个方面来帮助用户：为输入提供正确的范例；描述正确的输入；给出用户输入数据的正确格式，指导用户怎样输入这些正确的值；
    样例1：
    当用户注册邮箱的时候，用户输入的邮箱账号已经被注册，给出几个基于用户输入账号合法且未注册的候选账号；

    2.当需要用户输入内容时，要给出标签或说明
    为交互组件提交必要的目的说明，说明信息输入的必要性；
    (1)使用aria-describedby属性为交互控件提供文本说明，通过使用id将描述信息与一个或多个控件联系起来。
    样例1：
    ```
    使用aria-describedby属性描述临近button的行为；
<button aria-label="Close" aria-describedby="descriptionClose"
    onclick="myDialog.close()">按钮</button>//id为descriptionClose的控件为button提供描述文本
...
<div id="descriptionClose">关闭此窗口将忽略输入的所有信息，并回返回到主页</div>```
    样例2：
    使用aria-describedby属性将说明与表单联系起来；
```
<form>
<label for="fname">名</label>
<input name="" type="text" id="fname" aria-describedby="int2">
<p id="int2"> 该区域使用aria-describedby连接说明文本. </p>
</form>```
    样例3：
    使用aria-describedby为button提供详细信息
```
<p><span id="fontDesc">选择该网页的字体大小</span>
<button type="button" id="fontB" onclick="doAction('Fonts');" aria-describedby="fontDesc">字体</button>
</p>
<p><span id="colorDesc">选择该网页的颜色</span>
 <button type="button" id="colorB" onclick="doAction('Colors');" aria-describedby="colorDesc">颜色</button>
</p>
<p><span id="customDesc">自定义此页面上使用的布局和样式</span>
 <button type="button" id="customB" onclick="doAction('Customize');" aria-describedby="customDesc">自定义</button>
</p>```

样例4：
使用aria-describedby属性为表单区域连接提示
```role="tooltip"```表示提示文本
aria-hidden字符串。可选值为true和false, true表示元素隐藏(不可见)，false表示元素可见。
关键代码：
```
<input 此处省略部分代码
      aria-describedby="tp1"
      aria-required="false"/>```
全部代码：
```
<html lang="en-us">
<head>
<title>行内：提示样例1</title>
//链接外部样式表，js和图片；
<link rel="stylesheet" href="css/tooltip1_inline.css" type="text/css">
<script type="text/javascript"src="js/tooltip1_inline.js">
</script>
<script type="text/javascript" src="../js/widgets_inline.js">
</script>
<script type="text/javascript" src="../js/globals.js"></script>
<link rel="icon" href="http://www.cites.uiuc.edu/favicon.ico" type="image/x-icon">
<link rel="shortcut icon" href="http://www.cites.uiuc.edu/favicon.ico" type="image/x-icon">
</head>
   ...
<body onload="initApp()">
<div id="container">
<h1>提示样例1</h1>
<h2>创建账户</h2>
<div class="text">
<label for="first"> 名:</label>
<input type="text" id="first" name="first" size="20"
      onmouseover="tooltipShow(event, this, 'tp1');"
      onfocus="tooltipShow(event, this, 'tp1');"
      aria-describedby="tp1"
      aria-required="false"/>
<div id="tp1" role="tooltip" aria-hidden="true">你的名字可选. </div>
</div>```
    (2)使用aria-labelledby连接一个标签和多个文本节点，应用与输入控件，aria-labelledby可以被用于label本地输入和非本地输入，例如contenteditable="true"的自定义输入控件div;aria-labelledby的一个特殊使用是文本输入控件，当一个有意义的标签应该包含多个label；id顺序应该是有逻辑的能被读屏软件读取的顺序；
    样例1：
    一个连接超时输入字段标签；
```
<form>
<p>
<span id="timeout-label" tabindex="-1">
<label for="timeout-duration">延长时间到</label>
</span>
<input type="text" size="3" id="timeout-duration" value="20" 
    aria-labelledby="timeout-label timeout-duration timeout-unit">//timeout-label包含label， timeout-duration为label的id; 

timeout-unit是个span元素的id；
<span id="timeout-unit" tabindex="-1"> 分钟</span>
</p>
</form>```

    样例2：
    文本输入的简单数据表格；
    关键代码：
```
<td><input type="text" size="20" aria-labelledby="tpayer gross"/></td>```
    全部代码：
```
<table>
<tr>
<td></td>
<th id="tpayer">纳税人</th>
<th id="sp">配偶</th>
</tr>
<tr>
<th id="gross">W2总值</th>
<td><input type="text" size="20" aria-labelledby="tpayer gross"/></td>
<td><input type="text" size="20" aria-labelledby="sp gross" /></td>
</tr>	
<tr>
<th id="div">股息</th>
<td><input type="text" size="20" aria-labelledby="tpayer div"/></td>
<td><input type="text" size="20" aria-labelledby="sp div" /></td>
</tr>
</table>
```
    样例3：
    会议工作坊预订表；
    关键代码：
```<p><input type="checkbox" id="TM1" aria-labelledby="title-TM1 track1 am1 TM1-att">
<label id="TM1-att" for="TM1">参加</label></p>```
    全部代码：
```
<h1>恐龙研讨会的时间表星期四，14。星期五，15。月2013</h1>
<table>
<caption>恐龙会议研讨会预订表</caption>
<tbody><tr>
	<td rowspan="2"></td>
	<th colspan="2" scope="colgroup">星期四</th>
	<th colspan="2" scope="colgroup">星期五</th>
</tr>

<tr>
	<th scope="col" id="am1">上午9-12</th>
	<th scope="col" id="pm1">下午2-5</th>
	<th scope="col" id="am2">上午9-12</th>
	<th scope="col" id="pm2">下午2-5</th>
</tr>

<tr>
<th id="track1" scope="row">路径1</th>
<td>
<h2 id="title-TM1">古生代 </h2>
<p>剩下两个地方</p>
<p><input type="checkbox" id="TM1" aria-labelledby="title-TM1 track1 am1 TM1-att">
<label id="TM1-att" for="TM1">参加</label></p>
</td>
<td>
<h2 id="title-TA1">中生代概述</h2>
<p>剩下2个地方</p>
<p><input type="checkbox" id="TA1" aria-labelledby="title-TA1 track1 am2 TA1-att">
<label id="TA1-att" for="TA1">参加</label></p>
</td>	
<td>
<h2 id="title-FM1">三叠世时期恐龙的崛起</h2>
<p>剩下1个地方</p>
<p><input type="checkbox" id="FM1" aria-labelledby="title-FM1 track1 pm1 FM1-att">
<label id="FM1-att" for="FM1">参加</label></p>
</td>	
<td>
<h2 id="title-FA1">侏罗纪时期</h2>
<p>剩下11个地方</p>
<p><input type="checkbox" id="FA1" aria-labelledby="title-FA1 track1 pm2 FA1-att">
<label id="FA1-att" for="FA1">参加</label></p>
</td>
</tr>
<tr>
<th id="track2" scope="row">路径2/th>
<td>
<h2 id="title-TM2">白垩系</h2>
<p>剩下18个地方</p>
<p><input type="checkbox" id="TM2" aria-labelledby="title-TM2 track2 am1 TM2-att">
<label id="TM2-att" for="TM2">参加</label></p>
</td>
<td>
<h2 id="title-TA2">恐龙的灭绝</h2>
<p>剩下两个地方</p>
<p><input type="checkbox" id="TA2" aria-labelledby="title-TA2 track2 am2 TA2-att">
<label id="TA2-att" for="TA2">参加</label></p>
</td>
<td>
<h2 id="title-FM2">首次发现恐龙</h2>
<p>剩下2个地方</p>
<p><input type="checkbox" id="FM2" aria-labelledby="title-FM2 track2 pm1 FM2-att">
<label id="FM2-att" for="FM2">参加</label></p>
</td>
<td>
<h2 id="title-FA2">新兴学术</h2>
<p>剩下19个地方</p>
<p><input type="checkbox" id="FA2" aria-labelledby="title-FA2 track2 pm2 FA2-att">
<label id="FA2-att" for="FA2">参加</label></p>
</td>
</tr>
</tbody>
</table>```
    (3)使用组的roles来区分有关表单控件；
    这个技巧是用来将表单内的一组相关控件标记为一个组。与组有关的任何标签都有普通标签的作用或者作为组内单独控件的限定符。辅助技术可以识别组的开始和结束，组的标签可以作为进入和离开组的导航。这是表单组控件编程式添加替代，当界面设计不允许出现fieldset-legend的时候。
    对于单选控件组，可以使用role="radiogroup"而不是role="group";group可以使用aria-labelledby标记；这个技巧不是针对表单内所有的元素，只是针对role="group"的单个容器；
    
    样例1：
    社会保障号码有9位，分成3部分，可以使用role="group";
```
<div role="group" aria-labelledby="ssn1">
<span id="ssn1">社会保障号码#</span> 
<span style="color: #D90D0D;"> * </span>
<input size="3" type="text" aria-required="true" title="前三位" />-
<input size="2" type="text" aria-required="true" title="后两位" />-
<input size="4" type="text" aria-required="true" title="最后四位" />
</div>```
    样例2：识别单选groups
    下面的例子使用的是role=radiogroup；单选控件使用的是role=radio的自定义控件；
    关键代码：
    ```
    <div role="radiogroup" aria-labelledby="alert1">```
    全部代码：
```
<h3>为您的帐户设置警报</h3>
<div role="radiogroup" aria-labelledby="alert1">
<p id="alert1">平衡超过3000美元时发出警报</p>
<div>
<span tabindex="0" role="radio" aria-labelledby="a1r1" name="a1radio"></span>
<span id="a1r1">是</span>
</div>
<div>
<span tabindex="0" role="radio" aria-labelledby="a1r2" name="a1radio"></span>
<span id="a1r2">否</span>
</div>
</div>
<div role="radiogroup" aria-labelledby="alert2">
<p id="alert2">当收费超过250美元时发出警报</p>
<div>
<span tabindex="0" role="radio" aria-labelledby="a2r1" name="a2radio"></span>
<span id="a2r1">是</span>
</div>
<div>
<span tabindex="0" role="radio" aria-labelledby="a2r2" name="a2radio"></span>
<span id="a2r2">否</span>
</div>
</div>
<p><input type="submit" value="Continue" id="continue_btn" name="continue_btn" /></p>```
    有关的CSS样式为：
```
div[role=radiogroup] {
  border: black thin solid;
} ```
    (4)为期望数据提供模式和样例；
```
<label for="date">Date (dd-mm-yyyy)</label>
<input type="text" name="date" id="date" />```
    (5)在表单或者一系列需要填写的区域的开端提供必要的文字来描述必须输入的内容；
    1)在会员制网站，填写个人信息的时候，工作信息包括公司名、职位、期限、工作描述；在开端给出提示文本：输入你认为你的个人简历可以添加的内容，日期数据应该是mm/dd/yyyy format；
    2)一个企业档案允许用户在修改个人信息的时候允许用户修改电话号码、工作职责，顶部的提示信息要有：可以修改任何区域的信息，当修改完，想要保存点击确定，不想保存，点击取消；不能修改个人简历中的系统提供部分；电话号码智能包括数字和—；必填区域用*标记，必须填写；
    (6)根据label的位置来增加文本与控件的关系；
    1)Label在文本输入框的上面；
    2)Label在文本输入框的左侧；
    3)Label在单选按钮的右侧；
    (7)使用label和legend来明确支出表单控件的必填状态；
    1)可以使用文本来指出必填状态：
```
<label for="firstname">名(必填):</label> 
<input type="text" name="firstname" id="firstname" />```
    2)使用星号（*）来指出必填状态：
```
<p> 所需的领域都标有星号(<abbr class="req" title="必填">*</abbr>).</p>```
    3)使用图片来指出必填状态：
```
<p><img src="req_img.gif" alt="必填控件" /> 指示所需的窗体控件</p>```
    4)指出单选组和复选组的必填状态：
```
<fieldset>
<legend>I我对以下（要求）感兴趣：</legend>
<input type="checkbox" id="photo" name="interests" value="ph">
<label for="photo">摄影</label> </br>
<input type="checkbox" id="watercol" name="interests" checked="checked" value="wa">```
    legend 元素为fieldset 元素定义标题（caption）
    (8)使用fieldset和legend元素来描述表单控件中的组；
    这个技巧为有关的表单控件提供一个语义组。这可以使用户更快更好的理解控件间的关系更好的交互；可以使用fieldset来将表单控件分组闭合起来。所有的控件都在相关的fieldset内。fieldset的第一控件一定是legend元素，为组提供标签或描述。开发者应该尽量避免嵌套使用fieldset，因为嵌套使用会导致混乱；组控件对单选和复选特别重要，当单选和复选按钮包含明确的说明和区分选择，fieldset和legend不是必须。有时候，开发者会避免使用fieldset，因为有些浏览器会默认为fieldset添加边框。视觉的显示可以通过CSS样式来改变；
    
    样例1：多选测试
    这个立场展示一个测试项目，有一个问题和5个可能的答案。每一个答案通过单选按钮来显示，单选按钮包含在fieldset内，测试问题使用legend标记。
    fieldset 元素可将表单内的相关元素分组。<legend> 标签为 fieldset 元素定义标题。
    关键代码： 
   ``` 
   <legend>戏剧<cite>哈姆雷特</cite> 作者是:</legend>```
    全部代码：
```
<fieldset>
  <legend>戏剧<cite>哈姆雷特</cite> 作者是:</legend>
  <input type="radio" id="shakesp" name="hamlet" checked="checked" value="a">
  <label for="shakesp">莎士比亚威廉</label><br />
  <input type="radio" id="kipling" name="hamlet" value="b">
  <label for="kipling">英国作家吉卜林</label><br />
  <input type="radio" id="gbshaw" name="hamlet" value="c">
  <label for="gbshaw">萧伯纳</label><br />
  <input type="radio" id="hem" name="hamlet" value="d">
  <label for="hem">海明威厄内斯特</label><br />
  <input type="radio" id="dickens" name="hamlet" value="e">
  <label for="dickens">狄更斯查尔斯</label>
</fieldset>  ```

    样例2：复选框
    个人简介也允许用户指明自己的兴趣，通过选择复选按钮，每一个复选按钮都有一个标签。

```
<fieldset>
  <legend>我感兴趣的是以下（检查所有申请）：</legend>
  <input type="checkbox" id="photo" name="interests" value="ph">
  <label for="photo">摄影</label><br />
  <input type="checkbox" id="watercol" name="interests" checked="checked" value="wa">
  <label for="watercol">水彩画</label><br />
  <input type="checkbox" id="acrylic" name="interests" checked="checked" value="ac">
  <label for="acrylic">丙烯画</label>
  …
</fieldset>  ```

    样例3：
    相同name属性的单选按钮；

```
<form action="http://example.com/vote" method="post">
<fieldset>
<legend>你最喜欢的哲学家</legend>
<input type="radio" name="philosopher" id="philosopher_socrates" value="socrates"/>
<label for="philosopher_socrates">苏格拉底</label>
<input type="radio" name="philosopher" id="philosopher_plato" value="plato"/>
<label for="philosopher_plato">柏拉图</label>
<input type="radio" name="philosopher" id="philosopher_aristotle" value="aristotle"/>
<label for="philosopher_aristotle">亚里士多德</label>
</fieldset>
</form>   ```
    样例4：逻辑有关控件；
    此例子中，居住地址和邮寄地址是分开的;

```
<form action="http://example.com/adduser" method="post">
   <fieldset>
     <legend>居住地址：</legend>
     <label for="raddress">地址: </label>
     <input type="text" id="raddress" name="raddress" />
     <label for="rzip">邮编: </label>
     <input type="text" id="rzip" name="rzip" />
     更多居住信息
   </fieldset>
   <fieldset>
     <legend>邮寄地址</legend>
     <label for="paddress">地址: </label>
     <input type="text" id="paddress" name="paddress" />
     <label for="pzip">邮编： </label>
     <input type="text" id="pzip" name="pzip" />
   更多邮寄信息
   </fieldset>
</form>```
    (9)使用title属性来区分表单控件，当标签不能用的时候；
    样例1：
    一个限制搜索范围的下拉菜单；
    一个搜索表单使用下拉菜单来限制搜索的范围。当文本输入搜索表单的时候，下拉菜单立即与文本域连接，搜索区域与下拉菜单的关系看起来很清楚，但是没有可见的视觉标签，title属性可以用来明确选择菜单。title属性可以被屏幕阅读器阅读，为使用屏幕放大器的用户提供提示；
```
<label for="searchTerm">搜索:</label>
<input id="searchTerm" type="text" size="30" value="" name="searchTerm">
<select title="在以下中搜索" id="scope">
…
</select> ```
    样例2：电话号码的输入区域
    美国的电话号码包括三部分，地区代码、交换、后四位；
```
<fieldset><legend>电话号码</legend>
<input id="areaCode" name="areaCode" title="地区代码" 
type="text" size="3" value="" >
<input id="exchange" name="exchange" title="电话号码前三位" 
type="text" size="3" value="" >
<input id="lastDigits" name="lastDigits" title="电话号码后四位" 
type="text" size="4" value="" >
</fieldset> ```

    样例3：搜索功能：
    给文本输入控件添加title属性，用来告知用户功能来位置；
```
<input type="text" title="请输入搜索文本" />
<input type="submit" value="Search"/>```
    样例4：表单控件的数据表格
    表单控件的数据表格单元需要将每一个控件都与列和行的表头联系。没有标题，对视障用户来说当tab到表格是，需要停下来使用辅助技术去查看每个行列的值。
    (10)使用临近按钮来标记区域的目的
    样例1：搜索功能
    当一个网页包含文本输入框和一个搜索按钮来实现搜索功能，这个按钮被放置在文本输入框的右边，这样就能很清楚的知道文本输入框是输入文本的地方；
```
<input type="text" name="kw" id="kw" maxsize="100" maxlength="100" />
<input type="submit" value="搜索" />`````````

    样例2：选择表单
    美国用户必须填表单，因为法律和要求在不同的州是不一样的，用户需要选择自己州的表单样式。一个下拉菜单允许用户去选择一个州。临近按钮的标签为选择州表单。点击按钮，可以跳转到该州的表单网页。
    3.错误建议
    如果输入错误能够被自动发现，且修改建议已知，则提供建议给用户，除非它会危及安全或影响内容目的。 
    (1)为没有完成的必填区域添加文本描述；
    1种方法是在客户端检验提供一个弹出框来标识哪些必填区域被忽略；另一个方法是，使用客户端验证重新显示表单，在忽略的必填区域附近给予文本描述，或给给一个文本描述告知用户忽略的必填区域。
    最好的做法是包含一个信息或警告，因为一部分用户不知道错误发生且假设表单功能性错误。将错误警告包含在网页标题中也是个好方法，因为读屏用户经常相信网页提交正确，继续到当道其他页，而不去重新阅读网页的主要内容区域。
    (2)使用aria-required属性来区分必填区域；
    这个方法是编程式确定的方法来表明该区域必填，这个效果也可以通过视觉来达到。
    必填通常是视觉展示的，但是不能编程式作为区域名字的一部分；aria-required属性在提交前指明用户必填。aria-required属性有true和false。
    注：当星号和其他文本符号编程式与区域联系，aria-required="true"对辅助技术使用者来说是有好处的。
    元素必填经常通过视觉呈现，例如符号或符号在空间后。使用aria-required属性使用户代理更容易的通过用户代理特有的方式向用户传递信息。wai-aria状态和属性也兼容其他语言。
    
    样例1:
    必要属性通过星号来显示；
```
<form action="#" method="post"  id="login1" onsubmit="return errorCheck1()">
  <p>注意: [*]是必填区域</p> 
  <p>
    <label for="usrname">登录名: </label> 
    <input type="text" name="usrname" id="usrname" aria-required="true"/>[*]
  </p>
  <p>
    <label for="pwd">密码</label> 
    <input type="password" name="pwd" id="pwd" size="12" aria-required="true" />[*]
  </p> 
  <p>
    <input type="submit" value="Login" id="next_btn" name="next_btn"/>
  </p>
</form>	
```
    样例2：
    使用必填字样来指明必填属性；

```
<head>
<form action="#" method="post" id="step1" onsubmit="return errorCheck2()">
  <p>
    <label for="fname">名: </label> 
    <input type="text" id="fname" aria-required="true" />
    [必填]
  </p>
  <p>
    <label for="mname">中名: </label> 
    <input type="text" id="mname" />
  </p>
  <p>
    <label for="lname">姓: </label> 
    <input type="text" id="lname" aria-required="true" />
    [必填]
  </p>
  <p>
    <label for="email">邮件: </label> 
    <input type="text" id="email" aria-required="true" />
    [必填]
  </p>
  <p>
    <label for="zip_post">右边: </label> 
    <input type="text" id="zip_post" size="6" aria-required="true" />
    [必填]
  </p>
  <p>
    <input type="submit" value="Next Step" id="step_btn" name="step_btn" />
  </p>
</form> ```

    样例3：
    在内容之前使用CSS样式来渲染红边框指明必填属性。

```
<head>
<form action="#" method="post" id="alerts1">
  <label for="acctnum" data-required="true">账户号</label>
  <input size="12" type="text" aria-required="true" name="acctnum" />
 <p id="radio_label">当余额超过$3000名请发送警报。</p>
 <ul  id="rg" role="radiogroup" aria-labelledby="radio_label">
    <li id="rb1" role="radio" aria-required="true">Yes</li>
    <li id="rb2" role="radio" aria-required="true">No</li>
 </ul>	
</form> 
CSS样式：
<head>
[aria-required=true] {
  border: red thin solid;
} 
[aria-required=true]:before {
  content: url('/iconStar.gif');
}

[data-required=true]:after {
  content: url('/iconStar.gif');
}```

样例4.
通过使用JS添加aria-required属性；
关键代码：field.setAttribute("aria-required", "true");
全部代码：
<head>
 <script type="text/javascript">
 //<![CDATA[
 // 这个页面上所有必填区域的数组或id组
 var requiredIds = new Array( "firstName", "lastName");
 // 当页面加载时，给requiredIds数组里面每个元素添加aria-required属性
 function setRequired(){
 	if (requiredIds){
 		var field;
 		for (var i = 0; i< requiredIds.length; i++){
 			field = document.getElementById(requiredIds[i]);
 			field.setAttribute("aria-required", "true");
 		}
 	}
 }
 window.onload=setRequired;
//]]>
 </script>
 </head>
 <body>
 <p>请输入以下数据。必需字段已被编程鉴定为需要和带星号（*）以下字段标签标记。</p>
 <form action="submit.php">
 <p>
 <label for="firstName">名 *: </label><input type="text" name="firstName" id="firstName" value="" />
 <label for="lastName">姓 *: </label><input type="text" name="lastName" id="lastName"  value="" />
 </p>
 </form>
 </body>
(3)使用aria-alertdialog来指出错误；
(4)当用户用户提供的信息不在允许的列表值里面，提供一个文本描述。当输入值必须是合法的预设值里面的一个，文本描述应该告知用户，预设值列表应尽可能包含所有可能的值，或者建议输入的值应该与合法值非常类似；
(5)提供建议修正文本；
这个技巧是在用户提交的信息不被接受，为用户提供建议修正文本。这个建议可能包括正确拼写或者相似的文本。依靠表单，建议可以渲染在错误区域附件，或者在其他网页。可能的话，修改建议应该让用户容易获得和使用。例如，错误的提交应该返回一个可能的修正列表，用户可以通过选择来指出哪个选择是想要的。建议或者建议的链接应该与其联系的表单区域靠近买传说在表单顶部，在表单区域之前，或者临近需要修改的表单。
样例1：
一个表单要求用户输入时间长度，可以是年月日。用户输入数字6.服务器返回表单，用户输入的数据还在且包含建议文本：检测到错误：您是想选6天、6个周、6个月、6年？
样例2：
用户输入错误的城市名。服务器返回表单，在表单顶部还告知用户的错误和一个用户可能需要的城市列表，这个列表是通过城市名的数据库比对得来的。
```<script type="text/javascript">
</script>
<div class="message">
您是要找<a href="javascript:void(0);" onclick="document.getElementById('city').value = '北京';">北京</a>吗？
</div>
城市:<input type="text" name="city" id="city" value="北经" />```
样例3：
公交路线规划允许用户输入他们的目的地、允许用户输入街道地址、十字路口和城市路标。当用户输入"kohl",会返回与输入相似的结果，搜索‘Kohl’得到以下结果。一个选择框跟随建议列表, "Kohl Center," "Kohl's Dept. Store-East" 、 "Kohl's Dept. Store-West"，用户可以根据意向进行选择；
样例4：
搜索支持拼写检查，如果检查到拼写错误会提供替代链接。当用户点击链接时，搜索自动提交更正后的拼写。
(6)提供客户端验证和警告
(7)提供客户端验证，通过使用DOM添加错误信息
当客户端验证表单有问题时，这个技巧用来加强错误信息的显示。锚元素用来在列表里显示错误信息，并插入到表单顶部。锚元素被使用到错误信息中，所以焦点会被放置在错误信息上，吸引用户的注意。锚元素的href是个页面内地址，地址是有错误的区域；
在展示应用时，如果JS被关闭，客户端验证将不会出现。因此，这个技术只能在脚本依赖一致性的情况下才能够使用，或者当服务器端验证技术也同样用来获取错误和返回错误信息。
(8)当数据提交成功后，提供一个成功反馈。
为用户提供成功反馈，可以使用一致的反馈，如听觉和视觉一致性反馈，而不用用户再去导航发现；这个对于无法轻易扫描的行为结果的用户尤为重要。
样例1：
当用户登录到系统时，得到一个响应：“你已经成功登陆！”这样用户就不必再导航寻找自己已经登陆的标记，比如找到自己的用户名，或者登陆链接用注销链接所取代，寻找这些标记十分耗时间；
样例2：
用户填写问卷调查、测试然后提交。有个响应告知用户测试已经成功提交。所以他们不必去导航导数据区域，比如已提交测试列表，来确认测试提交；
样例3：
一名参观者创造一个网站上的帐户。提交表单后，反馈信息表明，“登记已成功提交......，”如果他们被自动记录在登记后，响应也说“......你已经登录。”如果需要确认，反馈包括信息，如“......一封电子邮件已经发送给你，你必须回复确认您的注册。”

样例4：
用户提交表单在说明帮助文档支持下。反馈表明，“该消息发送成功，您应该在48小时内收到回复。
4.错误预防（法律、金融、数据）
对于用户操作将引起法律承诺或者金融交易的网页、修改或删除数据存储系统里的用户可控数据的网页、提交用户测试响应的网页等 ，对于这些网页，以下部分至少有一为真：（AA级）1. 可逆: 提交是可逆的。2. 检查: 用户输入的数据将被检查是否有输入错误，并为用户提供一个改正错误的机会。3. 确认: 提供一个机制用于最后提交之前审查、确认和纠正信息。
(1)用户做了请求之后可以提供一个规定时间，允许用户来修改或取消该请求；
这个技巧允许用户在一定时间内检查错误并取消或更改请求；一般情况下，合同和订单都是法律协议，不能被取消。但是，网站可以选择去提供这种功能，提供一种方式让用户去修改错误；网也应该告知用户提交表单后多长时间内可以取消，取消的流程是怎样的。取消流程可能不能在线进行。比附，可能需要写一个通知到网页列表中的地址；提交表单之后，用户会被告知取消的时间长度以及取消的方法，最好是在提交表单的位置提供取消的流程，这样就会方便用户取消提交，为哪些不能使用其他机制的用户提供方便。但是，需要的话，取消流程可鞥通过其他机制，或者混合机制，只要它有等效的跨残疾无障碍。这样的事件中，用户会在提交表单前被警告，不能在线取消订单。
样例1：
在线购物网网站允许用户在24小时之内取消订单。网站会解释他们的政策，包括给用户发送购买收据的政策总结。24小时后，订单将会被锁定，不能被修改。
样例2:
定制订单：一个卖定制运动衬衣的网站需要下订单。消费者选择材料，提供尺码。网站会给消费者三天的时候更改会取消订单。一旦材料被裁剪，这个订单就不能更改和取消。公司的政策在网站上也有描述。
(2)在提交之前为用户提供复查更正答案的能力
这个技巧是让用户在完成不可逆转的交易之前保证自己的输入是正确的。测试、财政还有法律应用不允许出现取消交易。因此提交的数据的准确性是非常重要的，一旦交易被提交，使用者不会有机会去更正错误。
小例子：一页的表单在提交之前容易复查。如果一个表单包含很多歌网页，但是在交易确定之前，数据收集来自很多个步骤。用户不可能对如此多的步骤的所有数据复查。
一个方法是缓存每一步的结果，允许用户来回查看已输入的数据。另一个方法是提供一个多有已输入数据的总结。在交易提交和确认之前，说明应该提供去督促用户复查输入，一旦用户确认，交易完成。
样例1：
一个在线银行应用提供很多步骤去完成转账：选择转出账户、选择转入账户、输入转账金额；
样例2：
交易总结来显示余额和转账金额。用户可以选择按钮或者其他操作来完成交易或取消。
样例3：
测试应用提供了很多页的问题，任何时候，用户都可以选择返回前面的已将完成的部分去复查和修改答案。最后一页提案能一个按钮来提交或者修改答案。
(3)在提交按钮之外提供一个复选框
在用户提交之前，提供给用户一个复选框，用户必须选择已经复查过输入，准备好确认了。这对交易来说很重要，因为如果输入错误被发现或者数据被错误删除，将是不可逆转的。这个复选框可以有“我确认输入是正确的而且准备好提交”“我确认我要删除这个数据”。这个复选框应该在提交按钮附件，让用户在提交的时候注意到。当用户提交时，如果复选框没有被选中，提交是拒绝的，用户建议去复查输入，选择复选框再去提交。只有在复选框选中，提交才会被接收，交易才可以进行。
注意：当用户在没有选择复选框时提交信息，当用户重新提交的时候，用户输入的信息应该保留。
样例1：
在线银行服务允许用户在不同的货币帐户之间转移资金。因为汇率在不停的波动，如果用户发现输入错误在交易进行之后，是不能以相同汇率转账的。除了转出账户、转入账户、金额之外，需要有一个标签为“我已经确认转账信息”的复选框。当用户提交的时候，复选框没有被转红，交易不能进行，用户将会被告知。如果复选框已经选择了，不可逆转的交易将会进行。
样例2：
在线支付系统会存储用户银行信息去支付。用户需要一个可阐述流程来输入新的账户，并确认自己是拥有者。提供便利删除旧账户，但是如果账户被偶然删除，将会很难恢复，交易历史也会丢失。因此，网页允许用户删除账户，且有一个复选框“我确认删除账户”。如果用户提交时没有选择复选框，账户不会被删除，用户会受到错误信息。只有当复选框被选中时，账户才能删除。
样例3：
购物网站的结算表单包括一个收集订单、发货和账单信息的表单。提交表单之后，用户会跳转到一个有提交信息汇总的网页，用来复查提交信息；在汇总以下，有一个复选框带有“我已复查且确认数据正确”。用户必须标记复选框，激活完成订单按钮来完成订单。
(4)提供一种机制恢复删除信息
当web应用提供删除信息功能，服务器可以提供一种方式来恢复被用户错误珊瑚的信息。一个方法是通过标记延迟数据的删除或者将数据转移到一个隐藏的区域等待一段时候真正删除。在此期间，用户可以请求数据重新存储或者从隐藏区域恢复。另一个方法是记录所有的删除交易，这样用户可以恢复数据，比如维基百科会保存编辑历史。存储可恢复的信息，用户应该可以选择要保存或更正的版本。
样例1：
一个web应用允许用户设置文件夹来保存数据。每一个文件夹和数据条目需要一个复选框能来标记行为，两个按钮来移动和删除。如果用户选择错误的选择了删除按钮，数据将会丢失。应用将会显示数据已经删除，但是设定它一周后真正删除。在这一周的时间内，用户可以到删除条目请求文件夹和数据来恢复。
(5)请求确认继续进行已选择的操作
这个技巧为用户的可能操作寻求确认。在操作不能取消的情况下，适用这个技巧。这个会帮助用户避免错误提交表单和删除数据。确认请求应该会告知用户已选择的操作和操作会带来的结果。
样例1：航空旅行
航空旅行允许用户创建旅游行程，将会在不容航线里预留座位。用户可以查找、修正和取消当前的行程、如果用户需要取消旅行计划，找到网页中的行程并从当前行程列表里删除就可以了。这个操作的结果是预留的座位不能恢复。用户将会被告知当前的草错将会取消当前的预留操作，如果选择该操作，将不能在想听的飞机上订位置。用户将会要求去确认和取消行程的删除。
样例2：
一个Web邮件应用将用户的邮件存储在服务器上，这样用户就可以随时随地登陆查看邮件，当用户删除一个邮件，这个邮件会被移动到垃圾箱，如果是错误删除的话可以被恢复。有一个清空垃圾箱的命令可以删除垃圾箱中的所有信息从服务器的垃圾箱文件夹中。一旦垃圾箱文件被删除，信息不能再恢复，在清空垃圾箱之前，用户应该被询问是不是真的要删除垃圾箱。
样例3：在线测试
一个用来收集答案的表单。当提交和重置按钮被选择时，用户将会跳转到一个网页，这个网页将会告知用户的选择以及需要确认才能继续。比如：你已经选择重置表单，这会删除所有刚刚输入的数据而且不会提交任何答案，你确定要重置吗，YES No。你已经选择提交表单，这会作为你的最终答案被提交且不能更改，你确定要提交吗？YES No
样例4：买卖股票
某券商网站允许用户购买和出售股票和其他证券。如果用户在交易时段进行交易，呈现一个对话框，告知该交易是直接的，不可逆的，并且具有“继续”按钮和“取消”按钮。
5.帮助:上下文相关的帮助是可用的
(1)在每一个web页面上提供一个帮助链接
当用户输入数据时，这个技巧在每个网页上用来提供敏感信息帮助。另一个方法是为每一个交互控件提供帮助链接。将这个帮助链接置于控件之前或之后，如果用户对控件有问题，允许用户容易的tab到。在新窗口打开帮助信息要保证已经输入的数据不会丢失。
样例1：帮助链接
关键代码：```<a href="help.html" target="_blank">帮助</a></label>```
全部代码：
```<form action="test.html">
<label for="test">测试空间
<a href="help.html" target="_blank">帮助</a></label>
<input type="text" name="test" id="test" />
</form>```
(2)在网页上使用助手提供帮助
这个技巧主要是使用多媒体虚拟形象在网页中提供帮助。虚拟形象可以帮助无法阅读文字的认知障碍群体，使用视觉可以将人们的注意力集中到显示的材料上。
样例1：
在线银行在首页嵌入一个虚拟形象Vanna，她给在线银行客户提供应用特点的解说。这个助手可以打开和关闭暂停。客户可以重看和快速浏览。信息的替代文本可以从虚拟形象旁边的链接里获得。
样例2：
在志愿者网站有一个志愿者欢迎页面。在里面有一个申请表，在页面右侧还有一个虚拟形象的多媒体交互文件，这个交互会解释申请表的特点和章节。
(3)提供拼写检查和文本输入建议。
这个技巧提供拼写检查和文本建议。认知障碍群体有拼写障碍，但是可以给出近似的拼写。拼写检查程序将会保存他们是怎样拼写单词的。盲人或者低视力者在输入时会发生错误。这也会帮助使用头点式的肢体残疾。拼写检查提供使用建议和样例，可以选择并输入，为用户提供重要帮助；
样例1：
搜索引擎有一个搜索的表单，当表单提交时，服务器端的应用就会检查拼写。如果没有匹配的拼写，将会返回一个页面，这个页面在顶部说“你想要。。。”，同时有一个建议文字的链接。如果用户点击链接，建议条目会被输入到表单重新提交。
样例2：
航线有一个在线购买应用。当用户输入一个城市的名字，下拉列表中会显示出与输入最相近的城市。
(4)在表单区域起始部分提供文本说明来描述必要输入
这个技巧通过在表单顶部告知用户必须输入的数据格式来帮助用户避免错误。说明需要在表单顶部提供。这个技巧适用于小数目的表单或者很多要求相同数据格式输入的表单。在这种情况下，在表单顶部的说明里一次性的描述格式比多次重复想听信息更有效率。
样例1：
一个商业网站允许用户描述自己的工作，这个表单要收集的信息包括公司名、职位、工作事件、工作描述。在表单顶部的说明：
请输入你想要加入到简历中的个人工作信息。日期应该是月/日/年，这样的格式。
样例2：
公司通讯录可以让用户通过编辑配置为自定义信息，如电话号码和工作职责，在表单顶部有如下说明：您可以修改在表单中任何信息。当您选择完成，您的更改将被保存，你将有机会发表您的个人资料。如果你不想要保留更改，请选择取消按钮。您无法编辑系统显示的个人资料（即不包含在一个字段）。此信息是从人力资源部门获得的。如果你发现了一些不正确或过期，选择旁边的帮助信息图标，以了解如何改正。只是 - 电话号码可能包含数字和破折号（）。必填字段标有星号（*），并必须填写填写表格。
(5)提供期待数据的格式和样例
(6)使用title属性提供上下文敏感帮助
这个技巧为用户提供上下文敏感帮助，当用户输入数据时使用title属性提供帮助信息。帮助应该包括格式信息和输入样例。
样例1：
一个地图应用提供一个表单，包含一个地址的标签，一个输入框和一个value值为找到地图的提交按钮。输入框有一个title属性，内容时用户应该输入的地址样式：
```<label for="searchAddress">地址: </label>
<input id="searchAddress" type="text" size="30" value="" name="searchAddress" ```
 title="地址例如：101的柯林斯街，墨尔本，澳大利亚" />

样例2：
一个表单允许用户在线支付，但是要求用户输入账号。输入框与账号标签联系在一起，输入框有一个title属性提供账号的位置。
```<label for="accNum1">账号: </label>
<input id="accNum1" type="text" size="10" value=""``` title="您的帐号可以在您的账单上右上角找到." />
6.错误预防（全部）
对于要求用户提交信息的网页，以下部分至少有一为真
1. 可逆: 提交是可逆的。
2. 检查: 用户输入的数据将被检查是否有输入错误，并为用户提供一个改正错误的机会。
3. 确认: 提供一个机制用于最后提交之前审查、确认和纠正信息。

