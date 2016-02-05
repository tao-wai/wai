## 最佳实践

### 1. 一个焦点覆盖到多个元素

> iOS

对于一个焦点覆盖到多个元素，且这多个元素无法切换焦点的情况，可以通过设置其AccessibilityElements的方式进行处理。

#### 为该容器视图A中无焦点的元素创建UIAccessibilityElements对象

```js
//[注]elements的frame坐标是相较于整个windows而言的，因此想要准确拿到这个位置，应该传入当前VC的view来作为相对位置
UIAccessibilityElement *elements = [[UIAccessibilityElement alloc] initWithAccessibilityContainer:label];
elements.accessibilityLabel      = label.text;
CGRect frame = [label convertRect:label.frame toView:self.viewController.view];
elements.accessibilityFrame      =  frame;
```

#### 在容器视图中进行如下操作

**Step 1: 实现了UIAccessibilityContainer方法的容器视图A不能是一个accessibility elements，因为用户是与它中间的内容交互，而不是容器本身，因此要进行以下步骤**

```js
self.isAccessibilityElement = NO; //默认
```

**Step 2: 实现协议**

```js
- (NSInteger)accessibilityElementCount
{
    return self.elements.count;
}

- (id)accessibilityElementAtIndex:(NSInteger)index
{
    if (index >= 0 && index < self.elements.count) {
        return [self.accessibilityElements objectAtIndex:index];
    }
    return nil;
}

- (NSInteger)indexOfAccessibilityElement:(id)element
{
    if (element) {
        return [self.accessibilityElements indexOfObject:element];
    }
    return 0;
}

- (NSArray *)accessibilityElements
{
    return self.elements;
}
```

> Android

对于焦点，可以通过setFocusable()来设置view能否具有获取焦点的资格。对于一个焦点覆盖多个子元素，可以通过父容器控制child View获取焦点的能力，比如是否阻止child View获取焦点。

调用方法`setDescendantFocusability(int)`

### 2. 焦点顺序不符合逻辑

> iOS

**Step1: 将其shouldGroupAccessibilityChildren设置为YES。此时，大部分要求可以得到满足，即顺序：从左至右，从上至下**
```js
self.shouldGroupAccessibilityChildren = YES;
```

他有三个常量可供设置 

* FOCUS_BEFORE* _DESCENDANTS : ViewGroup本身先对焦点进行处理，如果没有处理则分发给child View进行处理

* FOCUS_AFTER_DESCENDANTS : 先分发给Child View进行处理，如果所有的Child View都没有处理，则自己再处理

* FOCUS_BLOCK_DESCENDANTS : ViewGroup本身进行处理，不管是否处理成功，都不会分发给ChildView进行处理

上述实现也可以在XML中通过设置android:descendantFocusability属性达到同样的效果。

**Step2: 若是需要更深层次的定义顺序，可以实现下面的协议。与问题1类似**
-(BOOL)isAccessibilityElement{
    return NO;
}

-(NSInteger)accessibilityElementCount{
    return self.subviews.count;
}

-(id)accessibilityElementAtIndex:(NSInteger)index{
    return [self.subviews objectAtIndex:index];
}

-(NSInteger)indexOfAccessibilityElement:(id)element{
    return [self.subviews indexOfObject:element];
}


> Android

系统焦点顺序是在某一方向上邻近的组件，如果需要自定义焦点顺序，可以覆写下列XML属性的布局文件：`nextFocusDown`，`nextFocusLeft`，`nextFocusRight`，和`nextFocusUp`设置他们的值来明确焦点从当前界面移动下个界面的Id。

### 3. 部分控件无焦点

> iOS

首先，需要明确的是，在iOS系统中icon和文本图片不是从UIView或者UIControl中集成而来的，所以期本身是不能够自动访问的。因此，针对这部分问题，可以参考问题1的方法，为在这个容器中无焦点的对象定义其accessibilityElements.
另外，在实战中会发现，UILabel和单独的一个ImageView不能作为焦点对焦，如果有需要可以参考问题一的解决方案进行解决。

