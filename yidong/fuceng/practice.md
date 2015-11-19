## 最佳实践

### 1. 浮层透传

> iOS

此时需要屏蔽底层浮层的可读属性，可以将底层视图隐藏，或者将其accessibilityElementsHidden设置为NO

```js
view.accessibilityElementsHidden = NO;
```

> Android

在浮层切换的时候，在浮层的view上设置android:focusable=true，这样在新浮层的拉起的时候浮层有机会获取焦点。


### 2. 浮层不能关闭

> iOS

首先，确保当前浮层拥有一个UIButton，或者浮层本身最上面的视图是一个UIView的对象。此时，可以对应到焦点，进行浮层的关闭。

> Android

因为存在物理的Back按键，这个问题在Android上并不存在。




