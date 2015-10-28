### 1.3浮层
背景描述：<br/>
　　*浮层通常是通过frame、div等实现提供提示、通告等功能的弹出的可移动的独立窗口。网站多使用浮窗来实现登陆、警告等功能。但是，用户多是只能通过视觉来感知弹层的存在，对视觉受限的屏幕阅读器用户来说，没有其他感知的提示有浮窗的存在。这些用户在点击按钮或链接以后，键盘焦点仍停留在原来的焦点位置，不会自己聚焦到浮窗上，只有使用tab键便利在网页最后，才会进入浮窗，这给屏幕阅读器用户带来很大的不便。小朱同学要使用某宝付款，上某度下载东西的时候就遇上了类似的问题。*<br/>
#### 1.3.1不知道有浮层弹出
![](/9.png)<br/>
图9 　不知道有浮层弹出【示例】<br/>
【问题描述】<br/>
由于网页浮层弹出时，焦点没有及时聚焦到浮层元素内，键盘使用者无法获知有浮层的存在；<br/>
【可能原因】<br/>
1、弹出的浮层没有table index属性，焦点无法跟在触发控件后面；<br/>
2、浮层内容缺少文本描述，例如登录对话框，建议添加title属性来描述。<br/>
【修改建议】<br/>
#### 1.3.2焦点不在触发控件之后
![](/10.png)<br/>
图10　 焦点不在触发空间之后【示例】<br/>
【问题描述】<br/>
按tab移动网页焦点到触发浮层控件，激活后，焦点没有及时进入浮层内容，下一个焦点不在浮层内；<br/>
【可能原因】<br/>
可能是弹出的浮层子元素没有添加tabindex，或是javascript直接追加元素非紧跟当前焦点插入元素。<br/>
【修改建议】<br/>
样例1：<br/>
给浮层内的子元素增加tabindex属性。<br/>
样例2：<br/>
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
<input name="but1" id="but1" type="button" 
onclick="createInput('divid');" value="新增输入框1" /><br />
<input name="but2" id="but2" type="button" 
onclick="createInput('divid');" value="新增输入框2" /><br />
<input name="but3" id="but3" type="button" 
onclick="createInput('divid');" value="新增输入框3" /><br />
</div>```
#### 1.3.3不能使用键盘关闭浮层
![](/11.png)<br/>
图11 　不能使用键盘关闭浮窗【示例】<br/>
【问题描述】<br/>
浮层中的关闭按钮为图片，或自定义控件，导致焦点无法聚焦到关闭控件。<br/>
【可能原因】<br/>
自定义控件为图片链接，没有给图片链接添加alt或title属性，或自定义控件导致的没有焦点。<br/>
【修改建议】<br/>
样例1：
```<img src="img0.jpg" alt="关闭" tabindex="0" role="button" />```
#### 1.3.4用键盘操作，焦点无法进入浮层
![](/12.png)<br/>
图12　 用键盘操作，焦点无法进入浮层【示例】<br/>
【问题描述】<br/>
使用键盘，无法遍历到浮层内元素；<br/>
【可能原因】<br/>
可能浮层内有阻止焦点进入的代码，或者自定义控件没考虑键盘操作；<br/>
【修改建议】<br/>















