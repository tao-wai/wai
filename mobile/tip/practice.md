## 最佳实践

### 1. 自定义朗读文本

> iOS

```js
//若箭头号是label实现的，则将其accessibilityLabel设置为空
arrowLabel.accessibilityLabel = @"";

//设置视图的accessibilityLabel文本
self.accessibilityLabel = @"收件箱";
self.accessibilityHint = @"双击展开";
```

> Android

在xml中添加属性项 

```
android:contentDescription="@string/xxx"
```

或者在代码中设置view的contentDescription 

```
view.setContentDescription("双击展开")
```

### 2. 自定义朗读属性

> iOS

```js
//设置控件的提示音及类型
self.accessibilityHint = @"输入搜索关键字";
self.accessibilityTraits = UIAccessibilityTraitSearchField;
```

> Android

参考问题1