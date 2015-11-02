## 最佳实践
### 描述
我们可以利用[WAI-ARIA](http://www.w3.org/TR/wai-aria/)标准，它对于网页富交互指定了一系列描述性的attribute，通常用于:
1. 描述伪元素，例如利用`div`模拟的`button`。
2. 描述伪元素对应的交互行为，例如浮出层，对话框弹出，下拉列表展开。

本案例用到 :

- [`role`](http://www.w3.org/TR/wai-aria/roles#role_definitions): 用于描述伪元素的真实角色。
- `aria-pressed`: `button`这个`role`对应的`aria`状态，是否被按下。
- `aria-labelledby`: 类似`label`的作用，指定说明文案的ID。
- `aria-hidden`: `dialog`这个`role`对应的`aria`状态，是否被隐藏。

这些状态属性会被读屏软件读到，更多的属性可以查看文档。

### 方案
触发按钮
```
<div id="J_Trigger"  tabindex="0" role="button"  aria-pressed="false">点击打开弹窗</div>
```

浮层结构

```
<div id="J_Overlay" role="dialog" tabindex="0" aria-labelledby="overlay-header" style="display:none;" aria-hidden="true">
  <a href="javascript:void('close')" id="J_Close" role="button"></a>
  <div id="overlay-header">收藏</div>
  <div id="overlay-body"></div>
</div>
```

脚本，这里采用JQuery的写法
```
$('#J_Trigger').on('click',function(){
  $('#J_Overlay').attr('aria-hidden', false).show();
  $('#J_Close').focus();//定位到关闭按钮
})

$('#J_Close').on('click',function(){
  $('#J_Overlay').attr('aria-hidden', true).hide();
  $('#J_Trigger').focus();//关闭重新定位到trigger
})
```

**一般打开浮层先定位到关闭按钮，这个是每个浮层都有的。**

### 原则：
> 有焦点，有描述；哪里进，哪里出；能关闭，能手输。