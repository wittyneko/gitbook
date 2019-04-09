# View

### 系统属性

首先了解下Android系统属性和样式如何查看。很多问题不需要一味的Google搜索，只要你查看系统属性，稍加了解都可以迎刃而解。Android系统资源和属性源码在SDk`platforms/android-23/data`目录下，通过Android Studio可以很方便的在`External Libraries` 对应版本的`res`目录下查看，跟应用源码的资源目录一样，同样有`values` `deawable` `layout` 等目录，我们要查看都属性都在`values`下。

![api 23 res](http://upload-images.jianshu.io/upload_images/1845254-2c219bbefe8d975b.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

`attrs.xml`系统属性定义文件\(`android:id` `android:backgound` 都在这里定义\)，`styles.xml` 默认样式定义，`themes.xml` 默认主题定义。样式和主题的区别在以后自定义控件再讲，这里要注意的是不同版本会读取不同的样式和主题文件。4.0以后新增HOLO `themes_holo.xml`，5.0又新增Meterial Design `themes_meterial.xml`，4.0以下读取themes主题，5.0以下读取themes\_holo主题，5.0以上读取themes\_meterial主题，不同主题对应着不同样式，不同版本样式都有很大区别。

View作为Android视图界面的基类，所有能看见的都是View及其子类。虽然实际开发多数使用的是View的子类很少直接使用View，但是View的属性可以更好的了解View的共同特性。了解它的属性是很有必要的，需要注意的是`layout_width` `layout_height` 和 `margin`系列由ViewGroup确定并不是View属性，enum和flag的区别在于单选和多选。

View的属性特别多不可能全部了解记忆，只需要记住一些常用的属性及其对应的方法。那为啥要了解呢，开头说了只要对属性有叫深入的了解都可以迎刃而解。View的属性内容多得有点恐怖。

| 属性 | 类型 | 说明 |
| :--- | :--- | :--- |
| id | reference | 引用ID |
| tag | string | tag标签 |
| scrollX | dimension | 水平滑动距离 |
| scrollY | dimension | 垂直滑动距离 |
| background | reference/color | 背景图片/背景色 |
| padding | dimension | 内部上下左右填充距离 |
| paddingLeft | dimension | 左边填充距离 |
| paddingRight | dimension | 右边填充距离 |
| paddingTop | dimension | 上边填充距离 |
| paddingBottom | dimension | 下边填充距离 |
| focusable | boolean | 可获取焦点 |
| focusableInTouchMode | boolean | 触摸事件可获取焦点 |
| visibility | enum \(visible/invisible/gone\) | 是否显示View |
| fitsSystemWindows | boolean | 适配系统窗口 |
| scrollbars | flag \(none/horizontal/vertical\) | 是否显示滚动条 |
| scrollbarStyle | emum | 滚动条样式 |
| isScrollContainer | boolean | 是否作为可滚动容器使用 |
| fadeScrollbars | boolean | 自动隐藏 |
| scrollbarFadeDuration | integer | 自动隐藏时间 |
| scrollbarDefaultDelayBeforeFade | integer | 淡化效果开始时间 |
| scrollbarSize | dimension | 滚动条宽度 |
| scrollbarThumbHorizontal | reference | 水平滚动条颜色 |
| scrollbarThumbVertical | reference | 垂直滚动条颜色 |
| scrollbarTrackHorizontal | reference | 水平滚动条背景 |
| scrollbarTrackVertical | reference | 垂直滚动条背景 |
| scrollbarAlwaysDrawHorizontalTrack | boolean | 始终显示水平滚动条 |
| scrollbarAlwaysDrawVerticalTrack | boolean | 始终显示垂直滚动条 |
| fadingEdge | flag \(none/horizontal/vertical\) | 显示边界阴影 |
| requiresFadingEdge | flag \(none/horizontal/vertical\) | 滚动时边缘是否褪色 |
| fadingEdgeLength | dimension | 边界阴影长度 |
| nextFocusLeft | reference | 左边下个焦点控件，方向切换 |
| nextFocusRight | reference | 右边下个焦点控件 |
| nextFocusUp | reference | 上边下个焦点控件 |
| nextFocusDown | reference | 下边下个焦点控件 |
| nextFocusForward | reference | 下个焦点控件，tab切换 |
| clickable | boolean | 允许点击 |
| longClickable | boolean | 允许长按 |
| contextClickable | boolean |  |
| saveEnabled | boolean | 配置改变等情况，保存View的数据 |
| filterTouchesWhenObscured | boolean | 所在窗口被其它可见窗口遮住时,是否过滤触摸事件 |
| drawingCacheQuality | enum \(auto/low/high\) | 半透明质量 |
| keepScreenOn | boolean | 强制手机屏幕一直打开 |
| duplicateParentState | boolean | 从父容器中获取绘图状态 |
| minHeight | dimension | 最小高度 |
| minWidth | dimension | 最小宽度 |
| soundEffectsEnabled | boolean | 点击时是否使用音效 |
| hapticFeedbackEnabled | boolean | 触感反馈\(振动\) |
| contentDescription | string | 组件的内容描述信息，临时放一点字符串数据 |
| accessibilityTraversalBefore | integer | 可访问性遍历，被访问之前先访问设置的组件 |
| accessibilityTraversalAfter | integer | 可访问性遍历，被访问之后访问设置的组件 |
| onClick | string | 单击事件绑定监听器 |
| overScrollMode | enum \(always/ ifContentScrolls/never\) | 拉到尽头的行为 2.3之前 |
| alpha | float | 透明度属性,  0 \(完全透明\) ~ 1 \(完全不透明\) |
| elevation | dimension | z 轴深度 |
| translationX | dimension | X方向上的位移 |
| translationY | dimension | Y方向上的位移 |
| translationZ | dimension | Z方向上的位移 |
| transformPivotX | dimension | 旋转时旋转中心的X坐标 |
| transformPivotY | dimension | 旋转时旋转中心的Y坐标 |
| rotation | float | 旋转的角度 |
| rotationX | float | 绕X轴旋转的角度 |
| rotationY | float | 绕Y轴旋转的角度 |
| scaleX | float | 水平方向的缩放比 |
| scaleY | float | 水平方向的缩放比 |
| verticalScrollbarPosition | enum \(defaultPosition/left/right\) | 滚动条的位置 |
| layerType | enum \(none/software/hardware\) | 指定层的类型 |
| layoutDirection | enum \(ltr/rtl/inherit/locale\) | 布局图纸的方向 |
| textDirection | integer - enum | 文本的显示方向 |
| textAlignment | integer - enum | 文本的显示对齐方式 |
| importantForAccessibility | integer - enum \(auto/yes/no/ noHideDescendants\) | 无障碍服务的重要性 |
| accessibilityLiveRegion | integer - enum \(none/polite/assertive\) | 无障碍服务 组件改变时是否通知用户，不通知，通知、打断语音. |
| labelFor | reference |  |
| theme | reference | 主题 |
| transitionName | string |  |
| nestedScrollingEnabled | boolean | 允许嵌套滑动 |
| stateListAnimator | reference | 5.0点击阴影效果 |
| backgroundTint | color | 背景色 |
| backgroundTintMode | enum | 背景色的混合模式 |
| outlineProvider | enum | 指定阴影\(轮廓\)的判定方式 |
| foreground | reference/color | 前景图片/前景色 |
| foregroundGravity | enum | 前景图片位置, 默认 left 和 top |
| foregroundInsidePadding | boolean |  |
| foregroundTint | color | 前景颜色 |
| foregroundTintMode | enum | 前景图片的混合模式, 默认 SRC\_IN |
| scrollIndicators | flag | 滑动指示器 |

附：  
[android之View属性](http://www.jianshu.com/p/875a9adb4952)  
[Android View 组件](http://www.bozhiyue.com/anroid/wenzhang/2016/0516/103333.html)  
[Android layout属性详细说明](http://www.cnblogs.com/skywang12345/archive/2013/06/15/AndroidAttr.html)  
[\[教程\] 【也说Android开发】第三讲 Layout文件属性讲解](http://blog.chinaunix.net/uid-29134536-id-3982048.html)

### 常用方法

### 事件分发

