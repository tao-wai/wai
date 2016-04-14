## 最佳实践

### 1. 利用label元素的for属性

给表单项加一个id，并与label的`for`属性关联起来。

```
<label for=“contentType”>Content-Type</label>
<input type="text" class="form-control ng-pristine ng-valid" ng-model="formData.contentType" id=“contentType”>
```


#### 2. 不方便试用label标签的，可以利用`aria-label`和`aria-labelledby`属性


```
<tr>
    <td><input type="text" class="form-control ng-pristine ng-valid" ng-model="formData.contentType" aria-label=“Content-Type”></td>
</tr>
```
`aria-labelledby`属性需要给文案添加id

```
<tr>
	<td class="nowrap" id=“contentType”>Content-Type</td>
    <td><input type="text" class="form-control ng-pristine ng-valid" ng-model="formData.contentType" aria-labelledby=“contentType”></td>
</tr>
```


这种方式也适用于模拟表单项的情况，这时候还需要配合`tabindex=0`来使用，使其能获取键盘焦点。

#### 3.用label标签将表单包裹起来。（不推荐）
见下

```
<label>Content-Type
<input type="text" class="form-control ng-pristine ng-valid" ng-model="formData.contentType" id=“contentType”>
</label>
```
很多旧的代码喜欢采取这种方式，这样读屏软件也能读出对应表单的功能，但是这是不规范的用法，不推荐。
