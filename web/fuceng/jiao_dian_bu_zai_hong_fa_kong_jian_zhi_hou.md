#### 焦点不在触发控件之后
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

