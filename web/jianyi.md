
# （三）Web端无障碍建议
    该部分内容参考自Web Content Accessibility Guidelines (WCAG)
2.0（http://www.w3.org/Translations/WCAG20-zh/）、How to Meet WCAG 2.0（http://www.w3.org/WAI/WCAG20/quickref/#qr-text-equiv-all）。在进行web内容开发时，可参考以下建议。

## 3.1焦点可见：键盘用户操作时焦点可见



### 3.1.1当界面元素获得焦点时突出显示


    样例1：
    当html文本输入区域接收到焦点时，浏览器在文本输入区域显示闪烁的竖线；
    样例2：
    当html链接接收到焦点时，它们被聚焦亮点矩形包围；

### 3.1.2使用CSS改变控件获得焦点时的显示


    样例1：链接元素
```
html内容：
<ul id="mainnav">
  <li class="page_item">Home</li>
  <li class="page_item"><a href="/services">Services</a></li>
  <li class="page_item"><a href="/projects">Projects</a></li>
  <li class="page_item"><a href="/demos">Demos</a></li>
  <li class="page_item"><a href="/about-us">About us</a></li>
  <li class="page_item"><a href="/contact-us">Contact us</a></li>
  <li class="page_item"><a href="/links">Links</a></li>
</ul>
CSS代码:
#mainnav a:hover, #mainnav a:active, #mainnav a:focus {
  background-color: #DCFFFF;
  color:#000066;
}```
    样例2：焦点元素高亮显示
```
<html>
  <head>
    <style type="text/css">
      input.text:focus {
        background-color: #7FFF00; 
        color: #000;
      }
      input[type=checkbox]:focus + label, input[type=radio]:focus + label {
        background-color: #FF6; 
        color: #000; 
      }
    </style>
  </head>
  <body>
    <form method="post" action="form.php">
      <p><label for="fname">Name: </label>
        <input class="text" type="text" name="fname" id="fname" />
      </p>
      <p>
        <input type="radio" name="sex" value="male" id="sm" /> <label for="sm">Male</label><br />
        <input type="radio" name="sex" value="female" id="sf" /> <label for="sf">Female</label>
      <p>
    </form>
  </body>
</html>```

### 3.1.3使用默认的焦点提示


    样例1：
    Microsoft Windows默认的焦点显示是个1px的黑色虚线，在焦点元素的周围。一个黑色背景的网页，默认显示很难看到。网页的生成器使用默认的显示，用户可以自定义改变；
    样例2：
    在html中，表单元素和链接可以默认聚焦。此外，任何具有tabindex且tabindex大于等于0的元素都可以获得焦点。两种焦点元素都可以使用系统焦点显示，会识别焦点显示样式的平台改变。

### 3.1.4开发者提供一种高度可见的焦点提示


    在该技巧中，可以使用鼠标、tab键、箭头键、快捷键、或其他的方法让用户将焦点放置在一个元素上，使用高对比度的颜色、粗线、或者其他的视觉提示，比如闪烁；
    样例1：链接
    网页有深背景颜色和比较亮的文本和链接。当焦点在链接上时，链接外有一个亮的黄色的线。
    样例2:表单元素
    网页里包含表格内的表单。表格和表单的边框都很细、黑色的线。当焦点位置表单元素时，元素外有半透明的红色线；
    样例3：菜单
    网页中的交互菜单包含子菜单。用户可以使用上下光标来移动焦点。因为焦点移动，当前焦点菜单条目改变背景颜色，与周围条目有一个3:1的对比度，与文字的对比度为4.5:1。

### 3.1.5使用脚本来改变焦点元素的背景颜色或者边框


    样例1：
    本例中，当链接接收到焦点时，其背景变为黄色；inherit是继承父类的属性，一般用于字体、颜色、背景等；
    此处有省略...
```
<script>
 function toggleFocus(el)
 {
  el.style.backgroundColor =  el.style.backgroundColor=="yellow" ? "inherit" : "yellow";
 }
</script>
此处有省略...
<a href="example.html" onfocus="toggleFocus(this)" onblur="toggleFocus(this)">焦点</a>
此处有省略...```
    3.2用户在浏览一系列网页时，当前网页的位置信息应该可以获得
    面包屑（breadcrumb trail ）：
    使用">", "|", "/", "::"在面包屑中分开条目：
    样例1：
    主页::信息无障碍测试::怎样加入，当前页面“怎样创建超链接”是不在面包屑中的；
    样例2：
    主页/画廊/南极洲/企鹅/巴布亚企鹅:除了最后一个巴布亚企鹅，其他都是个链接，巴布亚企鹅包含在面包屑中，却不是个链接；
    
    网站地图（map site）:
    可以提供整个网站的总览，帮助用户了解网站包含的内容和内容是怎样组织的；提供了一个不同于复杂导航条的导航方式。网站地图应该做到提供所有网站所有部分的链接，地图呈现出来的组织方式应该和网站的组织方式相同，不包含无效链接；
    样例1：
    WAI的网站提供一个WAI的网站地图，列出了网站的不同部分，展示了网站的不同部分及其内部结构；
    样例2：
    在线杂志会列出杂志的所有章节和其下所有子章节。包含帮助、联系我们、版权政策、雇佣机会、投稿、主页等等链接。
    
    使用导航条来指明当前位置：
    可以使用添加个图标或者文本，或者改变条目的状态。
    样例1：
    导航栏的当前页面栏目，颜色发生改变；
    样例2：
    在一个网页中设计两个框架（frame），一个用来装目录，一个用来装内容；
    样例3：
    焦点或鼠标划过的时候，有背景颜色的改变。

## 3.3创建一种机制跳过一堆界面相同的部分，直接到达主内容



### 3.3.1在网页第一交互条目就是添加一个链接到主内容的开始


    样例1：
    在线报纸网页，第一个tab就是跳到主要故事；
    样例2：
    第一个链接为跳到主要内容；

### 3.3.2提供一种机制从网页模块开头跳转到模块尾部


    当有许多模块需要跳转的时候，用户使用这种机制跳转；
    样例1：
    跳过导航链接，网页第一个链接的title为（跳过导航区域）；
    样例2：
    书目导航，在目录前边有术语解释或者其他内容，这个区域的第一个链接应该是：跳过给区域到目录；
    样例3：
    一个网站的所有网页包含网站地图的链接、杂志信息、怎样联系机构。所有的链接都包含子链接，第一个模块的第一个链接的title应为跳过导航链接，第二个模块的title应为跳过章节链接，跳过所有子链接。

### 3.3.3在网页顶端添加网页各内容的链接


    样例1：
    在所有网页开始都有三个链接：跳转到主页、搜索区域、导航条。
    
### 3.3.4使用ARIA路标（landmark）来区分网页中的区域


    网页内的某一区域作为导航路标。辅助技术应该允许用户快速导航到该区域，主流的用户代理允许用户快速的导航到路标区域。注：路标是网页集的规则简介。开发者不建议在内容中使用该角色。
    landmark是网页上用户想快速浏览的某一区域，这个区域的内容与其他区域的用户目的不同，比如导航、搜索、查看详细内容做作用。
    路标通过添加role属性来标记区域。role属性的值就是路标的名字，值有：banner（旗帜）、complemenary（附加）、contentinfo（引用）、form（表单）、navigation（导航）、search（搜索）、application（应用）。最好landmark中包含网页中的所有内容，读屏使用者不会丢失内容。
    landmark上一级role是region（区域），下一级role有application（应用）、banner（旗帜）、complementary（补充）、contentinfo、form（表单）、main（主题）、navigation（导航）、search（搜索）；
    样例1：简单路标
```
<div id="header" role="banner">旗帜图片和介绍性标题</div>
<div id="sitelookup" role="search">搜索区域</div>
<div id="nav" role="navigation">这有一群链接  </div>
<div id="content" role="main">渥太华是加拿大的首都</div>
<div id="rightsideadvert" role="complementary">.这有一个广告</div>
<div id="footer" role="contentinfo">(c)自由公司、123自由路、美国T</div>```
    样例2：
    如果使用多次同一role值的路标，应该依靠aria-labelledby属性来区分，aria-labelledby属性值是子元素的id值；
```
<div id="leftnav" role="navigaton" aria-labelledby="leftnavheading">
<h2 id="leftnavheading">系统链接</h2>
<ul><li>一堆链接这里有</li> </ul></div>
<div id="rightnav" role="navigation" aria-labelledby="rightnavheading">
<h2 id="rightnavheading">有关的题目</h2>
<ul><li>这里有一堆信息无障碍相关链接</li></ul></div>```
    样例3：
    同一role值的路标，没有可以区分的文本，使用aria-label来区分；
```
<div id="leftnav" role="navigaton" aria-label="Primary">
<ul><li>这里有一堆信息无障碍相关链接 </li></ul> </div>
<div id="rightnav" role="navigation" aria-label="Secondary">
<ul><li>这里有一堆信息无障碍相关链接 </li> </ul></div>```
    样例4：
    搜索表单；
```
<form role="search">
<label for="s6">搜索</label><input id="s6" type="text" size="20">
</form> ```
  
###   3.3.5在每一个章节内容前提供标题元素：要求上下级标题有继承和逻辑关系


    样例1：
    通过使用h2标签组织章节；
```
<h1>搜索信息无障碍技术周刊</h1>
 <h2>搜索</h2>
 <form action="search.php">
  <p><label for="searchInput">输入搜索主题：</label>
  <input type="text" size="30" id="searchInput">
  <input type="submit" value="Go"></p>
 </form>
 <h2>可获得的周刊</h2>
 <div class="jlinks">
  <a href="pcoder.com">视障工程师</a> |
  <a href="algo.com">无障碍方法</a> |
  <a href="jse.com">信息无障碍期刊</a>
 </div>
 <h2>搜索期刊</h2>
  搜索到的期刊   ``` 
    样例2：使用标题展示网页内容的组织；
```
<!-- Logo, 旗帜广告, 搜索表单, 等等.  -->
  <h2>导航</h2>
    <ul>
      <li><a href="about.htm">关于我们</a></li>
      <li><a href="contact.htm">联系我们</a></li>
       
    </ul>
  <h2>所有的标题</h2>```
   <!-- 文字, 图片,网页中的其他内容 --> 
    样例3：标题可以展示出主要内容材料的组织方式
```
<html xmlns="http://www.w3.org/1999/xhtml">
  <head>
    <title>信息无障碍</title>  
  </head>   
  <body>     
    <h1>可访问性</h1>     
    <p>       
       这里有些文本      
    </p>           
    <h2>可操作性</h2> 
    <p> 
         这里有些文本      
    </p>           
    <h2>可理解性</h2>       
    <p>
         这里有些文本      
    </p>   
  </body> 
</html>```
    注：H标签的优化用法
    1）如果在一个页面中定义很多H1标签，搞得用户和搜索引擎不知道你这个页面到底要说明什么内容，是会被搜索引擎惩罚的。所以应用H1要谨慎，要从服务用户的角度去出发，真正的在页面中合理使用H1标签。
    2）在主页，<H1/>标签当仁不让的用来定义“站点名称”。<H2/>标签用来定义“站点副标题”。如果没有副标题，<H2/>标签最好也空着，以备不时之需。<H3/>标签用来定义栏目名称，<H4/>标签用来定义文章标题，但大多数内容系统，文章列表输出用<UL/>标签，所以<H4/>可能就派不上用场，这里只是以此类推。
    3）目录页(栏目页)和主页类似，<H/>系列标签同主页定义。
    4）文章内容页，<H1/>标签给文章的主标题；以利于提高文章在搜索引擎中的权重。
    5）整个网站(一般指首页如何对H标签定义)关键词设置时本着，重点中的重点用h1标签(网站的核心关键词)，相对重点用h2标签(网站的各个频道级重要的长尾关键词)，再往下用h3标签(一般指类表页或者最终页的标题)…….依次类推，不过一般网页不会超过h3标签的定义!

### 3.3.6使用框架元素来代替网页中的重复部分


```
<frameset cols="20%, *">
  <frame src="navigation.html" name="navbar" title="导航栏" />
  <frame src="main.html" name="maincontent" title="主要新闻内容" />
  <noframes>
    <p><a href="noframe.html">无框架部分</a>.</p>
  </noframes>
</frameset> ```    
    横向框架是： <frameset cols=#>
    比如说有两列，左边一个，右边一个。
    纵向框架是： <frameset rows=#>
    比如说有两行，上边一个，下边一个。
    cols是说有几列，rows是说有几行  
    样例1：
    使用title属性来描述带有导航条和文件的框架；
```
<html xmlns="http://www.w3.org/1999/xhtml">
  <head>
    <title>一个简单的框架文件</title>
  </head>
  <frameset cols="10%, 90%">
    <frame src="nav.html" title="主菜单" />
    <frame src="doc.html" title="文件" />
    <noframes>
      <body>
        <a href="lib.html" title="图书馆链接">选择去盲文图书馆</a>
      </body>
    </noframes>
  </frameset>
</html> ```
    样例2：
    使用iframe的title属性来描述框架的内容；
```
<html xmlns="http://www.w3.org/1999/xhtml">
  <head>
    <title>使用iframe的文件</title>
  </head>
<iframe src="banner-ad.html" id="testiframe" 
  name="testiframe" title="广告">
    <a href="banner-ad.html">广告</a>
</iframe>
</html>  ```
    
### 3.3.7使用展开和折叠菜单绕过内容块：使用可展开折叠菜单来跳过重复的内容


    样例1：
    使用html、css、JS脚本在网页顶部添加一个折叠菜单：
  ```
  <script type="text/javascript">
  function toggle(id){
    var n = document.getElementById(id);//获得固定id值的元素，赋给n；
    n.style.display =  (n.style.display != 'none' ? 'none' : '' );
  }//将控件n的display属性设置为none，不可用；
  </script>
  <a href="#" onclick="toggle('navbar')">切换导航栏</a>
  <ul id="navbar">
  <li><a href="http://target1.html">链接 1</a></li>
  <li><a href="http://target2.html">链接 2</a></li>
  <li><a href="http://target3.html">链接 3</a></li>
  <li><a href="http://target4.html">链接 4</a></li>
  </ul>```
    样例2：
    内容列表在每个网页都有出现，在列表前加一个按钮来移除和添加按钮；
       ```
       <script type="text/javascript">
  function toggle(id){
    var n = document.getElementById(id);
    n.style.display =  (n.style.display != 'none' ? 'none' : '' );
  }
  </script>
  <button onclick="return toggle('toc');">无障碍内容切换表</button>
  <div id="toc">
  </div>```
   
##  3.4焦点：当任何用户界面组件接收焦点时，不会引起上下文变化


    
### 3.4.1使用activate作为上下文改变的触发器而不是focus（焦点）


    样例1：
    一个页面打开，只有当用户点击按钮，而不是使用onfocus事件来触发；
    样例2：
    提交按钮是用来移动到其他数据页的，而不是当提交按钮获得焦点时就自动跳转；
   
###  3.4.2必须时才可以通过链接打开一个新窗口


    限制链接和按钮的使用。当链接的新窗口打开时，需要提醒用户；
    样例1:在线表单
    在线表单为每一个表单区域提供上下文蜜柑帮助信息，在不同的页面。上下文敏感链接帮助打开新的窗口来阻止已输入数据的丢失；
    样例2：
    安全网站的一个网页包含一个外部链接，是在当前安全机制以外，链接应该在新窗口打开，不要破坏原来的安全机制；
    样例3：
    数据采集器：当需要打开新窗口采集数据时，要保证原来输入的数据不会丢失；

### 3.4.3打开新窗口时提供给用户提示信息


    样例1：
    在控件内包含提示文本；
    <a href="knitting.html" target="_blank">点击（打开一个新窗口）</a>
    样例2：
    使用CSS样式提供提示，打开一个新窗口；


<html>
<head>
<title>Pop-Up Warning</title>
<style type="text/css">
body {
margin-left:2em;
margin-right:2em;
}
:focus { outline: 0; }
a.info {
position:relative;
z-index:24;
background-color:#ccc;
color:#000;
text-decoration:none
}
a.info:hover, a.info:focus, a.info:active {
z-index:25;
background-color:#ff0
}
a.info span {
position: absolute;
left: -9000px;
width: 0;
overflow: hidden;
}
a.info:hover span, a.info:focus span, a.info:active span {
display:block;
position:absolute;
top:1em; left:1em; width:12em;
border:1px solid #0cf;
background-color:#cff;
color:#000;
text-align: center
}
div.example {
margin-left: 5em;
}
</style>
</head>
<body>
<h1>跳转警告</h1>
<p> 这是一个警告 <a class="info"
href="http://www.siaa.org.cn/" target="_blank">
<strong>外部链接</strong><span>打开一个新窗口</span></a>
</p>
</body>
</html>
3.5输入：改变任何用户界面组件的设置不会自动导致上下文的变化，除非在使用组件之前用户被告知了此行为会导致变化
3.5.1提供一个提交按钮来确认上下文的改变
样例1：提交按钮用在每一个引起上下文变化的表单中；
3.5.2提供一个submit按钮
提交按钮产生一个http请求，适合用来作为引起上下文改变的控件；
样例1：submit基本样例
<form action="http://www.example.com/cgi/subscribe/" method="post">
<br /> 
<p>请输入你的邮件</p>
<br /> 
<label for="address">输入邮件地址</label>
<input type="text" id="address" name="address" /> 
<input type="submit" value="Subscribe" /><br /> 
</form>       
样例2：服务器端脚本
<form action="http://www.example.com/cgi/redirect/" method="get"><br/> 
<p>网页导航</p><br /> 
    <select name="dest"><br /> 
      <option value="/index.html">主页</option/><br /> 
      <option value="/blog/index.html">我的微博--信息无障碍</option/><br /> 
      <option value="/tutorials/index.html">路径</option/><br /> 
      <option value="/search.html">搜索</option/><br /> 
    </select><br /> 
<input type="submit" value="转向网页" /><br /> 
</form>
3.5.3使用具有选择元素的按钮来实现某个活动
当用户满意自己当前的选择时，提供一个按钮来保存当前的选择，这对键盘使用者来说特别重要；
样例1：
日期选择器：网页允许用户选择年月，显示该年月的日历。当用户设置好年月，可以通过点击显示按钮来显示日历。这就依靠客户端的脚本来实现。
<label for="month">月:</label>
<select name="month" id="month">
<option value="1">1月</option>
<option value="2"> 2月</option>
  
<option value="12">3月</option>
</select> 
<label for="year">年:</label>
<input type="text" name="year" id="year">
<input type="button" value="显示" onclick = "">
样例2：
<form action="http://somesite.com/action" method="post">
  <label for="action">选择:</label>
  <select name="action" id="action">
    <option value="help">帮助</option>
    <option value="reset">重置</option>
    <option value="submit">提交</option>
  </select> 
  <button type="submit" name="submit" value="submit">执行 </button>
</form>  
3.5.4在表单的改变引起上下文的改变时，需要在提交前告知用户将要发生的改变
样例1：
在页面顶部有一系列单选按钮，包括德国、法国和西班牙，在选择按钮时，将给出提示文本，网页的语言将会发生变化；
样例2：
含有50个问题的在线问卷调查，每次只显示一个页面。在调查开始前应该告知用户选择选项后将会跳到下一个题目。
3.5.5使用onchange事件来选择元素，不引起上下文的变化
样例1：
这个例子包含两个选择元素。当第一个元素被选择时，第二个元素的会发生改变；
关键代码：<select id="continent" onchange="countryChange(this);">//当选择发生改变时，国家列表也发生改变；
全部代码：
<?xml version="1.0" encoding="UTF-8"?> 
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" 
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"> 
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en"> 
  <head> 
    <meta http-equiv="content-type" content="text/xhtml; charset=utf-8" /> 
    <title>动态选择</title> 
<script type="text/javascript">
 //<![CDATA[ 
 // 可能国家的数组，顺序与在国家列表出现的相同；
 var countryLists = new Array(4) 
 countryLists["空"] = ["选择一个国家"]; 
 countryLists["北美"] = ["加拿大", "美国", "墨西哥"]; 
 countryLists["南美"] = ["巴西", "墨西哥", "奇了", "厄瓜多尔"]; 
 countryLists["亚洲"] = ["俄国", "中国", "日本"]; 
 countryLists["欧洲"]= ["英国", "法国", "西班牙", "德国"]; 
 /* CountryChange()被选择元素的onchange事件调用
 * param selectObj 被onchange事件激活的选择事件；
 */ 
 function countryChange(selectObj) { // 获得选择项的索引
 var idx = selectObj.selectedIndex; // 获得选择项的值 
 var which = selectObj.options[idx].value; // 使用选择项的值重置国家列表
 cList = countryLists[which]; // 通过已知的id获得国家选择元素
 var cSelect = document.getElementById("country"); 
//将国家选择的当前列表移除
 var len=cSelect.options.length; 
 while (cSelect.options.length > 0) { 
 cSelect.remove(0); 
 } 
 var newOption; 
 // 创建新的选项
 for (var i=0; i<cList.length; i++) { 
 newOption = document.createElement("option"); 
 newOption.value = cList[i];  // 假设选项字符串和值是相同的 
 newOption.text=cList[i]; 
 //添加新的选项
 try { 
 cSelect.add(newOption);  // dom浏览器失效，但是IE需要
	；} 
 catch (e) { 
 cSelect.appendChild(newOption); } } } 
//]]>
</script>
</head>
<body>
  <noscript>此网页需要JavaScript可用并启用正常</noscript>
  <h1>动态选择状态</h1>
  <label for="continent">选择洲</label>
  <select id="continent" onchange="countryChange(this);">
    <option value="empty">选择一个洲</option>
    <option value="North America">北美</option>
    <option value="South America">南美</option>
    <option value="Asia">亚洲</option>
    <option value="Europe">欧洲</option>
  </select>
  <br/>
  <label for="country">选择一个国家</label>
  <select id="country">
    <option value="0">选择一个国家</option>
  </select>
</body>
</html>
3.6一致性导航
在多个页面出现的导航机制要以相同的逻辑顺序出现，除非用户被告知变化；
样例1：
一个网站在网页的顶部有logo，有标题，有搜索表单还有一个导航条，他们出现在网页的相关顺序都是一样的。一个网页的搜索框不见了，其他内容的顺序不会改变；
样例2：
一个网站有一个左侧导航按钮，这个导航按钮有网站主要部分的链接。当用户使用链接去到网站其他部分的时候，其他主要内容的链接的顺序在下个网页是一样的。有时候链接会被删除和添加，但是其他链接总是保持在同样的顺序。例如，一个公司网站，卖产品和提供训练，当用户从商品转移到训练时，个人商品就会被懂导航列表移除，培训的链接会被添加；
3.7一致性识别
网页集里有相同功能的元素要被一致性识别；使用标签、名字和替代文本的一致性为相同功能内容提供一致性；
样例1：
一个网页在顶部有一个标签为搜索的表单区域。网页底部也有一个相同功能的表单区域，也要被标签为搜索；
样例2：
一个问题标记的图片用来提醒用户去到提供额外信息的网页。问题标记的每次出现都有相同的替代文本“更多信息”；
样例3：
一个网站联系我们网页的链接有一个链接文本“联系”。在网页的底部也有一个链接去到联系我们网页，它的链接文本也是“联系”；
3.8请求变更
上下文的改变应该发生在用户请求，或者可以将这种改变关闭的情况下；

3.8.1提供一种机制来变更网页的刷新而不是自动刷新
手动进行网页刷新，而不是自动刷新，自动刷新会给屏幕阅读器带来困扰，因为屏幕阅读器不知道发生了什么，虚拟光标不会停留在当前位置会移动到页面顶部；
样例1：
提供一个按钮来自动刷新网页：
<a href="news.jsp">刷新网页</a>
样例2：
email的网页界面，开发者可以提供一个按钮或者链接来查看新进来的邮件，而不是自动刷新；
3.8.2使用元刷新创建一个即时的客户端重定向
在html和xhtml中可以使用http-equiv属性值为“Refresh（刷新）”、“content”（内容）属性设置为“0”的元元素，还有url属性。
<html xmlns="http://www.w3.org/1999/xhtml">    
  <head>      
    <title>信息无障碍研究会</title>      
    <meta http-equiv="refresh" content="0; URL='http://www.siaa.org.cn/'" />    
  </head>    
  <body> 
    <p>此网页被转移到<a href='http://www.siaa.org.cn/'" >
   信息无障碍研究会</a>.</p> 
  </body>  
</html>  
3.8.3在服务器端设置自动重定向而不是在客户端
使用html元素重定向的时候，会有几秒钟的挺短，这使得该网页不能被一些用户获得，尤其是一些读屏用户。服务器端的技术提供方法来重定向而不会困扰用户。服务器端脚本和配置文件可以引起服务器发送合适的http响应，当浏览器接收到这个响应，地址栏的变化和浏览器发出新的URL的请求。
3.8.4使用target属性去打开一个窗口当用户请求的时候，并在链接文本里告知用户
样例1：<a href="help.html" target="_blank">帮助 (在新窗口中打开)</a>
3.9内容的可理解性
3.9.1添加一个文本摘要，可以被低文化水平的人理解
1)点出内容中最最重要的思想和信息；
2)包含一个多个段落，使用更多短句和更多相同的词汇来表达相同的思想和信息；
3)评价摘要的可读性；
4)编辑摘要，拆分成短句；
5)重复34步。
3.9.2提供视觉例子，图片，样本来帮助解释思想、事件、或过程
图表和图形帮助用户理解复杂的数据。
图，流程图，视频和动画帮助用户理解过程。
概念图等图形组织者帮助用户了解如何想法是相互关联的。
照片，图纸，和视频可以帮助用户理解自然或历史事件或物体。
样例1：公司的年度报告，使用图表；
样例2：科技文档中的截屏；
样例3：复杂自然事件的举例；
3.9.3为文本提供语音版本
3.9.4使文本更易阅读
1)每个段落一个主题；
2)使用最简单的句子结构，主谓宾；
3)使用句子的长度不超过中等教育的典型接收长度，英文25个词；
4)把长句子切分为2个短句子；
5)使用包含不多于2个连词的句子；
6)表明短语、句子、段落、和段落之间的逻辑关系；
7)避免使用专业术语、俚语等术语，或者其他对大多数人意义不明的词汇；
8)用较短的，更一般的术语替换长或不熟悉的单词；
9)在不改变句子意思的前提下，去掉多余的；
10)使用单名词或者短多词短语；
11)使用项目符号或编号里诶啊哦而不是段落包含一连串的单词或短语用逗号隔开；
12)明确文档中的代词指引；
13)多使用主动语态，容易理解；
14)使用名词和标签一致。
3.9.5为内容中的信息、思想、过程等添加手语版本
3.9.6若单词或短语被特定或有限制的方式使用，包括成语和术语，则提供一个确定这些单词或短语的具体定义
1）为不常见的词或有特定语言环境的词提供定义；（方言、俚语、专业术语、外语中不熟悉的词汇、业内术语）
2）链接到页内定义区：
<p>这是文本<a href="#definition">这是专业名词</a></p>
<h3>脚注：（在脚注里给出定义）</h3>
<dl>
<dt id="definition" name="definition">信息无障碍专业名词</dt>
<dd>这是专业名词的解释</dd>
</dl>
3）使用定义列表，使用dl、dt、dd来保证词汇与定义之间的关系，列表在使用字母排序的时候最容易使用。定义列表一般使用在词汇表。
样例：航海术语定义列表：
<dl title="无障碍术语">
  <dt>Knot</dt>
  <dd>
    <p> <em>信息无障碍</em>是指任何人（无论是健全人还是残疾人，无论是年轻人还是老年人）在任何情况下都能平等的、方便地、无障碍地获取信息、利用信息。</p>
  </dd>
  <dt>可访问性</dt>
  <dd>
    <p><em>可访问性</em>  为所有非文本内容提供替代文本，使之可以转化为用户需要的其他形式（例如大字版本、盲文、语音、符号语言、简化语言）；</p>
  </dd>
  <dt>可操作性</dt>
  <dd>
    <p><em>可操作性</em>所有功能均可通过键盘操作；</p>
  </dd>
</dl>       
4）当词汇和定义列表不在一个网页重视，使用link来链接定义列表，link的rel值为glossary，href为定义页面的地址。
样例：<link rel="glossary" href="http://www.w3c.org/TR/WCAG20/#glossary">
5）使用行内定义：在上下文中给出词汇的定义；
6）使用dfn元素来明确词汇的定义实例。这个只是将词汇括起来而已，并不是定义，是在词汇定义的位置使用。
<p> Web内容辅助功能准则要求非文本内容必须有替代文本。 <dfn>非文本内容</dfn>是内容，是不是可以以编程方式确定或顺序字符，其中序列状态并没有表达的东西在人类语言;这包括ASCII艺术（这是字符），表情符号，（这是字符替代），和代表文字图像。</p>
7）提供一个词汇表：位于页面地步，用来定义
8）提供一个功能可以在线搜索词典；
3.9.7提供一个机制用于确定缩写词的扩展形式或含义
1）为缩写提供扩展和解释；
2）缩写第一次使用时在之前或之后提供扩展形式；
联合国高级人权专员（unHCR）成立于1950年，以提供保护和援助难民。
该WAI（无障碍网页倡议）演示了W3C的承诺可访问性。
3）链接到定义；
4）使用abbr元素来定义缩写；
样例1：使用abbr来扩展缩写；
<p>5<abbr title="无障碍信息bug">bug<abbr></p>
<p>欢迎 <abbr title="Shenzhen information accessibility association">SIAA</abbr>!</p>   
样例2：使用abbr来扩展；
<p>深圳市信息无障碍研究会<abbr title="和其他">et al.</abbr> <abbr title="versus（与）">v.</abbr>纽约时间<abbr title="and others（和其他）">et al.</abbr> 是中国信息无障碍联盟的重要成员</p> 
样例3：使用abbr来扩展缩写；
<p> <abbr title="accessibility technology">AT</abbr> 的使用成为流行。。</p>   
3.9.8网页的默认语言可以编程式确定
1）通过使用lang和xml：lang属性来确定。
确定文件的默认语言的重要性：
它允许盲文翻译软件来代替重音字符的控制代码，并插入必要的控制代码，以防止2级盲文收缩的错误创造。
支持多语言的语音合成器将能够定向和改变页面语言的发音和语法，使用正确的发音口音来朗读文本。
标记语言可以受益于技术的未来发展，例如用户无法翻译语言将能够用机器来实现陌生语言之间的翻译。
标记语言还可以在用户使用字典提供定义提供帮助。
样例1：
法语html文件：<html lang="fr"> 
样例2：
xhtml中的lang使用：<html xmlns="http://www.w3.org/1999/xhtml" lang="fr" xml:lang="fr">满足xhtml的需求，同时兼容html
样例3：
当网页内容为application/xhtml+xml时，只使用xml：lang：
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="fr">
<head>
  <title>法语文件</title>
	<meta http-equiv="content-type" content="application/xhtml+xml; charset=utf-8" />
</head>
2）使用lang属性来标记语言的改变
对于网页中插入某种特殊的语言时，该区块的lang或xml：lang属性可以指定为该语言的简写：
样例1：
<blockquote xml:lang="de">
  <p>
    此处是法语，虽然看到的是汉语，大家想想吧。。。。法语。。。。法语。
  </p>
</blockquote>   
3.10鲁棒性
内容必须健壮到可信地被种类繁多的用户代理(包括辅助技术)所解释。
3.10.1兼容：最大化兼容当前和未来的用户代理(包括辅助技术)
1）解析:使用标记语言实现的内容，元素要有完整的开始和结束标签，元素根据其规格进行嵌套，元素不包含重复的属性，任何ID都是唯一的，除非规范允许这些特性。 （A级）
注: 缺少关键特性的开始和结束标签是不完整的，比如一个右尖括号或不匹配的属性值引用标记。
3.10.2名称，角色，值
对于所有用户界面组件（包括但不限于：表单元素，链接和由脚本生成的组件），名称和角色可以编程式确定; 可由用户设置的状态、属性和值可以编程式设置，这些变化通知对用户代理（包括辅助技术）有效。 （A级）
注: 此成功标准主要用于Web作者开发或编写自己的用户界面组件。比如根据规范使用标准HTML控件时，标准HTML控件已经满足这一成功标准。
这个标准是为了确保辅助技术可以收集活跃控件的信息，并不断跟踪用户界面控件的状态变化。
1)在可见label不能使用的时候，使用aria-label提供不可见标签；
对于视觉用户，一个元素的上下文和视觉呈现可以提供足够的信息来 判定该元素的目的。比如，弹出窗口右上角的叉号表明这个控件可以关闭这个窗口；
在某些情况下，当可见的label不能使用是，可根据选择的设计方法，或者通过视觉和上下文来呈现的目的，可以提供aria-label属性来提供name。
在另外的情况，元素可以使用aria-label来提供可获得的name，当html标准标签元素不支持控件的时候，例如：将div设置为contentEditable（可编辑），而不是使用标准表单元素例如使用type=text的输入元素或者文本域来提供丰富的文本编辑经验。
样例1：
弹出框的叉号按钮；
<div id="box">这里有一个弹出框
   <button aria-label="Close" onclick="document.getElementById('box').style.display='none';" class="close-button">X（叉号）</button>			
</div>
样例2：多区域电话号码
<div role="group" aria-labelledby="groupLabel">
  <span id="groupLabel>工作电话</span>
  +<input type="number" aria-label="国家代码">
  <input type="number" aria-label="地区代码">
  <input type="number" aria-label="详细号码">
</div>
2）使用aria-labelledby为用户界面控件提供name
这个技巧用来为用户界面控件提供name，这些name可以被辅助技术阅读。WAI-ARIA使用aria-labelledby将文本与章节、设计、表单元素、图片等联系起来。这个技巧使用aria-labelledby属性连接用户界面控件，例如表单区域；
aria-labelledby可以接受很多id来指向其他网页上的其他元素，使用分隔列表。这个能力将aria-labelledby变得格外有用，在视觉用户使用周围的文字来判定控件目的的时候。使用aria-labelledby可以串联多个文本节点到label，这个文本节点包含状态的样例，这些状态来自其他的网页上的其他文本元素；
即使aria-labelledby的功能与标准html控件类似，仍有些不同：
aria-labelledby可以引用多个文本元素，label只能引用一个；
aria-labelledby可以被应用到多种元素，label元素只能用于表单元素；
点击label焦点自动链接到表单元素，这个不会发生在aria-labelledby。这个行为只有在使用label或者使用JS脚本的时候才会发生。
注：在老版本的浏览器和辅助技术里面，label比aria-labelledby支持的好；
样例1：
标记简单文本区域：使用aria-labelledby为简单文本区域提供标签，当没有文本可用来描述，但是在网页上有其他文本可用来精确标记控件;
<input name="searchtxt" type="text" aria-labelledby="searchbtn">
<input name="searchbtn" id="searchbtn" type="submit" value="Search">
样例2：
标记滑块：使用aria-labelledby为滑块控件提供label，它的标记信息来自临近的文本。
<p><span id="mysldr-lbl">请选择旅行时间</span></p>
<div id="mysldr" role="slider" aria-labelledby="mysldr-lbl"></div>
样例3：
来自多个文本的label；
<label id="l1" for="f3">通知我</label>
<select name="amt" id="f3" aria-labelledby="l1 f3 l2">
  <option value="1">1</option>
  <option value="2">2</option>
</select>
<span id="l2" tabindex="-1">提前多少天</span>
3）使用标记功能暴露出元素的名称和角色，允许用户直接更改的属性可以直接设置，并提供更改通知；
使用html控件和链接；
使用label元素连接文本label和表单控件；
使用框架和内置框架的title的属性；
当label不能使用的时候使用title属性来识别表单元素；
4）使用wai-aria角色来暴露用户界面元素；
使用这个技巧可以定义一个元素的角色，角色role的属性值是wai-aria定义的非抽象值。wai-aria说明文档为每一个角色提供了描述信息，怎样连接其他元素，每个角色的状态和属性。当丰富互联网应用定义新的用户界面小程序，暴露出的role可以让用户更好的理解小程序并与之交互；
样例1：
一个简单的工具条；
wai-aria开发实践文档定义包含三个按钮的工具条。div有一个toolbar属性，图片元素有一个button属性。
关键代码：
<div role="toolbar" 略去部分属性>
<img src="img/btn1.gif"  role="button" 略去部分属性>
全部代码：
 <div role="toolbar"
      tabindex="0" 
      id="customToolbar" 
      onkeydown="return optionKeyEvent(event);"
      onkeypress="return optionKeyEvent(event);"
      onclick="return optionClickEvent(event);"
      onblur="hideFocus()"
      onfocus="showFocus()"
      > 
      <img src="img/btn1.gif" 
           role="button" 
           tabindex="-1" 
           alt="Home" 
           id="b1" 
           title="Home">
      <img src="img/btn2.gif" 
           role="button" 
           tabindex="-1" 
           alt="Refresh" 
           id="b2" 
           title="Refresh">
     <img src="img/btn3.gif" 
           role="button" 
           tabindex="-1" 
           alt="Help" 
           id="b3" 
           title="Help"> 
 </div>  
样例2：
树形应用；
tree、treeitem、group的role值用来辨别树和它的结构。
role="tree"表示树形
role="treeitem"表示树结构选项
role="group"表示组合并
关键代码：
<ul role="tree" tabindex="0">
  <li role="treeitem">鸟类</li>
  <li role="treeitem">猫
    <ul role="group">
全部代码：
<ul role="tree" tabindex="0">
  <li role="treeitem">视障工程师</li>
  <li role="treeitem">2年
    <ul role="group">
      <li role="treeitem">孟琦</li>
      <li role="treeitem">阿彪</li>
    </ul>
  </li>
  <li role="treeitem">
    <ul role="group">
      <li role="treeitem">1年
        <ul role="group">
          <li role="treeitem">广锐</li>
          <li role="treeitem">广荣</li>
          <li role="treeitem">鸿利</li>
        </ul>
      </li>
    </ul>
  </li>
</ul>
5）使用wai-aria状态和属性来暴露用户界面元素的状态；
这个技巧使用来暴露用户界面元素的状态属性和值，这样就可以被辅助技术读取和设置，辅助技术也可以被告知这些值的改变。wai-aria说明提供每个属性和每个role的正式描述。当丰富互联网应用定义新的用户界面小程序，暴露出的role可以让用户更好的理解小程序并与之交互；
样例1：切换按钮
有role的值为button为小程序当有aira-pressed属性的时候可以作为切换按钮。当aria-pressed为真时，按钮在按下的状态。当aria-pressed为假时，未被按下。如果aria-pressed不存在时，按钮只是个简单的控制按钮。
全部代码：
<li id="bold1"  
    class="toggleButton"
    role="button"
    tabindex="0"
    aria-pressed="false"
    aria-labelledby="bold_label"
    aria-controls="text1">//此时列表只是个控制按钮
    <img src="http://www.oaa-accessibility.org/media/examples/images/button-bold.png" alt="bold text" align="middle">
</li>
脚本程序：用来切换aria-pressed的true和false的状态；
function togglePressed(id) {
    // reverse the aria-pressed state
    if ($(id).attr('aria-pressed') == 'true') {
      $(id).attr('aria-pressed', 'false');
    }
    else {
      $(id).attr('aria-pressed', 'true');
    }
  }
样例2：滑块
一个role为slider的小程序，允许用户在一个规定范围内选择一个值。滑块通过滑块的大小和位置来呈现的当前值和范围。这些滑块的属性通过aria-valuemin、aria-valuemax、aria-valuenow来呈现；
以下为ajax无障碍样例，展示了使用js创建滑块。
var handle = '<img 
id="' + id + '" 
class="' + (this.vert == true ? 'v':'h') +'sliderHandle"+'src="http://www.oaa-accessibility.org/media/examples/images/slider_' + (this.vert == true ? 'v':'h') + '.png" ' + 'role="slider"' +'aria-valuemin="' + this.min +'" 'aria-valuemax="' + this.max +'" 
aria-valuenow="' + (val == undefined ? this.min : val) +'" 
aria-labelledby="' + label +'" 
aria-controls="' + controls + '" 
tabindex="0"></img>';
以下通过JS刷新aria-valuenow属性
slider.prototype.positionHandle = function($handle, val) {
    此处省略部分代码
   // 设置aria-valuenow的滑动位置
  $handle.attr('aria-valuenow', val);
   此处省略部分代码
  }
