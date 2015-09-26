
# （一）web端控件的无障碍问题



# 1.1图片<img>



### 1.1.1装饰性图片未能被辅助技术忽略

【问题描述】＜br/＞
　　纯装饰性图片应该能够被辅助技术所忽略，当用户使用屏幕阅读器浏览页面时，不会浏览到它们，提高浏览效率。装饰性图片（如背景图）未能被辅助技术忽略；＜br/＞
【可能原因】＜br/＞
【修改建议】＜br/＞
样例1：
将图片设置为背景图片：＜br/＞
```
CSS:
#bgimg
{
    background-image: url(img/demo.jpg);
}
HTML:
<div id="bgimg"></div>```
样例2：＜br/＞
将图片的tabindex属性设置为-1；（此条仅适用于删除具有焦点的图片访问。）＜br/＞
```
<img tabindex="-1" src="img001.gif" />```
样例3：＜br/＞
当图片没有title属性且alt属性值为空时，可被屏幕阅读器忽略。＜br/＞
```
<img src="squiggle.gif" alt="" />```

### 1.1.2非装饰性图片无替代文本


【问题描述】＜br/＞ 
　　对于非装饰性图片，应该添加正确的替代文本，用以说明图片所展示的内容，否则用户将无法了解到图片所要传递的信息。＜br/＞
　　使用 alt 属性为图片添加替代文本。如果图片展示包含理解网页重要信息的文字，alt属性应该添加这些字。alt不一定要描述图片的视觉特性，但是必须与图片传达的含义相同。＜br/＞
【可能原因】＜br/＞
【修改建议】＜br/＞
样例1：
为图片链接添加 ALT 属性：＜br/＞
```
<a href="home.html">
<img src="house.gif" alt="无障碍主页">去到无障碍主页</a>```
样例2：＜br/＞
为网页中的照片，添加详尽的描述文本；＜br/＞
```
<img alt="信息无障碍联盟LOGO" src="img001.gif" />```


## 1.2链接<a> 



### 1.2.1链接无键盘焦点


【问题描述】＜br/＞
　　链接应该具有键盘焦点，当按键盘TAB键移动焦点时，链接可被变历到。如果链接不能通过键盘变历到，用户则无法通过TAB键访问到链接内容，因而可能会影响到用户下一步操作。＜br/＞ 
【可能原因】＜br/＞
使用JS脚本来改变链接样式，导致链接无焦点，建议采用标准CSS样式；＜br/＞
【修改建议】＜br/＞

### 1.2.2链接无目的文本


【问题描述】＜br/＞
　　链接的目的文本用以说明链接的目的导向。用户通过屏幕阅读器获取链接的目的文本，从而了解链接作用。＜br/＞
【可能原因】＜br/＞
【修改建议】＜br/＞
样例1：
为链接添加目的描述文本：＜br/＞
```
<a href="routes.html">无障碍路线</a>```
样例2：
图片链接，图片无意义，可为img元素添加alt属性来描述链接目的：＜br/＞
```
<a href="routes.html"> <img src="topo.gif" alt="去到无障碍论坛的路线" /></a>```
样例3：
图片和文字链接，图片无意义：＜br/＞
```
<a href="routes.html">
<img src="topo.gif" alt="" />去到无障碍论坛的路线
</a>```
样例4：
图片和文字链接，图片有意义：＜br/＞
```
<a href="prod_123_feedback.htm">反馈
<img src="response.gif" width="15" height="15" alt="收到响应图标" />
</a>```
样例5：
链接到文件（pdf、doc、xls）：＜br/＞
```
<p>
<a href="2009mycorp_report.pdf">信息无障碍联盟年度报告（pdf）</a>
<br />
<a href="2009mycorp_budget.xls">信息无障碍联盟年度财务 (Excel)</a>
</p>```
样例6：
使用 title 属性添加链接文本：
title属性用已描述链接目的：＜br/＞
```
<a href="index.html" title="了解更多无障碍研究会的内容">无障碍研究会</a>```
Title用来描述新窗口打开方式：＜br/＞
```
<a href="http://www.siaa.org.cn/" target="_blank"  title="在新窗口中打开"> </a>```
样例7：
给列表内链接添加描述文本，用已描述链接目的。＜br/＞

```
<ul>
<li>
<a href="tomb_raider.htm">视障工程师王</a>
<a href="tomb_raider_images.htm">链接目的文本</a>
<a href="tomb_raider.mpeg">下载demo</a>
</li>
<li>
<a href="fear_extraction.htm">视障工程师朱</a>
<a href="fear_extraction_images.htm">看图片</a>
<a href="fear_extraction.mpeg">下载demo</a>
</li>
<li>
<a href="call_of_duty.htm">视障工程师刘</a>
<a href="call_of_duty_images.htm">See 看图片</a>
<a href="call_of_duty.mpeg">下载demo</a>
</li>
<li>
<a href="Warhammer 40K.htm">视障工程师沈</a>
<a href="warhammer_40k_images.htm">看图片</a>
<a href="Warhammer_40k.mpeg">下载demo</a>
</li>
</ul>```   
样例8：
使用链接文本为链接添加目的描述：＜br/＞
```
<h3>互联网产品信息无障碍</h3>
<p>互联网产品信息无障碍大意是，互联网产品可以被视障者等用户顺畅使用...<a href="final15.html">[查看更多]</a></p>
<h3>Folk artists get awards</h3>
<p>从即将到来的全国民俗节表演者收到国家文物奖学金。<a href="nheritage.html">[更多]</a></p>```
更多链接添加 title 属性，会描述的更清楚；＜br/＞
样例9：
为表格内链接添加目的文本：＜br/＞
```
<tr>
<th scope="row">经济车</th>
<td>
<a href="econ_ala.htm">$67/天</a>
</td>
<td><a href="econ_bud.htm">$68/天</a></td>
<td><a href="econ_nat.htm">$72/天</a></td>
<td><a href="econ_av.htm">$74/天</a></td>
<td><a href="econ_hz.htm">$74/天</a></td>
</tr>```
样例10：
链接文本为父级内容添加链接目的：＜br/＞
```
<li>年度报告2005-2006
<ul>
<li>
<a href="annrep0506.html">(HTML)版</a>
</li>
<li>
<a href="annrep0506.pdf">(PDF)版</a>
</li>
<li>
<a href="annrep0506.rtf">(RTF)版</a>
</ul>
</li>```

### 1.2.3链接不能响应回车键


【问题描述】 ＜br/＞
　　使用键盘对链接进行点击操作，是使用按下回车键（enter）来完成的。如果链接不能响应回车键的点击操作，用户将无法使用键盘来激活这个链接。
onclick 属性由元素上的鼠标点击触发。onclick 事件会在对象被点击（click事件完成）时发生，是一个click事件的监听器，监听到点击后，执行对应Js代码。
请注意， onclick 与 onmousedown 不同。单击事件是在同一元素上发生了鼠标按下事件之后又发生了鼠标放开事件时才发生的。通过使用anchors（锚点）和buttons的onclcik事件使键盘可用对于HTML标准控件links和buttons来说，默认可以通过鼠标点击，和按enter键来实现。＜br/＞
【可能原因】＜br/＞
【修改建议】＜br/＞
样例1：链接onclick事件：＜br/＞
```
<a href="#" onclick="无障碍弹窗;">无障碍</a>```


## 1.3编辑框



### 1.3.1控件类型提示不正确


【问题描述】＜br/＞
　　当控件获得焦点时屏幕阅读器不能准确的提示此控件是编辑框， 用户无法确定应该如何操作此控件；＜br/＞
【可能原因】＜br/＞
控件类型提示不正确的情况存在于自绘控件；＜br/＞
【修改建议】＜br/＞
方案1：
使用html标准控件元素，为网页添加编辑框;＜br/＞
 ```
 <input type="text" title="视障工程师名字" size="20" />```
方案2：
为自定义编辑框添加 role 属性，让屏幕阅读器提示为编辑框，用户可对编辑框正确操作。
role="textbox"代表是一个编辑框， 自绘的编辑框加上role="textbox"属性，屏幕阅读器就会提示用户这是一个编辑框。＜br/＞


### 1.3.2编辑框无法用键盘访问与操作


【问题描述】＜br/＞
用TAB键或Shift+TAB键在网页上浏览，编辑框控件无法获得键盘焦点。＜br/＞
【可能原因】＜br/＞
（1）所有可获得焦点的元素 tabindex属性应为"0"＜br/＞
 ```
 <input type="text" title="视障类型" size="20" tabindex="0" />```
（2） 使用了自绘的编辑框＜br/＞
【修改建议】 ＜br/＞
方案1：
使用html标准控件；＜br/＞
```<input type="text" title="输入视障工程师年龄" tabindex="0" />```
方案2：＜br/＞
将控件的contenteditable设为true，tabindex 属性设为"0"；＜br/＞


### 1.3.3编辑框无目的提示


【问题描述】＜br/＞
编辑框缺少提示文本，用户难以理解此编辑框输入哪种类型的信息；＜br/＞
【可能原因】＜br/＞
没有用title、label或其他方式给编辑框添加目的描述文本；＜br/＞
【修改建议】 ＜br/＞
当需要用户输入内容时，要给出标签或说明：为交互组件提交必要的目的说明，说明信息输入的必要性。＜br/＞
方案1： 
给控件添加title来说明编辑框的目的：＜br/＞
```<input title="请输入信息无障碍产品联盟网址" type="text" size="20" tabindex="0"/>```
方案2： 
使用 label 为编辑框添加标签，让用户正确判断需要在编辑框内录入哪种类型的数据；＜br/＞
```<label for="name">联盟网址：</label>
<input type="text" id="name" tabindex="0"/>```
方案3： 
使用aria-describedby属性为编辑框关联提示文本；＜br/＞
注： 此方法国内的一些屏幕阅读器可能暂时不支持＜br/＞
```<div id="container">
<h1>web端信息无障碍</h1>
<h2>移动端信息无障碍</h2>
<div>
<label for="first">名:</label>
<input type="text" id="first" name="first" size="20"
      aria-describedby="tp1"
      aria-required="false"/>
<div id="tp1" role="tooltip" aria-hidden="true">无障碍工具可选</div>
</div>```
方案4：
使用aria-labelledby连接一个标签和多个文本节点，应用与输入控件，aria-labelledby可以被用于label本地输入和非本地输入，例如contenteditable="true"的自定义输入控件div;aria-labelledby的一个特殊使用是文本输入控件，当一个有意义的标签应该包含多个label；id顺序应该是有逻辑的能被读屏软件读取的顺序；＜br/＞
一个连接超时输入字段标签：＜br/＞
```<form>
<p>
<span id="timeout-label" tabindex="-1">
<label for="timeout-duration">延长时间到</label>
</span>
<input type="text" size="3" id="timeout-duration" value="20" 
    aria-labelledby="timeout-label timeout-unit">
<!--timeout-label包含label， timeout-duration为label的id; timeout-unit是个span元素的id；-->
<span id="timeout-unit" tabindex="-1">分钟</span>
</p>		
</form>```
方案5：
placeholder 属性提供可描述输入字段预期值的提示信息（hint）。该提示会在输入字段为空时显示，并会在字段获得焦点时消失。＜br/＞
注释：placeholder 属性适用于以下的 <input> 类型：text, search, url, telephone, email 以及 password。＜br/＞
```<form action="demo_form.asp" method="get">
输入要搜索的工程师名字
  <input type="search" name="user_search" placeholder="输入要搜索的工程师名字" />
  <input type="submit" value="搜索"/>
</form>```

### 1.3.4预设文本无法用键盘清除


【问题描述】＜br/＞
编辑框内有预先设定的文本， 用backspace键不能删除编辑框内的预设文本，只能用鼠标删除。＜br/＞
【可能原因】＜br/＞
自绘的编辑框控件没有对backspace键或所有键盘操作进行支持。＜br/＞
【修改建议】＜br/＞
方案1：
将自绘控件的contenteditable属性设为true， 然后在自绘编辑框的键盘事件处理代码中支持backspace删除文本；＜br/＞
方案2：
使用placeholder属性设置编辑框的预设文本；＜br/＞
```<form>
无障碍搜索
<input type="text" placeholder="信息无障碍研究会" tabindex="0"/>
</form>```

### 1.3.5焦点进入编辑框，焦点无法移出


【问题描述】＜br/＞
键盘用户使用TAB键或TAB+Shift键进入编辑框内后无法用TAB或Shift+TAB键把焦点离开编辑框；＜br/＞
【可能原因】＜br/＞
自绘控件没有对TAB键进行支持或对TAB键做了支持但形成了键盘陷阱（就是焦点跳转形成一个死循环， 无法用TAB跳转出循环区域）；＜br/＞
【修改建议】＜br/＞
方案1： 使用标准控件＜br/＞
```<input type="search" title="请输入无障碍内容" tabindex="0"/>```
方案2： 在自绘编辑框的键盘处理事件代码中对tab键进行支持＜br/＞
方案3： 避免键盘陷阱＜br/＞
　　保证键盘用户不会陷入子集出不来，这些子集仅在使用鼠标和点触设备时可用。最常见的是插件，如果插件可以获得焦点，但是没 有提供可以跳出插件将焦点返回父窗口的机制，插件就会成为陷阱。编辑框内无法用tab键跳出也是此问题。＜br/＞
使用以下机制可以有效避免该陷阱：＜br/＞
1.事先定义好内容焦点（通常使用tabindex），当子集或插件导航到最后位置时，跳出子集或插件，事先定义好的焦点可以获得。＜br/＞
2.定义键盘事件，将焦点移出子集内容。＜br/＞
3.如果子集使用的技术里面包含回到父级的键盘命令，在用户进入该子集前提示用户该命令。＜br/＞


## 1.4列表



### 1.4.1列表无键盘焦点


【问题描述】＜br/＞
用TAB或Shift+TAB在网页上浏览，列表无法获得焦点；＜br/＞
【可能原因】＜br/＞
(1) <select>标签的tabindex属性的值被设置为："-1"＜br/＞
(2) 使用自绘控件作为列表且没有添加tabindex属性＜br/＞
【修改建议】＜br/＞
方案1：
使用html标准控件并把tabindex属性设置为适当的值；＜br/＞
```<select tabindex="0" title="信息无障碍项目列表">
<option>手机qq android项目</option>
<option>手机qq ios项目</option>
<option>手机淘宝无障碍项目</option>
</select>```
方案2：
将自绘列表的tabindex属性设置为0；＜br/＞

### 1.4.2键盘焦点进入后无法移出列表


【问题描述】＜br/＞
用tab或shift+tab浏览到列表内后无法用tab或shift+tab跳出列表＜br/＞；
【可能原因】＜br/＞
自绘列表控件没有对TAB键做支持或支持出现问题导致陷入键盘陷阱；＜br/＞
【修改建议】＜br/＞
方案1： 自绘列表控件在键盘处理事件代码中对tab键进行支持；＜br/＞
方案2： 避免键盘陷阱；＜br/＞
使用以下机制可以有效避免该陷阱：＜br/＞
1.事先定义好内容焦点（通常使用tabindex），当在列表中用tab浏览时跳出列表，事先定义好的焦点可以获得。＜br/＞
2.定义键盘事件，将焦点移出列表内容。＜br/＞
3.如果列表使用的技术里面包含回到父级的键盘命令，在用户进入该列表前提示用户该命令。＜br/＞

### 1.4.3方向键无法在列表项中移动


【问题描述】＜br/＞
用tab或shift+tab浏览到列表后不能用方向键在列表项之间移动；＜br/＞
【可能原因】＜br/＞
【修改建议】＜br/＞


### 1.4.4列表项<option>无提示文本


【问题描述】＜br/＞
用方向键在列表项目之间移动的时候列表项没有提示文本；<br/>
【可能原因】＜br/＞
1、 列表的<option></option>之间没有文本；<br/>
2、 <option>之内添加了图片，但没有给图片添加替代文本；<br/>
3、 自绘列表没有给列表项文本提示；<br/>
【修改建议】<br/>
方案1: 
给option之内添加文本<br/>
```<select title="无障碍bug严重程度" tabindex="0">
<option>致命</option>
<option>严重</option>
<option>一般</option>
<option>提示</option>
<option>建议</option>
</select>```
方案2：
当列表项为图片时，使用alt属性提供替代文本；<br/>
注： 经过测试此方法不能朗读， 暂时没有找到一种方法能朗读。<br/>
方案3：
自绘列表的列表项提供文本或替代文本；
<br/>

### 1.4.5列表项选择后页面刷新导致当前控件焦点丢失


【问题描述】<br/>
当选择了列表中的某一个列表项后网页进行刷新， 刷新后焦点已经不在此列表处了；<br/>
【可能原因】<br/>
刷新网页后没有把焦点设置到刷新之前的位置；<br/>
【修改建议】<br/>
刷新后把焦点设置到刷新之前的位置；<br/>


### 1.4.6控件类型朗读不正确


【问题描述】<br/>
当此控件获得焦点的时候屏幕阅读器朗读的控件类型与实际不符，导致用户无法确定如何操作此控件；<br/>
【可能原因】<br/>
自绘的列表没有提供一种方式告诉屏幕阅读器此控件的类型；<br/>
【修改建议】<br/>
方案1：
使用html标准控件；<br/>
```<select title="无障碍测试报告" tabindex="0">
<option>手机qq无障碍测试报告</option>
<option>手机淘宝无障碍测试报告</option>
<option>手机qq轻聊无障碍测试报告</option>
<option>支付宝无障碍测试报告</option>
</select>```
方案2：
使用aria的role属性来告诉屏幕阅读器此控件的类型， role="combobox"表示下拉列表框、role="option"表示选项、role="listbox"表示列表框。<br/>
注： 下面的代码只展示了如何让屏幕阅读器知道自绘控件是一个列表，但不是一个完全无障碍支持的自绘列表的代码。<br/>
```<label for="cb1-list">视障工程师列表</label>
<ul id="cb1-list" tabindex="0" role="listbox" aria-expanded="true">
    <li id="cb1-opt1" role="option">一同</li>
    <li id="cb1-opt2" role="option">槐荫飞龙</li>
    <li id="cb1-opt3" role="option">铁箸书生</li>
</ul>```

## 1.5复选框checkbox



### 1.5.1复选框控件类型朗读不正确


【问题描述】<br/>
复选框类型朗读错误，例如打开复选框，朗读成，打开按钮；<br/>
【可能原因】<br/>
自定义的控件没有提供控件类型说明；<br/>
【修改建议】<br/>
样例1：
使用html标准控件；<br/>
 ```<input type="checkbox" title="qq项目" tabindex="0"/>qq项目```
样例2：
自绘控件使用aria的role属性描述控件类型， role=”checkbox”表示复选框；<br/>
```<div tabindex="0" role="checkbox">淘宝项目</div>```
注： 此代码只提示控件类型并不是一个完整的无障碍自绘复选框的代码， 因为选中状态不能朗读。<br/>

### 1.5.2复选框无法获得键盘焦点


【问题描述】<br/>
用tab键，无法定位到复选框；<br/>
【可能原因】<br/>
1、 标准控件的tabindex属性的值设置为-1；<br/>
2、 没有给自定义的复选框设置tabindex属性；<br/>
【修改建议】<br/>
样例1：
使用html标准控件，  且tabindex属性的值不能为-1；<br/>
``` <input type="checkbox" tabindex="0" title="支付宝项目" />支付宝项目```
样例2：
自绘控件将控件的tabindex属性设为0；<br/>
```<div tabindex="0" role="checkbox">pc qq项目</div>```
注： 此代码只提示控件类型和获得焦点并不是一个完整的无障碍自绘复选框的代码， 因为选中状态不能朗读。<br/>

### 1.5.3复选框无法响应空格选中或取消选中


【问题描述】<br/>
tab定位到复选框后，无法用空格选中或取消选中该复选框；<br/>
【可能原因】<br/>
自定义控件没有提供键盘处理事件；<br/>
【修改建议】<br/>
样例1：
使用html标准控件；<br/>
``` <input type="checkbox" title="工程师名字" tabindex="0"/>工程师名字```
样例2：
为控件添加空格点击响应事件；<br/>
```<html>
<head>
<title>test</title>
<script>
function setstate(id){
if(event.keyCode!==32) return false;
var obj=document.getElementById(id);
if(obj.getAttribute("aria-checked")=="false")
obj.setAttribute("aria-checked","true");
else
obj.setAttribute("aria-checked","false");
}
</script>
</head>
<body>
<div>
<ul>
<li tabindex="0" onkeydown="setstate('chk');" role="checkbox" aria-checked="false" id="chk" />
<label for="chk">正在测试的项目</label>
<li tabindex="0" onkeydown="setstate('chk2');" role="checkbox" aria-checked="false" id="chk2" />
<label for="chk2">完成测试的项目</label>
<li tabindex="0" onkeydown="setstate('chk3');" role="checkbox" aria-checked="false" id="chk3" />
<label for="chk3">回归测试的项目</label>
</ul>
</div>
</body>
</html>```

注： 上面的代码添加了键盘处理事件， 键盘处理事件里面改变aria-checked的属性值， 在实际应用中开发者可以根据实际需要修改键盘事件代码。<br/>

### 1.5.4复选框无提示文本


【问题描述】<br/>
tab定位到复选框，辅助程序不朗读是什么复选框；<br/>
【可能原因】<br/>
没有用label、title或其他方式提供目的文本；<br/>
【修改建议】<br/>
样例1：
为复选框选项添加label;<br/>
```<input type="checkbox" id="checkbox" tabindex="0"/>
 <label>已经回归的项目</label>```
注： 1、 label必须在checkbox的后面；2、此种方法对nvda无效， 争渡和永德读屏有效。<br/>
样例2： 
添加title来说明checkbox的目的；<br/>
```<input type="checkbox" tabindex="0" title="已经解决的bug"/>已经解决的bug；```
注： title的值应该与视觉所见的文本一致。<br/>
样例3： 
用label标签把checkbox包起来；<br/>
```<label><input type="checkbox" >qq project</label>```
样例4：
使用label 的for属性为复选框链接提示文本；<br/>
``` <input type="checkbox" id="checkbox" tabindex="0"/>
<label for="checkbox">未解决的bug</label>```
注： label标签的for属性的值必须与checkbox的id属性的值一致。此种方法label放在什么地方都没有问题。<br/>
样例5：
使用aria-label为复选框添加提示文本；<br/>
```<input type="checkbox" tabindex="0" aria-label="结束的项目"/>结束的项目```
样例6：
使用aria-describedby为复选框提供提示文本<br/>
 ```<input type="checkbox" tabindex="0" aria-describedby="label"/>
<div id="label">male</div>```
注： 国内的一些读屏可能暂时不支持aria-describedby<br/>

### 1.5.5勾选后刷新，当前控件焦点丢失


【问题描述】<br/>
tab定位到复选框后，空格选中，页面自动刷新，焦点不会重新定位回该复选框；<br/>
【可能原因】<br/>
【修改建议】
<br/>
### 1.5.6选中和取消选中状态不朗读


【问题描述】<br/>
tab定位到该复选框后，不朗读复选框的选中状态；<br/>
【可能原因】<br/>
自定义的控件没有播报状态给读屏；<br/>
【修改建议】<br/>
样例1：
使用标准html控件；<br/>
``` <input type="checkbox" tabindex="0" title="项目名称"/>项目名称```
样例2：
自会控件role=checkbox的情况下，使用aria-checked属性；
aria-checked属性是true代表选中， 是false代表没有选中， 此选项应该用编程动态确定。<br/>
```<html>
<head>
<title>test</title>
<script>
function setstate(id){
if(event.keyCode!==32) return false;
var obj=document.getElementById(id);
if(obj.getAttribute("aria-checked")=="false")
obj.setAttribute("aria-checked","true");
else
obj.setAttribute("aria-checked","false");
}
</script>
</head>
<body>
<div>
<ul>
<li tabindex="0" onkeydown="setstate('chk');" role="checkbox" aria-checked="false" id="chk" />
<label for="chk">正在测试的项目</label>
<li tabindex="0" onkeydown="setstate('chk2');" role="checkbox" aria-checked="false" id="chk2" />
<label for="chk2">完成测试的项目</label>
<li tabindex="0" onkeydown="setstate('chk3');" role="checkbox" aria-checked="false" id="chk3" />
<label for="chk3">回归测试的项目</label>
</ul>
</div>
</body>
</html>```


### 1.5.7选中或取消选中后，没有及时读出选中状态


【问题描述】<br/>
tab定位到该复选框后，选中或取消选中，不会及时朗读选中状态，要重新定位回该焦点，才会朗读出选中状态；<br/>
【可能原因】<br/>
自定义复选框没有及时播报选中状态；<br/>
【修改建议】<br/>
样例1：
使用html标准控件；<br/>
```<input type="checkbox" tabindex="0" title="项目名称"/>项目名称```
样例2： 
使用编程是和aria-checked属性及时播报选中状态;<br/>
```<html>
<head>
<title>test</title>
<script>
function setstate(id){
if(event.keyCode!==32) return false;
var obj=document.getElementById(id);
if(obj.getAttribute("aria-checked")=="false")
obj.setAttribute("aria-checked","true");
else
obj.setAttribute("aria-checked","false");
}
</script>
</head>
<body>
<div>
<ul>
<li tabindex="0" onkeydown="setstate('chk');" role="checkbox" aria-checked="false" id="chk" />
<label for="chk">正在测试的项目</label>
<li tabindex="0" onkeydown="setstate('chk2');" role="checkbox" aria-checked="false" id="chk2" />
<label for="chk2">完成测试的项目</label>
<li tabindex="0" onkeydown="setstate('chk3');" role="checkbox" aria-checked="false" id="chk3" />
<label for="chk3">回归测试的项目</label>
</ul>
</div>
</body>
</html>```


## 1.6单选框



### 1.6.1单选框键盘无法获得焦点


【问题描述】<br/>
使用屏幕阅读器浏览网页，使用tab在网页内的控件间切换，tab找不到该单选框；<br/>
【可能原因】<br/>
自定义的单选框没有添加tabindex属性；<br/>
【修改建议】<br/>
样例1：
使用html标准控件；<br/>
```<fieldset>
<legend>搜索顺序</legend> 
<input type="radio" name="order" id="order_alpha" />
<label for="order_alpha">按字母排序</label>
<input type="radio" name="order" id="order_default" checked="true" />
<label for="order_default">默认</label>
</fieldset>```
样例2：
自绘控件时，将role设置为radio，且tabindex属性设为0；<br/>
 ```<div role="radio" tabindex="0">男</div>```

### 1.6.2无法使用方向键在单选框与单选框之间切换


【问题描述】<br/>
焦点到达单选框，用上下方向键无法改变单选按钮的选中状态；<br/>
【可能原因】<br/>
1、 一组标准控件单选框的name属性的值不一致；<br/>
2、 自定义单选框没有做光标在单选框之间选择的支持；<br/>
【修改建议】<br/>
样例1：
标准控件的单选框的一组的name属性的值设置为一致；<br/>
```<fieldset>
<legend>性别</legend> 
<input type="radio" name="order" id="order_alpha" />
<label for="order_alpha">男</label>
<input type="radio" name="order" id="order_default" checked="true" />
<label for="order_default" >女</label>
</fieldset>```
样例2：
自定义控件的单选框对上下光标选中单选框做支持；<br/>

### 1.6.3单选框无提示文本


【问题描述】<br/>
tab浏览到单选框或上下光标在单选框之间移动，不会朗读出这是什么单选框；<br/>
【可能原因】<br/>
 没有给单选框添加label、title或其他任何一种方式的提示文本；<br/>
【修改建议】<br/>
样例1：
为复选框选项添加label;<br/>
<fieldset>
```<legend>性别</legend> 
<input type="radio" name="order" id="order_alpha" />
<label >男</label>
<input type="radio" name="order" id="order_default" checked="true" />
<label >女</label>
</fieldset>```
注： 此种方式国内的读屏可以支持（争渡、永德）， 国外的读屏不大支持（nvda）<br/>
样例2：
使用label for属性为复选框链接提示文本；<br/>
```<fieldset>
<legend>性别</legend> 
<input type="radio" name="order" id="order_alpha" />
<label for="order_alpha">男</label>
<input type="radio" name="order" id="order_default" checked="true" />
<label for="order_default">女</label>
</fieldset>```
样例3： 
使用label把radio包起来<br/>
```<fieldset>
<legend>性别</legend>
<label><input type="radio" name="0"/>男</label>
<label><input type="radio" name="0"/>女</label>
</fieldset>```
样例4：
使用aria-label为单选框添加提示文本；<br/>
```<fieldset>
<legend>性别</legend>
男
<input type="radio" name="0" aria-label="男"/>
女
<input type="radio" name="0" aria-label="女"/>
</fieldset>```
样例5：
使用aria-describedby为单选框提供提示文本；<br/>
```<fieldset>
<legend>性别</legend>
<label id="male">男</label>
<input type="radio" name="0" aria-describedby="male"/>
<label id="femal">女</label>
<input type="radio" name="0" aria-describedby="femal"/>
</fieldset>```
注： 此种方式国内的读屏有可能不支持（争渡、永德）， 国外的读屏支持（nvda）<br/>

### 1.6.4焦点无法进入单选框


【问题描述】<br/>
Tab焦点进入单选框，焦点不停留，直接跳过单选框，进入下一个元素；<br/>
【可能原因】<br/>
【修改建议】<br/>

### 1.6.5控件类型朗读不正确


【问题描述】<br/>
控件类型朗读错误，例如男单选框，朗读成，男按钮；<br/>
【可能原因】<br/>
自定义的单选框没有播报控件类型；<br/>
【修改建议】<br/>
样例1：
使用html标准控件；<br/>
```<fieldset>
<legend>残疾类型</legend>>
<input type="radio" name="00" id="00"/>
<label for="00">盲人</label>
<input id="01" name="00" type="radio"/>
<label for="01">聋人</label>
<input id="02" name="00" type="radio"/>
<label for="02">肢残</label>
<input type="radio" id="03" name="00"/>
<label for="03">其他</label>
</fieldset>```
样例2：
自绘控件时使用aria中的role="radio"表示单选框；<br/>
role="radiogroup" 表示单选组
aria-checked 字符串。表示检查的状态。true表示元素被选择；false表示元素未被选择；mixed表示元素同时有选择和未选择状态。<br/>
```<h3 id="girl_label">视障工程师</h3>
<ul role="radiogroup" aria-labelledby="girl_label">
    <li tabindex="-1" role="radio" aria-checked="false">
        <img role="presentation" src="radio-unchecked.gif" />孟奇
    </li>
    <li tabindex="0" role="radio" aria-checked="true">
        <img role="presentation" src="radio-checked.gif" /> 广锐
    </li>
    <li tabindex="-1" role="radio" aria-checked="false">
        <img role="presentation" src="radio-unchecked.gif" /> 鸿利
    </li>  
</ul>```
注： 上面的代码书写上没有什么问题， 但是不读状态<br/>

## 1.7按钮、图片按钮



### 1.7.1按钮缺少目的文本


【问题描述】<br/>
由于按钮使用图片或某些特殊性标识符展现，屏幕阅读器无法读出按钮所展现内容，用户难以理解按钮本身所表达的意思，从而无法做出正确的操作。<br/>
【可能原因】<br/>
开发者使用一张图片或一个标识符来展现按钮的用途，屏幕阅读器无法读出图片中内容；<br/>
【修改建议】<br/>
给按钮添加易于理解的提示文本;<br/>
样例1：
给按钮添加目的文本；<br/>
```<button type="button">信息无障碍研究会</button>```
样例2：
使用title属性，给按钮添加目的文本；<br/>
```<button type="button" title="信息无障碍产品联盟"><img src="logo.jpg" alt=""></button>```
样例3：
使用 label 为按钮添加目的文本；<br/>
```<label for="btn-desc">视障工程师</label>
<button type="button" id="btn-desc"></button>```
样例4：
使用 alt 属性为图片按钮添加替代文本；<br/>
```<button type="button" ><img src="1.jpg" alt="信息无障碍研究会"></button>```
样例5：
使用 aria-describedby 为按钮提供详细信息；<br/>
```<p><span id="font-desc">选择该网页的字体大小</span>
<button type="button" id="font-b" onclick="doAction('Fonts');" aria-describedby="font-desc">字体</button>
</p>
<p><span id="color-desc">选择该网页的颜色</span>
 <button type="button" id="color-b" onclick="doAction('Colors');" aria-describedby="color-desc">颜色</button>
</p>
<p><span id="custom-desc">自定义此页面上使用的布局和样式</span>
 <button type="button" id="custom-b" onclick="doAction('Customize');" aria-describedby="custom-desc">自定义</button>
</p>```
样例6：
使用aria-describedby属性描述临近按钮元素的行为；<br/>
```<button type="button" aria-label="信息无障碍研究会" aria-describedby="description-close" onclick="myDialog.close()">按钮文本</button>
<!-- id为description-close的控件为button提供描述文本 -->
...
<div id="description-close">关闭此窗口将忽略输入的所有信息，并会返回到主页</div>```
样例7：
使用aria-describedby属性将说明与按钮联系起来；<br/>
```<form>
<label for="fname">名</label>
<input type="text" name="fname" id="fname" aria-describedby="int2">
<p id="int2">该区域使用aria-describedby关联说明文本。</p>
</form>```


### 1.7.2按钮无法获得键盘焦点


【问题描述】<br/>
使用屏幕阅读器浏览网页，无法聚焦到按钮上，导致无法操作；<br/>
【可能原因】<br/>
开发者为了让按钮更加美观，故意使用各类方式让按钮无法聚焦；<br/>
【修改建议】<br/>
样例1：
使用html标准元素添加按钮；<br/>
```<button type="button">视障工程师</button>```
样例2:
给自定义按钮添加role和tabindex属性；<br/>
```<span class="btn-close" tabindex="0" role="button" onclick="closeCurrentWindow()" onkeydown="if (event.keyCode == 13 || event.keyCode == 32) closeCurrentWindow();">关闭当前窗口</span>```

### 1.7.3控件类型朗读不正确


【问题描述】<br/>
自定义按钮，屏幕阅读器无法提示为“按钮”控件，使用屏幕阅读器用户无法对按钮做出正确的操作。<br/>
【可能原因】<br/>
自定义“按钮”缺少 role、tabindex 属性，导致屏幕阅读器无法聚焦到此元素且无法读出正确的控件类型。<br/>
【修改建议】<br/>
样例1：
使用html标准元素（button、input type=button/submit）给网页添加按钮;<br/>
```<form action="/login" method="post">
...
<input type="image" name="submit" src="button.gif" alt="登录" />
</form>```
样例2：
自定义按钮时，添加 role="button" 属性，让屏幕阅读器辨识；
如果输入控件的类型为图片，功能为提交，此时alt表明的是按钮的功能，不是描述图片。当界面上有很多提交按钮的时候，这个属性尤为重要。<br/>
role="button"表示把角色设置为按钮，屏幕阅读器可正确提示为按钮。<br/>
role="toolbar" 表示把角色设置为工具栏，屏幕阅读器会自动读出为工具栏。<br/>
aria-activedescendant表示后代的id值<br/>
```<div role="toolbar" tabindex="0" aria-activedescendant="btn1">
  <img src="123.jpg" id="btn1" role="button" alt="信息无障碍研究会" />
  <img src="456.jpg" id="btn2" role="button" alt="视障工程师" />
  <img src="def.jpg" id="btn3" role="button" alt="按钮3" />
</div>```


### 1.7.4按钮无法响应键盘点击


【问题描述】<br/>
按钮无法用键盘直接激活，导致无法执行按钮的命令；<br/>
【可能原因】<br/>
【修改建议】<br/>
样例1：submit 点击事件
<form action="/login" method="post">
...
<input type="submit" value="登录" />
</form>
样例2：图片按钮点击事件：<br/>
```<input type="image" src="example.gif" alt="关闭" onclick="closePopWnd()" keydown="if (event.keyCode == 13) closePopWnd();" />```
样例3：Button onclick事件:<br/>
```<button type="button" onclick="closePopWnd()"><img src="btn-closepopwnd.gif" alt="关闭"></button>```
样例4：为按钮添加键盘空格点击事件；<br/>
```<div role="button" tabindex="0" onclick="closePopWnd()" onkeydown="if (event.keyCode == 13 || event.keyCode == 32) closePopWnd();">关闭</div>```

### 1.8菜单



### 1.8.1控件类型朗读不正确


【问题描述】<br/>
屏幕阅读器用户通过反馈的控件类型来确定这个控件应该如何操作，如菜单则说明执行一条命令，菜单栏则可以进行展开折叠动作来显示隐藏菜单项，因此，设置错误的控件类型会导致用户无法判断控件应该如何操作<br/>。
【可能原因】<br/>
【修改建议】<br/>
样例1：自定义菜单控件使用role=”menu”属性<br/>
role="menu"表示菜单<br/>
role="menubar"表示菜单栏<br/>
role="menuitem"表示菜单项<br/>
 role="menuitemradio"表示只能单选的菜单项 <br/>
```<ul role="menubar" title="视障工程师菜单">
  <li role="menuitem" tabindex="0" aria-haspopup="true">视障工程师
    <ul role="menu" aria-hidden="true">
      <li role="menuitemradio"  aria-checked="true">王孟琦</li>      <li role="separator">朱广锐</li> 
      <li role="menuitemradio" aria-checked="false">刘彪</li>
      <li role="menuitemradio"aria-checked="false">李鸿利</li>
    </ul>
  </li>
  <li role="menuitem" aria-haspopup="false">信息无障碍深圳</li>
  <li role="menuitem" aria-haspopup="false">信息无障碍北京</li>
  <li role="menuitem" aria-haspopup="false">信息无障碍上海</li>
</ul>```


### 1.8.2折叠/展开无法用键盘操作


【问题描述】<br/>
屏幕阅读器的用户一般通过键盘导航来对控件进行操作，如果控件不能支持用户的键盘操作，将导致使用屏幕阅读器的用户无法操作这个控件。<br/>
【可能原因】<br/>
【修改建议】<br/>
样例1： 使用keydown事件使回车键可以展开、折叠菜单。 <br/>


### 1.8.3折叠/展开状态无提示


【问题描述】<br/>
屏幕阅读器的用户通过反馈得知菜单是否折叠展开来确定是否子菜单项是否可以访问，是否需要改变当前菜单的折叠状态，如果不能提示菜单的折叠状态，将对用户产生困扰。<br/>
【可能原因】<br/>
【修改建议】<br/>
样例1：
添加aria-expanded属性，字符串。表示展开状态。默认为undefined, 表示当前展开状态未知。其它可选值：true表示元素是展开的；false表示元素不是展开的。<br/>
```<ul role="menu" aria-hidden="true" aria-expanded="false" >
      <li role="menuitemcheckbox" tabindex="-1" aria-checked="true">晴川</li>
      <li role="menuitemcheckbox" tabindex="-1" aria-checked="true">静秋</li>
      <li role="menuitemcheckbox" tabindex="-1" aria-checked="false">黄小仙</li>
</ul>4）```


### 1.8.4菜单无法聚焦


【问题描述】<br/>
使用标准键盘操作方式，一个没有聚焦的元素，是不能被操作的。因而，菜单相关元素必须是可以聚焦的，否则用户将无法对他们进行操作。<br/>
【可能原因】<br/>
【修改建议】<br/>
样例1：
将自定义菜单控件的tabindex属性设置为0； <br/>
```<li role="menuitem" tabindex="0" href="...">安全退出</li>```


### 1.8.5键盘焦点无法进入


【问题描述】<br/>
通过键盘操作，一个无法聚焦的元素将无法操作，一个菜单栏内的菜单项无法聚焦，则键盘焦点无法进入这个菜单，用户将不能进行菜单相关的操作。<br/>
【可能原因】<br/>
【修改建议】<br/>
样例1：
给子菜单项添加键盘焦点，如添加tabinedx属性；<br/>
```<li role="menuitem" tabindex="0" href="...">安全退出</li>```


### 1.8.6键盘焦点无法离开


【问题描述】<br/>
此情况较为复杂，可因菜单项具有onfocus="this.blur()"属性设置或使用了js代码限定了焦点的访问范围。<br/>
例：使用了不适当的属性HTML；<br/>
```<li tabindex="0" role="menuitem" onfocus="this.blur()">安全退出</li>```
【可能原因】<br/>
【修改建议】<br/>


### 1.8.7子菜单项无法获得焦点


【问题描述】<br/>
使用键盘操作，一个无法聚焦的元素将无法操作；<br/>
【可能原因】<br/>
【修改建议】<br/>
样例1：
为自定义控件添加role="menuitem"表示菜单项；<br/>
```<li role="menuitem" tabindex="-1" aria-haspopup="false">靓女</li>```
样例2：
为自定义控件添加tabindex属性；<br/>
```<li tabindex="0" aria-haspopup="false">靓女</li>```


### 1.8.8子菜单项无法键盘点击


【问题描述】<br/>
通过键盘操作，应能支持键盘的点击操作。通常是应能支持回车键的操作；<br/>
【可能原因】<br/>
【修改建议】<br/>
样例1：
使用keydown事件使回车键可以展开、折叠菜单；<br/>
样例2：
添加空格点击选中事件；<br/>
```<html>
<head>
<title>test</title>
<script>
function setstate(id){
if(event.keyCode!==32)return false;
var obj=document.getElementById(id);
if(obj.getAttribute("aria-checked")=="false")
obj.setAttribute("aria-checked","true");
else
obj.setAttribute("aria-checked","false");
}
</script>
</head>
<body>
<div>
<ul>
<li tabindex="0" onkeydown="setstate('chk');" role="checkbox" aria-checked="false" id="chk" /><label for="chk">???</label>
<li tabindex="0" onkeydown="setstate('chk2');" role="checkbox" aria-checked="false" id="chk2" /><label for="chk2">????</label>
<li tabindex="0" onkeydown="setstate('chk3');" role="checkbox" aria-checked="false" id="chk3" /><label for="chk3">???</label>
</ul>
</div>
</body>
</html>```


### 1.8.9子菜单项无提示文本


【问题描述】<br/>
菜单项缺少目的描述文本将使使用屏幕阅读器的用户无法得知菜单命令的目的，将使用户操作变得非常困难。<br/>
【可能原因】<br/>
【修改建议】<br/>
样例1：
子菜单项为图片时，添加alt属性给出替代文本；<br/>
```<li ><img src=”1.jpg”  alt=”第一”/></li>```

## 1.9嵌入对象<object>



### 1.9.1对于需要键盘访问的嵌入式对象无法聚焦


【问题描述】 <br/>
对于需要键盘访问的嵌入式对象，如果无法聚焦，使用键盘TAB键将无法访问。<br/>
【可能原因】<br/>
【修改建议】<br/>
样例1：
使用html标准控件；<br/>
样例2：
将自定义控件的tabindex属性设置为0；<br/>
```<object tabindex="0" ...>...</object>```

### 1.9.2焦点无法移出嵌入对象


【问题描述】 <br/>
【可能原因】<br/>
【修改建议】<br/>
样例1：
使用SWFFocus类为flash内容生成临近的可获得焦点的元素，在html tab顺序中。默认的，SWFFocus类将会在嵌入的flash内容的前后生成一个隐藏的链接。这两个链接被作为锚当tab出flash内容的时候将焦点移动到这两个链接。这个方法容易实现，不需要开发者的额外工作。但是隐藏的链接会扰乱html的tab顺序，因此，建议使用下面的方法；<br/>
全部代码：<br/>
```<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" 
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html lang="en"（语言为英文） xml:lang="en" xmlns="http://www.w3.org/1999/xhtml">
  <head>
    <title>键盘陷入修复样例</title>
    <meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
    <script src="swfobject_2_1.js" type="text/javascript"/>
    <script type="text/javascript">
      var flashvars = {};
      var params = {};
      params.scale = "noscale";
      var attributes = {};
      attributes.id = "FlashSample1SWF";
      attributes.name = "FlashSample1SWF";
      swfobject.embedSWF("keyboard_trap_fix_custom_as3.swf", "flashSample1", \ "150", "200", "9.0.0", "expressInstall.swf",flashvars, params, attributes);
</script>
  </head>
  <body>
    <p>下面的这个flash内容自动产生一个可以看到链接在flash内容的前后，允许键盘将焦点移出flash内容。</p>
    <div id="flashSample1">
      <a href="http://www.adobe.com/go/getflashplayer">
        <img alt="获得flash播放器"
src="图片地址http://www.adobe.com/images/shared/download_buttons/get_flash_player.gif"/>
      </a>
    </div>
  </body>
</html>```
样例2：
在html tab顺序中，在flash内容的之前和之后，明确定义可获焦点元素。
使用这个方法，开发者使用ID值来识别html tab顺序中的flash内容前后的元素。这个可通过为flash内容<object>设置特殊的class名字来实现。这个方法很常用，因为这个方法不必引起tab顺序不必要的混乱。但是，这导致开发者更多的工作和无障碍意识。同时，在某些场景中，在flash内容的前后没有可获得焦点的元素。<br/>
全部代码：<br/>
```<a href="http://www.lipsum.com/" id="focus1">test 1</a>
<object class="swfPrev-focus1 swfNext-focus2"
  data="keyboard_trap_fix_as3.swf" tabindex="0"
  type="application/x-shockwave-flash"/>
<a href="http://www.lipsum.com/" id="focus2">test 2</a>```

### 1.9.3嵌入对象不支持键盘操作


【问题描述】 <br/>
【可能原因】<br/>
【修改建议】<br/>
样例1：定义键盘响应事件；<br/>

### 1.9.4嵌入对象无替代文本


【问题描述】 <br/>
【可能原因】<br/>
【修改建议】<br/>
样例1：
嵌入对象包含一个长描述；<br/>
```<object classid="http://www.example.com/analogclock.py">
  <p>这里是一些用来描述对象和操作的文本。Here is some text that describes the object and its operation.</p>
</object>```
样例2：
嵌入对象的无文本内容有替代文本；<br/>
```<object classid="http://www.example.com/animatedlogo.py">
  <img src="staticlogo.gif" alt="公司名称" />
</object> ```
样例3：
图片类嵌入对象提供一个简短的描述来说明图片的目的；<br/>
```<object data="companylogo.gif" type="image/gif">
  <p>公司名称</p>
</object>```
样例4：
使用临近元素来提供替代说明；<br/>
```<object classid="java:Press.class" width="500" height="500">
  <object data="Pressure.mpeg" type="video/mpeg">
    <object data="Pressure.gif" type="image/gif">
      As temperature increases, the molecules in the balloon...
    </object>
  </object>
</object> ```

## 1.10文本域<textarea>



### 1.10.1文本域控件类型提示不正确


【问题描述】<br/>
自定义的输入框，屏幕阅读器无法提示，使用屏幕阅读器用户无法对编辑框做出正确的操作。<br/>
【可能原因】<br/>
  开发者为了界面美观，比较喜欢自己设计一些编辑框，但没考虑到屏幕阅读器用户的操作，对应的无障碍接口没有添加。<br/>
【修改建议】<br/>
样例1：
使用html标准控件；<br/>
```<textarea title="评论内容"></textarea>```
样例2：
当元素的contenteditable属性值为“true时，需要添加title、role、tabindex 属性，为文本域定义角色和添加目的文本，以及焦点可聚焦;<br/>
```<div contenteditable="true" role="textbox" title="评论内容" tabindex="0"></div>```

### 1.10.2文本域聚焦后焦点无法跳出


【问题描述】<br/>
部分情况下，自定义的文本域，焦点无法跳出；<br/>
【可能原因】<br/>
【修改建议】<br/>
使用以下机制可以有效避免该陷阱：<br/>
1.事先定义好内容焦点（通常使用tabindex），当子集或插件导航到最后位置时，跳出子集或插件，事先定义好的焦点可以获得。<br/>
2.定义键盘事件，将焦点移出子集内容。<br/>
3.如果子集使用的技术里面包含回到父级的键盘命令，在用户进入该子集前提示用户该命令。<br/>

### 1.10.3未给文本域添加提示文本


【问题描述】<br/>
缺少描述文本的“文本域”，用户无法获知文本域需要输入哪些信息；<br/>
【可能原因】<br/>
开发者忘记添加提示文本，或者用图片或某个符号代表文本域的提示信息；<br/>
【修改建议】<br/>
样例1：
使用title为文本域添加提示文本；<br/>
```<textarea title="评论内容"></textarea>```
样例2：
使用placeholder为文本域添加提示文本；<br/>
```<textarea placeholder="在此输入评论内容"></textarea>```
样例3：
使用value为文本域添加提示文本；<br/>
```<textarea>在此输入评论内容</textarea>```
样例4：
使用label for为文本域添加提示文本；<br/>
```<label for="comment-content">评论内容:</label>
<textarea id="comment-content"></textarea>```
样例5：
使用aria-label为文本域添加提示文本；<br/>
```<textarea aria-label="你对信息无障碍的理解"></textarea>```
样例6：
使用aria-describedby为文本与提供提示文本；<br/>
```<p><span id="message">请输入您对信息无障碍的理解</span>
<textarea aria-describedby="message"></textarea>
</p>```

### 1.10.4文本框内无法使用方向键逐行逐字浏览


【问题描述】<br/>
【可能原因】<br/>
【修改建议】<br/>
样例1：
使用html标准控件；<br/>
```<label for="message">您对视障工程师的理解:</label><textarea id="message"></textarea>```
样例2：<br/>
```<div contenteditable="true" role="textbox" title="评论内容" tabindex="0"></div>```


## 1.11Frame



### 1.11.1键盘焦点无法跳出


【问题描述】<br/>
键盘焦点无法跳出框架，即在一个框架内连续按tab键，焦点总是无法离开这个frame；<br/>
【可能原因】<br/>
未给离开frame的元素设置合理的tabindex，导致焦点无法离开。<br/>
【修改建议】<br/>

### 1.11.2框架无名称


【问题描述】<br/>
当用户按tab键进入该框架时，屏幕阅读器未朗读出框架的名称；<br/>
【可能原因】<br/>
1、未给对应框架加入合适的name属性；<br/>
2、框架的title属性赋值不当；<br/>
【修改建议】
样例1：<br/>
使用title属性来描述带有导航条和文件的框架；<br/>
```<html xmlns="http://www.w3.org/1999/xhtml">
  <head>
    <title>一个简单的框架文件</title>
  </head>
  <frameset cols="10%, 90%">
    <frame src="nav.html" title="主菜单" />
    <frame src="doc.html" title="文件" />
    <noframes>
      <body>
        <a href="lib.html" title="图书馆链接">选择去图书馆</a>
      </body>
    </noframes>
  </frameset>
</html>``` 

### 1.11.3焦点无法聚焦到框架内的链接


【问题描述】
按tab键无法到达某个框架内的链接；
【可能原因】
在进入框架前的一个链接设置了焦点模糊，导致该链接被聚焦后焦点会被重置；
【修改建议】
样例1：
强制去除框架前焦点的聚焦会导致该问题的出现：
<a href="#" onfocus="this.blur()">TAB焦点切不到我</a>
<iframe src="example.html" title="IFrame框架" />

## 1.12Iframe



### 1.12.1键盘焦点无法进入


【问题描述】<br/>
按tab键无法到达某个框架内的元素；<br/>
【可能原因】<br/>
1、在进入框架前的一个控件元素设置了强制去除焦点，导致无法越过该焦点进入iframe框架内；<br/>
2、框架内的元素未设置适当的tabindex；<br/>
【修改建议】<br/>
样例1：
强制去除框架前焦点的聚焦会导致该问题的出现：<br/>
```<a href="#" onfocus="this.blur()">TAB焦点切不到我</a>```
样例2：
为内联框架的子集添加焦点；<br/>
```example2.html:
<iframe src="child.html" title="IFrame框架" />
child.html:
<ul>
<li tabindex="0">子元素1</li>
<li tabindex="0">子元素2</li>
</ul>```

### 1.12.2键盘焦点无法移出


【问题描述】<br/>
键盘焦点无法跳出框架，即在一个框架内连续按tab键，焦点总是无法离开这个iframe；<br/>
【可能原因】<br/>
未给离开iframe的元素设置合理的tabindex，导致焦点无法离开。<br/>
【修改建议】<br/>

## 1.13密码控件



### 1.13.1密码控件无法获得键盘焦点


【问题描述】<br/>
tab无法找到密码框；<br/>
【可能原因】<br/>
【修改建议】<br/>
样例1：<br/>
```<input type="password" />
定义密码字段。密码字段中的字符会被掩码（显示为星号或原点）。
<input type="password" name="pwd" />```

### 1.13.2读屏打开状态下无法输入


【问题描述】<br/>
在读屏开启的状态下，密码框不可输入；<br/>
【可能原因】<br/>
【修改建议】<br/>

### 1.13.3密码控件无名称


【问题描述】<br/>
tab找到密码控件后，不会朗读这是什么密码框；<br/>
【可能原因】<br/>
【修改建议】<br/>
样例1：
使用label提示用户<br/>
```<label for="user-pwd">密码</label><input type="password" id="user-pwd" />```
样例2：
```使用title提示用户<br/>
<input type="password" title="密码" />```
样例3：
使用placeholder提示用户<br/>
```<input type="password" placeholder="请在此输入密码" />```
样例4：
使用aria-label提示用户<br/>
```<input type="password" aria-label="密码" />```

### 1.13.4密码控件键盘焦点无法移出


【问题描述】<br/>
使用屏幕阅读器浏览网页，tab到达密码框后，无法用tab跳出密码框；<br/>
【可能原因】<br/>
【修改建议】<br/>
使用以下机制可以有效避免该陷阱：<br/>
1.事先定义好内容焦点（通常使用tabindex），当子集或插件导航到最后位置时，跳出子集或插件，事先定义好的焦点可以获得。<br/>
2.定义键盘事件，将焦点移出子集内容。<br/>
3.如果子集使用的技术里面包含回到父级的键盘命令，在用户进入该子集前提示用户该命令。<br/>

### 1.13.5密码控件光标无法移动，或能移动不会读出字符


【问题描述】<br/>
tab键到达密码控件，用左右方向键不能移动光标，或能移动，读屏没声音<br/>。
【可能原因】<br/>
【修改建议】 <br/>