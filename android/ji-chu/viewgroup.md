# ViewGroup

## 属性

ViewGroup继承View后增加的属性不多，但是有几个相关的属性集合和属性需要注意

`ViewGroup`

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x5C5E;&#x6027;</th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">animateLayoutChanges</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x5E03;&#x5C40;&#x53D1;&#x751F;&#x53D8;&#x5316;&#x65F6;&#x6DFB;&#x52A0;&#x52A8;&#x753B;&#x6548;&#x679C;</td>
    </tr>
    <tr>
      <td style="text-align:left">clipChildren</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x9650;&#x5236;&#x5B50;View&#x5728;&#x5176;&#x8303;&#x56F4;&#x5185;&#xFF0C;&#x9ED8;&#x8BA4;true</td>
    </tr>
    <tr>
      <td style="text-align:left">clipToPadding</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x53BB;&#x6389;padding&#x7684;&#x7ED8;&#x5236;&#xFF0C;&#x9ED8;&#x8BA4;true</td>
    </tr>
    <tr>
      <td style="text-align:left">layoutAnimation</td>
      <td style="text-align:left">refrence</td>
      <td style="text-align:left">ViewGroup&#x52A8;&#x753B;&#x6548;&#x679C;</td>
    </tr>
    <tr>
      <td style="text-align:left">animationCache</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x5B50;&#x5E03;&#x5C40;&#x4E5F;&#x6709;&#x52A8;&#x753B;&#x6548;&#x679C;</td>
    </tr>
    <tr>
      <td style="text-align:left">persistentDrawingCache</td>
      <td style="text-align:left">
        <p>flag</p>
        <p>(none/animation/scrolling/all)</p>
      </td>
      <td style="text-align:left">&#x9AD8;&#x901F;&#x7F13;&#x5B58;&#x7684;&#x6301;&#x4E45;&#x6027;</td>
    </tr>
    <tr>
      <td style="text-align:left">alwaysDrawnWithCache</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x5B50;&#x5E03;&#x5C40;&#x662F;&#x5426;&#x5E94;&#x7528;&#x7ED8;&#x56FE;&#x7684;&#x9AD8;&#x901F;&#x7F13;&#x5B58;</td>
    </tr>
    <tr>
      <td style="text-align:left">addStatesFromChildren</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x662F;&#x5426;&#x5E94;&#x7528;&#x5B50;&#x5E03;&#x5C40;&#x7684;&#x80CC;&#x666F;</td>
    </tr>
    <tr>
      <td style="text-align:left">descendantFocusability</td>
      <td style="text-align:left">
        <p>enum</p>
        <p>(beforeDescendants/</p>
        <p>afterDescendants/</p>
        <p>blocksDescendants)</p>
      </td>
      <td style="text-align:left">&#x5B50;&#x5E03;&#x5C40;&#x7126;&#x70B9;&#x83B7;&#x53D6;&#x65B9;&#x5F0F;</td>
    </tr>
    <tr>
      <td style="text-align:left">touchscreenBlocksFocus</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">splitMotionEvents</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x5426;&#x4F20;&#x9012;touch&#x4E8B;&#x4EF6;&#x5230;&#x5B50;&#x5E03;&#x5C40;</td>
    </tr>
    <tr>
      <td style="text-align:left">layoutMode</td>
      <td style="text-align:left">
        <p>enum</p>
        <p>(clipBounds/opticalBounds)</p>
      </td>
      <td style="text-align:left">&#x8FB9;&#x754C;&#x662F;&#x5426;&#x7559;&#x767D;</td>
    </tr>
    <tr>
      <td style="text-align:left">transitionGroup</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left"><b>&#x8FC7;&#x6E21;&#x6574;&#x4F53;</b>
      </td>
    </tr>
  </tbody>
</table>附： [http://blog.163.com/allegro\_tyc/blog/static/33743768201371301526104/](http://blog.163.com/allegro_tyc/blog/static/33743768201371301526104/) [http://blog.csdn.net/jaysong2012/article/details/41047587](http://blog.csdn.net/jaysong2012/article/details/41047587) [http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2016/0711/4490.html](http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2016/0711/4490.html)

`ViewGroup_Layout` 子控件属性，通常使用其扩展ViewGroup\_MarginLayout和其它子类而不直接使用ViewGroup\_Layout

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x5C5E;&#x6027;</th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">layout_width</td>
      <td style="text-align:left">
        <p>dimension &amp; enum</p>
        <p>(fill_parent/match_parent/wrap_content)</p>
      </td>
      <td style="text-align:left">&#x5B50;&#x63A7;&#x4EF6;&#x5BBD;&#x5EA6;</td>
    </tr>
    <tr>
      <td style="text-align:left">layout_height</td>
      <td style="text-align:left">dimension &amp; enum</td>
      <td style="text-align:left">&#x5B50;&#x63A7;&#x4EF6;&#x9AD8;&#x5EA6;</td>
    </tr>
  </tbody>
</table>`ViewGroup_MarginLayout` 扩展ViewGroup\_Layout加入margin，需要知道的是这些属性并不是View的属性，虽然我们在布局文件填写参数的时候写在View下面，但是系统读取后，由ViewGroup生成一个`LayoutParams`类赋值给View，具体LayoutParams的类型由ViewGroup确定。

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x5C5E;&#x6027;</th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">layout_width</td>
      <td style="text-align:left">
        <p>dimension &amp; enum</p>
        <p>(fill_parent/match_parent/wrap_content)</p>
      </td>
      <td style="text-align:left">&#x5B50;&#x63A7;&#x4EF6;&#x5BBD;&#x5EA6;</td>
    </tr>
    <tr>
      <td style="text-align:left">layout_height</td>
      <td style="text-align:left">dimension &amp; enum</td>
      <td style="text-align:left">&#x5B50;&#x63A7;&#x4EF6;&#x9AD8;&#x5EA6;</td>
    </tr>
    <tr>
      <td style="text-align:left">layout_margin</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">&#x4E0E;&#x7236;&#x63A7;&#x4EF6;&#x7684;&#x504F;&#x79FB;&#x91CF;</td>
    </tr>
    <tr>
      <td style="text-align:left">layout_marginLeft</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">&#x5177;&#x4F53;&#x65B9;&#x5411;&#x504F;&#x79FB;&#x91CF;</td>
    </tr>
    <tr>
      <td style="text-align:left">layout_marginTop</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">&#x5177;&#x4F53;&#x65B9;&#x5411;&#x504F;&#x79FB;&#x91CF;</td>
    </tr>
    <tr>
      <td style="text-align:left">layout_marginRight</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">&#x5177;&#x4F53;&#x65B9;&#x5411;&#x504F;&#x79FB;&#x91CF;</td>
    </tr>
    <tr>
      <td style="text-align:left">layout_marginBottom</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">&#x5177;&#x4F53;&#x65B9;&#x5411;&#x504F;&#x79FB;&#x91CF;</td>
    </tr>
    <tr>
      <td style="text-align:left">layout_marginStart</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">&#x5177;&#x4F53;&#x65B9;&#x5411;&#x504F;&#x79FB;&#x91CF;</td>
    </tr>
    <tr>
      <td style="text-align:left">layout_marginEnd</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">&#x5177;&#x4F53;&#x65B9;&#x5411;&#x504F;&#x79FB;&#x91CF;</td>
    </tr>
  </tbody>
</table>layout\_gravity\(flag\) 常见LayoutParams派生类都具有该属性，子控件对齐方式，会和margin冲突； gravity\(flag\) 常见View和ViewGroup派生类都具有该属性，自身对齐方式； 属性内容是一样的，但记得不是同一个参数作用对象不同，具体意义看名字可以知道不具体说明了

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

