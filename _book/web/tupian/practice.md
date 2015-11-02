## 最佳实践

### 1. 非装饰性图片无替代文本
#### 利用alt属性

```
<img alt="信息无障碍联盟LOGO" src="img001.gif" />
```

### 2. 图片链接缺少目的文本
#### 在alt属性中描述目的
```
<a href="routes.html"><img src="topo.gif" alt="去到无障碍论坛的路线" /></a>
```
#### 利用链接文案
```
<a href="home.html"><br/>
  <img src="house.gif" alt="">去到无障碍主页
</a>
```

#### alt和链接文案配合使用
```
<a href="prod_123_feedback.htm">反馈
  <img src="response.gif" width="15" height="15" alt="收到响应图标" />
</a>
```

### 3. 图片按钮缺少目的文本
#### 利用title属性
```
<button type="button" title="信息无障碍产品联盟"><img src="logo.jpg" alt=""></button>
```
#### 利用alt属性
```
<button type="button" ><img src="1.jpg" alt="信息无障碍研究会"></button>
```

### 4. 图片按钮/链接不能响应回车键
#### 添加键盘响应事件
```
<img src="图片按钮" onkeyup="handle()">
```

### 5. 图片按钮控件类型朗读不正确
#### 利用role属性
```
<img src="图片按钮" onkeyup="handle()" role="button">
```

### 6. 图片按钮无法获得键盘焦点
#### 利用tabindex属性
网页元素中，只有超链接和表单元素是默认支持获取焦点的，其它元素要被focus到，就需要利用`tabindex`属性
```
//去掉 onfocuse="this.blur()" 
<img src="图片按钮" onkeyup="handle()" role="button" tabindex="0">
```






