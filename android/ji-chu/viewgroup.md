# ViewGroup

## 属性

ViewGroup继承View后增加的属性不多，但是有几个相关的属性集合和属性需要注意

`ViewGroup`

| 属性 | 类型 | 说明 |
| :--- | :--- | :--- |
| animateLayoutChanges | boolean | 布局发生变化时添加动画效果 |
| clipChildren | boolean | 限制子View在其范围内，默认true |
| clipToPadding | boolean | 去掉padding的绘制，默认true |
| layoutAnimation | refrence | ViewGroup动画效果 |
| animationCache | boolean | 子布局也有动画效果 |
| persistentDrawingCache | flag  \(none/animation/scrolling/all\) | 高速缓存的持久性 |
| alwaysDrawnWithCache | boolean | 子布局是否应用绘图的高速缓存 |
| addStatesFromChildren | boolean | 是否应用子布局的背景 |
| descendantFocusability | enum \(beforeDescendants/ afterDescendants/ blocksDescendants\) | 子布局焦点获取方式 |
| touchscreenBlocksFocus | boolean |  |
| splitMotionEvents | boolean | 否传递touch事件到子布局 |
| layoutMode | enum  \(clipBounds/opticalBounds\) | 边界是否留白 |
| transitionGroup | boolean | 过渡整体 |

附：  
[http://blog.163.com/allegro\_tyc/blog/static/33743768201371301526104/](http://blog.163.com/allegro_tyc/blog/static/33743768201371301526104/) [http://blog.csdn.net/jaysong2012/article/details/41047587](http://blog.csdn.net/jaysong2012/article/details/41047587) [http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2016/0711/4490.html](http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2016/0711/4490.html)

`ViewGroup_Layout` 子控件属性，通常使用其扩展ViewGroup\_MarginLayout和其它子类而不直接使用ViewGroup\_Layout

| 属性 | 类型 | 说明 |
| :--- | :--- | :--- |
| layout\_width | dimension & enum  \(fill\_parent/match\_parent/wrap\_content\) | 子控件宽度 |
| layout\_height | dimension & enum | 子控件高度 |

`ViewGroup_MarginLayout` 扩展ViewGroup\_Layout加入margin，需要知道的是这些属性并不是View的属性，虽然我们在布局文件填写参数的时候写在View下面，但是系统读取后，由ViewGroup生成一个`LayoutParams`类赋值给View，具体LayoutParams的类型由ViewGroup确定。

| 属性 | 类型 | 说明 |
| :--- | :--- | :--- |
| layout\_width | dimension & enum \(fill\_parent/match\_parent/wrap\_content\) | 子控件宽度 |
| layout\_height | dimension & enum | 子控件高度 |
| layout\_margin | dimension | 与父控件的偏移量 |
| layout\_marginLeft | dimension | 具体方向偏移量 |
| layout\_marginTop | dimension | 具体方向偏移量 |
| layout\_marginRight | dimension | 具体方向偏移量 |
| layout\_marginBottom | dimension | 具体方向偏移量 |
| layout\_marginStart | dimension | 具体方向偏移量 |
| layout\_marginEnd | dimension | 具体方向偏移量 |

layout\_gravity\(flag\) 常见LayoutParams派生类都具有该属性，子控件对齐方式，会和margin冲突； gravity\(flag\) 常见View和ViewGroup派生类都具有该属性，自身对齐方式； 属性内容是一样的，但记得不是同一个参数作用对象不同，具体意义看名字可以知道不具体说明了

| 属性 | 说明 |
| :--- | :--- |
| top | ～ |
| bottom |  |
| left |  |
| right |  |
| center |  |
| center\_vertical |  |
| center\_horizontal |  |
| fill |  |
| fill\_vertical |  |
| fill\_horizontal |  |
| clip\_vertical |  |
| clip\_horizontal |  |
| start |  |
| end | ～ |

