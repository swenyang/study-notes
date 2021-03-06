# 事件系统

## SyntheticEvent

所有的事件handler会接收一个`SyntheticEvent`的实例，`SyntheticEvent`是封装了浏览器的原生事件的跨浏览器事件。`SyntheticEvent`相比原生事件优点在于几乎能在所有浏览器运行一致，除此之外，它有和原生事件一致的接口，包括`stopPropagation()`和`preventDefault()`。

如果确实需要访问浏览器的原生事件，可以通过`nativeEvent`属性来访问获得。所有的`SyntheticEvent`都拥有以下的属性：

```java
boolean bubbles
boolean cancelable
DOMEventTarget currentTarget
boolean defaultPrevented
number eventPhase
boolean isTrusted
DOMEvent nativeEvent
void preventDefault()
boolean isDefaultPrevented()
void stopPropagation()
boolean isPropagationStopped()
DOMEventTarget target
number timeStamp
string type
```

注意，React v0.14之后`return false`将不会再停止事件的传播。需要适当的手动调用`e.stopPropagation()`或`e.preventDefault()`来停止传播。

## 事件的对象池

`SyntheticEvent`在React里面有对象池来缓存。这意味着`SyntheticEvent`可以被重用，在事件回调触发过后，所有的属性将被置空。对象池的目的是为了优化性能，另一方面也意味着你不能异步地访问事件对象。

```js
function onClick(event) {
  console.log(event); // => nullified object.
  console.log(event.type); // => "click"
  var eventType = event.type; // => "click"

  setTimeout(function() {
    console.log(event.type); // => null
    console.log(eventType); // => "click"
  }, 0);

  this.setState({clickEvent: event}); // Won't work. this.state.clickEvent will only contain null values.
  this.setState({eventType: event.type}); // You can still export event properties.
}
```

注意：如果想要异步访问事件对象，需要调用`event.persist()`，这样做后`SyntheticEvent`将被移出对象池，从而允许用户保持引用和自由访问。

## 支持的事件

React标准化了所有的事件，从而事件在所有浏览器都有相同的属性。

下面的所有事件都是在冒泡阶段触发的，如果要注册在捕获阶段的事件，可以在事件名称后加`Capture`，比如`onClick`=\>`onClickCapture`。

- 剪贴板事件

    事件名称：

    ```js
    onCopy onCut onPaste
    ```

    属性：

    ```java
    DOMDataTransfer clipboardData
    ```

- 复合事件

    事件名称：

    ```js
    onCompositionEnd onCompositionStart onCompositionUpdate
    ```

    属性：

    ```java
    string data
    ```

- 键盘事件

    事件名称：

    ```js
    onKeyDown onKeyPress onKeyUp
    ```

    属性：

    ```java
    boolean altKey
    number charCode
    boolean ctrlKey
    boolean getModifierState(key)
    string key
    number keyCode
    string locale
    number location
    boolean metaKey
    boolean repeat
    boolean shiftKey
    number which
    ```


- 焦点事件

    事件名称：

    ```js
    onFocus onBlur
    ```

    属性：

    ```java
    DOMEventTarget relatedTarget
    ```

    注意：焦点事件在所有的React DOM元素都会有，不仅仅是表单元素。

- 表单事件

    事件名称：

    ```js
    onChange onInput onSubmit
    ```

    关于表单事件的更多信息，可以参考[React表单](/react/3.React表单.md)

- 鼠标事件

    事件名称：

    ```js
    onClick onContextMenu onDoubleClick onDrag onDragEnd onDragEnter onDragExit
    onDragLeave onDragOver onDragStart onDrop onMouseDown onMouseEnter onMouseLeave
    onMouseMove onMouseOut onMouseOver onMouseUp
    ```

    跟常规的冒泡不一样，`onMouseEnter`和`onMouseLeave`事件从离开的元素传播到进入的元素，并且没有捕获阶段。

    属性：

    ```java
    boolean altKey
    number button
    number buttons
    number clientX
    number clientY
    boolean ctrlKey
    boolean getModifierState(key)
    boolean metaKey
    number pageX
    number pageY
    DOMEventTarget relatedTarget
    number screenX
    number screenY
    boolean shiftKey
    ```


- 选择事件

    事件名称：

    ```js
    onSelect
    ```


- 触摸事件

    事件名称：

    ```js
    onTouchCancel onTouchEnd onTouchMove onTouchStart
    ```

    属性：

    ```java
    boolean altKey
    DOMTouchList changedTouches
    boolean ctrlKey
    boolean getModifierState(key)
    boolean metaKey
    boolean shiftKey
    DOMTouchList targetTouches
    DOMTouchList touches
    ```


- UI事件

    事件名称：

    ```js
    onScroll
    ```

    属性：

    ```java
    number detail
    DOMAbstractView view
    ```


- 滚轮事件

    事件名称：

    ```js
    onWheel
    ```

    属性：

    ```java
    number deltaMode
    number deltaX
    number deltaY
    number deltaZ
    ```


- 媒体事件

    事件名称：

    ```js
    onAbort onCanPlay onCanPlayThrough onDurationChange onEmptied onEncrypted
    onEnded onError onLoadedData onLoadedMetadata onLoadStart onPause onPlay
    onPlaying onProgress onRateChange onSeeked onSeeking onStalled onSuspend
    onTimeUpdate onVolumeChange onWaiting
    ```


- 图片事件

    事件名称：

    ```js
    onLoad onError
    ```


- 动画事件

    事件名称：

    ```js
    onAnimationStart onAnimationEnd onAnimationIteration
    ```

    属性：

    ```java
    string animationName
    string pseudoElement
    float elapsedTime
    ```


- 过渡事件

    事件名称：

    ```js
    onTransitionEnd
    ```

    属性：

    ```java
    string propertyName
    string pseudoElement
    float elapsedTime
    ```
