# View

## 系统属性

首先了解下Android系统属性和样式如何查看。很多问题不需要一味的Google搜索，只要你查看系统属性，稍加了解都可以迎刃而解。Android系统资源和属性源码在SDk`platforms/android-23/data`目录下，通过Android Studio可以很方便的在`External Libraries` 对应版本的`res`目录下查看，跟应用源码的资源目录一样，同样有`values` `deawable` `layout` 等目录，我们要查看都属性都在`values`下。

![api 23 res](http://upload-images.jianshu.io/upload_images/1845254-2c219bbefe8d975b.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

`attrs.xml`系统属性定义文件\(`android:id` `android:backgound` 都在这里定义\)，`styles.xml` 默认样式定义，`themes.xml` 默认主题定义。样式和主题的区别在以后自定义控件再讲，这里要注意的是不同版本会读取不同的样式和主题文件。4.0以后新增HOLO `themes_holo.xml`，5.0又新增Meterial Design `themes_meterial.xml`，4.0以下读取themes主题，5.0以下读取themes\_holo主题，5.0以上读取themes\_meterial主题，不同主题对应着不同样式，不同版本样式都有很大区别。

View作为Android视图界面的基类，所有能看见的都是View及其子类。虽然实际开发多数使用的是View的子类很少直接使用View，但是View的属性可以更好的了解View的共同特性。了解它的属性是很有必要的，需要注意的是`layout_width` `layout_height` 和 `margin`系列由ViewGroup确定并不是View属性，enum和flag的区别在于单选和多选。

View的属性特别多不可能全部了解记忆，只需要记住一些常用的属性及其对应的方法。那为啥要了解呢，开头说了只要对属性有叫深入的了解都可以迎刃而解。View的属性内容多得有点恐怖。

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
      <td style="text-align:left">id</td>
      <td style="text-align:left">reference</td>
      <td style="text-align:left">&#x5F15;&#x7528;ID</td>
    </tr>
    <tr>
      <td style="text-align:left">tag</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">tag&#x6807;&#x7B7E;</td>
    </tr>
    <tr>
      <td style="text-align:left">scrollX</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">&#x6C34;&#x5E73;&#x6ED1;&#x52A8;&#x8DDD;&#x79BB;</td>
    </tr>
    <tr>
      <td style="text-align:left">scrollY</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">&#x5782;&#x76F4;&#x6ED1;&#x52A8;&#x8DDD;&#x79BB;</td>
    </tr>
    <tr>
      <td style="text-align:left">background</td>
      <td style="text-align:left">reference/color</td>
      <td style="text-align:left">&#x80CC;&#x666F;&#x56FE;&#x7247;/&#x80CC;&#x666F;&#x8272;</td>
    </tr>
    <tr>
      <td style="text-align:left">padding</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">&#x5185;&#x90E8;&#x4E0A;&#x4E0B;&#x5DE6;&#x53F3;&#x586B;&#x5145;&#x8DDD;&#x79BB;</td>
    </tr>
    <tr>
      <td style="text-align:left">paddingLeft</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">&#x5DE6;&#x8FB9;&#x586B;&#x5145;&#x8DDD;&#x79BB;</td>
    </tr>
    <tr>
      <td style="text-align:left">paddingRight</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">&#x53F3;&#x8FB9;&#x586B;&#x5145;&#x8DDD;&#x79BB;</td>
    </tr>
    <tr>
      <td style="text-align:left">paddingTop</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">&#x4E0A;&#x8FB9;&#x586B;&#x5145;&#x8DDD;&#x79BB;</td>
    </tr>
    <tr>
      <td style="text-align:left">paddingBottom</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">&#x4E0B;&#x8FB9;&#x586B;&#x5145;&#x8DDD;&#x79BB;</td>
    </tr>
    <tr>
      <td style="text-align:left">focusable</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x53EF;&#x83B7;&#x53D6;&#x7126;&#x70B9;</td>
    </tr>
    <tr>
      <td style="text-align:left">focusableInTouchMode</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x89E6;&#x6478;&#x4E8B;&#x4EF6;&#x53EF;&#x83B7;&#x53D6;&#x7126;&#x70B9;</td>
    </tr>
    <tr>
      <td style="text-align:left">visibility</td>
      <td style="text-align:left">
        <p>enum</p>
        <p>(visible/invisible/gone)</p>
      </td>
      <td style="text-align:left">&#x662F;&#x5426;&#x663E;&#x793A;View</td>
    </tr>
    <tr>
      <td style="text-align:left">fitsSystemWindows</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x9002;&#x914D;&#x7CFB;&#x7EDF;&#x7A97;&#x53E3;</td>
    </tr>
    <tr>
      <td style="text-align:left">scrollbars</td>
      <td style="text-align:left">
        <p>flag</p>
        <p>(none/horizontal/vertical)</p>
      </td>
      <td style="text-align:left">&#x662F;&#x5426;&#x663E;&#x793A;&#x6EDA;&#x52A8;&#x6761;</td>
    </tr>
    <tr>
      <td style="text-align:left">scrollbarStyle</td>
      <td style="text-align:left">emum</td>
      <td style="text-align:left">&#x6EDA;&#x52A8;&#x6761;&#x6837;&#x5F0F;</td>
    </tr>
    <tr>
      <td style="text-align:left">isScrollContainer</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x662F;&#x5426;&#x4F5C;&#x4E3A;&#x53EF;&#x6EDA;&#x52A8;&#x5BB9;&#x5668;&#x4F7F;&#x7528;</td>
    </tr>
    <tr>
      <td style="text-align:left">fadeScrollbars</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x81EA;&#x52A8;&#x9690;&#x85CF;</td>
    </tr>
    <tr>
      <td style="text-align:left">scrollbarFadeDuration</td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">&#x81EA;&#x52A8;&#x9690;&#x85CF;&#x65F6;&#x95F4;</td>
    </tr>
    <tr>
      <td style="text-align:left">scrollbarDefaultDelayBeforeFade</td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">&#x6DE1;&#x5316;&#x6548;&#x679C;&#x5F00;&#x59CB;&#x65F6;&#x95F4;</td>
    </tr>
    <tr>
      <td style="text-align:left">scrollbarSize</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">&#x6EDA;&#x52A8;&#x6761;&#x5BBD;&#x5EA6;</td>
    </tr>
    <tr>
      <td style="text-align:left">scrollbarThumbHorizontal</td>
      <td style="text-align:left">reference</td>
      <td style="text-align:left">&#x6C34;&#x5E73;&#x6EDA;&#x52A8;&#x6761;&#x989C;&#x8272;</td>
    </tr>
    <tr>
      <td style="text-align:left">scrollbarThumbVertical</td>
      <td style="text-align:left">reference</td>
      <td style="text-align:left">&#x5782;&#x76F4;&#x6EDA;&#x52A8;&#x6761;&#x989C;&#x8272;</td>
    </tr>
    <tr>
      <td style="text-align:left">scrollbarTrackHorizontal</td>
      <td style="text-align:left">reference</td>
      <td style="text-align:left">&#x6C34;&#x5E73;&#x6EDA;&#x52A8;&#x6761;&#x80CC;&#x666F;</td>
    </tr>
    <tr>
      <td style="text-align:left">scrollbarTrackVertical</td>
      <td style="text-align:left">reference</td>
      <td style="text-align:left">&#x5782;&#x76F4;&#x6EDA;&#x52A8;&#x6761;&#x80CC;&#x666F;</td>
    </tr>
    <tr>
      <td style="text-align:left">scrollbarAlwaysDrawHorizontalTrack</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x59CB;&#x7EC8;&#x663E;&#x793A;&#x6C34;&#x5E73;&#x6EDA;&#x52A8;&#x6761;</td>
    </tr>
    <tr>
      <td style="text-align:left">scrollbarAlwaysDrawVerticalTrack</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x59CB;&#x7EC8;&#x663E;&#x793A;&#x5782;&#x76F4;&#x6EDA;&#x52A8;&#x6761;</td>
    </tr>
    <tr>
      <td style="text-align:left">fadingEdge</td>
      <td style="text-align:left">
        <p>flag</p>
        <p>(none/horizontal/vertical)</p>
      </td>
      <td style="text-align:left">&#x663E;&#x793A;&#x8FB9;&#x754C;&#x9634;&#x5F71;</td>
    </tr>
    <tr>
      <td style="text-align:left">requiresFadingEdge</td>
      <td style="text-align:left">
        <p>flag</p>
        <p>(none/horizontal/vertical)</p>
      </td>
      <td style="text-align:left">&#x6EDA;&#x52A8;&#x65F6;&#x8FB9;&#x7F18;&#x662F;&#x5426;&#x892A;&#x8272;</td>
    </tr>
    <tr>
      <td style="text-align:left">fadingEdgeLength</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">&#x8FB9;&#x754C;&#x9634;&#x5F71;&#x957F;&#x5EA6;</td>
    </tr>
    <tr>
      <td style="text-align:left">nextFocusLeft</td>
      <td style="text-align:left">reference</td>
      <td style="text-align:left">&#x5DE6;&#x8FB9;&#x4E0B;&#x4E2A;&#x7126;&#x70B9;&#x63A7;&#x4EF6;&#xFF0C;&#x65B9;&#x5411;&#x5207;&#x6362;</td>
    </tr>
    <tr>
      <td style="text-align:left">nextFocusRight</td>
      <td style="text-align:left">reference</td>
      <td style="text-align:left">&#x53F3;&#x8FB9;&#x4E0B;&#x4E2A;&#x7126;&#x70B9;&#x63A7;&#x4EF6;</td>
    </tr>
    <tr>
      <td style="text-align:left">nextFocusUp</td>
      <td style="text-align:left">reference</td>
      <td style="text-align:left">&#x4E0A;&#x8FB9;&#x4E0B;&#x4E2A;&#x7126;&#x70B9;&#x63A7;&#x4EF6;</td>
    </tr>
    <tr>
      <td style="text-align:left">nextFocusDown</td>
      <td style="text-align:left">reference</td>
      <td style="text-align:left">&#x4E0B;&#x8FB9;&#x4E0B;&#x4E2A;&#x7126;&#x70B9;&#x63A7;&#x4EF6;</td>
    </tr>
    <tr>
      <td style="text-align:left">nextFocusForward</td>
      <td style="text-align:left">reference</td>
      <td style="text-align:left">&#x4E0B;&#x4E2A;&#x7126;&#x70B9;&#x63A7;&#x4EF6;&#xFF0C;tab&#x5207;&#x6362;</td>
    </tr>
    <tr>
      <td style="text-align:left">clickable</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x5141;&#x8BB8;&#x70B9;&#x51FB;</td>
    </tr>
    <tr>
      <td style="text-align:left">longClickable</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x5141;&#x8BB8;&#x957F;&#x6309;</td>
    </tr>
    <tr>
      <td style="text-align:left">contextClickable</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">saveEnabled</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x914D;&#x7F6E;&#x6539;&#x53D8;&#x7B49;&#x60C5;&#x51B5;&#xFF0C;&#x4FDD;&#x5B58;View&#x7684;&#x6570;&#x636E;</td>
    </tr>
    <tr>
      <td style="text-align:left">filterTouchesWhenObscured</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x6240;&#x5728;&#x7A97;&#x53E3;&#x88AB;&#x5176;&#x5B83;&#x53EF;&#x89C1;&#x7A97;&#x53E3;&#x906E;&#x4F4F;&#x65F6;,&#x662F;&#x5426;&#x8FC7;&#x6EE4;&#x89E6;&#x6478;&#x4E8B;&#x4EF6;</td>
    </tr>
    <tr>
      <td style="text-align:left">drawingCacheQuality</td>
      <td style="text-align:left">enum(auto/low/high)</td>
      <td style="text-align:left">&#x534A;&#x900F;&#x660E;&#x8D28;&#x91CF;</td>
    </tr>
    <tr>
      <td style="text-align:left">keepScreenOn</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x5F3A;&#x5236;&#x624B;&#x673A;&#x5C4F;&#x5E55;&#x4E00;&#x76F4;&#x6253;&#x5F00;</td>
    </tr>
    <tr>
      <td style="text-align:left">duplicateParentState</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x4ECE;&#x7236;&#x5BB9;&#x5668;&#x4E2D;&#x83B7;&#x53D6;&#x7ED8;&#x56FE;&#x72B6;&#x6001;</td>
    </tr>
    <tr>
      <td style="text-align:left">minHeight</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">&#x6700;&#x5C0F;&#x9AD8;&#x5EA6;</td>
    </tr>
    <tr>
      <td style="text-align:left">minWidth</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">&#x6700;&#x5C0F;&#x5BBD;&#x5EA6;</td>
    </tr>
    <tr>
      <td style="text-align:left">soundEffectsEnabled</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x70B9;&#x51FB;&#x65F6;&#x662F;&#x5426;&#x4F7F;&#x7528;&#x97F3;&#x6548;</td>
    </tr>
    <tr>
      <td style="text-align:left">hapticFeedbackEnabled</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x89E6;&#x611F;&#x53CD;&#x9988;(&#x632F;&#x52A8;)</td>
    </tr>
    <tr>
      <td style="text-align:left">contentDescription</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x7EC4;&#x4EF6;&#x7684;&#x5185;&#x5BB9;&#x63CF;&#x8FF0;&#x4FE1;&#x606F;&#xFF0C;&#x4E34;&#x65F6;&#x653E;&#x4E00;&#x70B9;&#x5B57;&#x7B26;&#x4E32;&#x6570;&#x636E;</td>
    </tr>
    <tr>
      <td style="text-align:left">accessibilityTraversalBefore</td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">&#x53EF;&#x8BBF;&#x95EE;&#x6027;&#x904D;&#x5386;&#xFF0C;&#x88AB;&#x8BBF;&#x95EE;&#x4E4B;&#x524D;&#x5148;&#x8BBF;&#x95EE;&#x8BBE;&#x7F6E;&#x7684;&#x7EC4;&#x4EF6;</td>
    </tr>
    <tr>
      <td style="text-align:left">accessibilityTraversalAfter</td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">&#x53EF;&#x8BBF;&#x95EE;&#x6027;&#x904D;&#x5386;&#xFF0C;&#x88AB;&#x8BBF;&#x95EE;&#x4E4B;&#x540E;&#x8BBF;&#x95EE;&#x8BBE;&#x7F6E;&#x7684;&#x7EC4;&#x4EF6;</td>
    </tr>
    <tr>
      <td style="text-align:left">onClick</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x5355;&#x51FB;&#x4E8B;&#x4EF6;&#x7ED1;&#x5B9A;&#x76D1;&#x542C;&#x5668;</td>
    </tr>
    <tr>
      <td style="text-align:left">overScrollMode</td>
      <td style="text-align:left">
        <p>enum</p>
        <p>(always/ifContentScrolls/</p>
        <p>never)</p>
      </td>
      <td style="text-align:left">&#x62C9;&#x5230;&#x5C3D;&#x5934;&#x7684;&#x884C;&#x4E3A; 2.3&#x4E4B;&#x524D;</td>
    </tr>
    <tr>
      <td style="text-align:left">alpha</td>
      <td style="text-align:left">float</td>
      <td style="text-align:left">&#x900F;&#x660E;&#x5EA6;&#x5C5E;&#x6027;, 0 (&#x5B8C;&#x5168;&#x900F;&#x660E;)
        ~ 1 (&#x5B8C;&#x5168;&#x4E0D;&#x900F;&#x660E;)</td>
    </tr>
    <tr>
      <td style="text-align:left">elevation</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">z &#x8F74;&#x6DF1;&#x5EA6;</td>
    </tr>
    <tr>
      <td style="text-align:left">translationX</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">X&#x65B9;&#x5411;&#x4E0A;&#x7684;&#x4F4D;&#x79FB;</td>
    </tr>
    <tr>
      <td style="text-align:left">translationY</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">Y&#x65B9;&#x5411;&#x4E0A;&#x7684;&#x4F4D;&#x79FB;</td>
    </tr>
    <tr>
      <td style="text-align:left">translationZ</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">Z&#x65B9;&#x5411;&#x4E0A;&#x7684;&#x4F4D;&#x79FB;</td>
    </tr>
    <tr>
      <td style="text-align:left">transformPivotX</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">&#x65CB;&#x8F6C;&#x65F6;&#x65CB;&#x8F6C;&#x4E2D;&#x5FC3;&#x7684;X&#x5750;&#x6807;</td>
    </tr>
    <tr>
      <td style="text-align:left">transformPivotY</td>
      <td style="text-align:left">dimension</td>
      <td style="text-align:left">&#x65CB;&#x8F6C;&#x65F6;&#x65CB;&#x8F6C;&#x4E2D;&#x5FC3;&#x7684;Y&#x5750;&#x6807;</td>
    </tr>
    <tr>
      <td style="text-align:left">rotation</td>
      <td style="text-align:left">float</td>
      <td style="text-align:left">&#x65CB;&#x8F6C;&#x7684;&#x89D2;&#x5EA6;</td>
    </tr>
    <tr>
      <td style="text-align:left">rotationX</td>
      <td style="text-align:left">float</td>
      <td style="text-align:left">&#x7ED5;X&#x8F74;&#x65CB;&#x8F6C;&#x7684;&#x89D2;&#x5EA6;</td>
    </tr>
    <tr>
      <td style="text-align:left">rotationY</td>
      <td style="text-align:left">float</td>
      <td style="text-align:left">&#x7ED5;Y&#x8F74;&#x65CB;&#x8F6C;&#x7684;&#x89D2;&#x5EA6;</td>
    </tr>
    <tr>
      <td style="text-align:left">scaleX</td>
      <td style="text-align:left">float</td>
      <td style="text-align:left">&#x6C34;&#x5E73;&#x65B9;&#x5411;&#x7684;&#x7F29;&#x653E;&#x6BD4;</td>
    </tr>
    <tr>
      <td style="text-align:left">scaleY</td>
      <td style="text-align:left">float</td>
      <td style="text-align:left">&#x6C34;&#x5E73;&#x65B9;&#x5411;&#x7684;&#x7F29;&#x653E;&#x6BD4;</td>
    </tr>
    <tr>
      <td style="text-align:left">verticalScrollbarPosition</td>
      <td style="text-align:left">
        <p>enum</p>
        <p>(defaultPosition/left/right)</p>
      </td>
      <td style="text-align:left">&#x6EDA;&#x52A8;&#x6761;&#x7684;&#x4F4D;&#x7F6E;</td>
    </tr>
    <tr>
      <td style="text-align:left">layerType</td>
      <td style="text-align:left">
        <p>enum</p>
        <p>(none/software/hardware)</p>
      </td>
      <td style="text-align:left">&#x6307;&#x5B9A;&#x5C42;&#x7684;&#x7C7B;&#x578B;</td>
    </tr>
    <tr>
      <td style="text-align:left">layoutDirection</td>
      <td style="text-align:left">
        <p>enum</p>
        <p>(ltr/rtl/inherit/locale)</p>
      </td>
      <td style="text-align:left">&#x5E03;&#x5C40;&#x56FE;&#x7EB8;&#x7684;&#x65B9;&#x5411;</td>
    </tr>
    <tr>
      <td style="text-align:left">textDirection</td>
      <td style="text-align:left">integer - enum</td>
      <td style="text-align:left">&#x6587;&#x672C;&#x7684;&#x663E;&#x793A;&#x65B9;&#x5411;</td>
    </tr>
    <tr>
      <td style="text-align:left">textAlignment</td>
      <td style="text-align:left">integer - enum</td>
      <td style="text-align:left">&#x6587;&#x672C;&#x7684;&#x663E;&#x793A;&#x5BF9;&#x9F50;&#x65B9;&#x5F0F;</td>
    </tr>
    <tr>
      <td style="text-align:left">importantForAccessibility</td>
      <td style="text-align:left">
        <p>integer - enum</p>
        <p>(auto/yes/no/</p>
        <p>noHideDescendants)</p>
      </td>
      <td style="text-align:left">&#x65E0;&#x969C;&#x788D;&#x670D;&#x52A1;&#x7684;&#x91CD;&#x8981;&#x6027;</td>
    </tr>
    <tr>
      <td style="text-align:left">accessibilityLiveRegion</td>
      <td style="text-align:left">
        <p>integer - enum</p>
        <p>(none/polite/assertive)</p>
      </td>
      <td style="text-align:left">&#x65E0;&#x969C;&#x788D;&#x670D;&#x52A1; &#x7EC4;&#x4EF6;&#x6539;&#x53D8;&#x65F6;&#x662F;&#x5426;&#x901A;&#x77E5;&#x7528;&#x6237;&#xFF0C;&#x4E0D;&#x901A;&#x77E5;&#xFF0C;&#x901A;&#x77E5;&#x3001;&#x6253;&#x65AD;&#x8BED;&#x97F3;.</td>
    </tr>
    <tr>
      <td style="text-align:left">labelFor</td>
      <td style="text-align:left">reference</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">theme</td>
      <td style="text-align:left">reference</td>
      <td style="text-align:left">&#x4E3B;&#x9898;</td>
    </tr>
    <tr>
      <td style="text-align:left">transitionName</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">nestedScrollingEnabled</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x5141;&#x8BB8;&#x5D4C;&#x5957;&#x6ED1;&#x52A8;</td>
    </tr>
    <tr>
      <td style="text-align:left">stateListAnimator</td>
      <td style="text-align:left">reference</td>
      <td style="text-align:left">5.0&#x70B9;&#x51FB;&#x9634;&#x5F71;&#x6548;&#x679C;</td>
    </tr>
    <tr>
      <td style="text-align:left">backgroundTint</td>
      <td style="text-align:left">color</td>
      <td style="text-align:left">&#x80CC;&#x666F;&#x8272;</td>
    </tr>
    <tr>
      <td style="text-align:left">backgroundTintMode</td>
      <td style="text-align:left">enum</td>
      <td style="text-align:left">&#x80CC;&#x666F;&#x8272;&#x7684;&#x6DF7;&#x5408;&#x6A21;&#x5F0F;</td>
    </tr>
    <tr>
      <td style="text-align:left">outlineProvider</td>
      <td style="text-align:left">enum</td>
      <td style="text-align:left">&#x6307;&#x5B9A;&#x9634;&#x5F71;(&#x8F6E;&#x5ED3;)&#x7684;&#x5224;&#x5B9A;&#x65B9;&#x5F0F;</td>
    </tr>
    <tr>
      <td style="text-align:left">foreground</td>
      <td style="text-align:left">reference/color</td>
      <td style="text-align:left">&#x524D;&#x666F;&#x56FE;&#x7247;/&#x524D;&#x666F;&#x8272;</td>
    </tr>
    <tr>
      <td style="text-align:left">foregroundGravity</td>
      <td style="text-align:left">enum</td>
      <td style="text-align:left">&#x524D;&#x666F;&#x56FE;&#x7247;&#x4F4D;&#x7F6E;, &#x9ED8;&#x8BA4; left
        &#x548C; top</td>
    </tr>
    <tr>
      <td style="text-align:left">foregroundInsidePadding</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">foregroundTint</td>
      <td style="text-align:left">color</td>
      <td style="text-align:left">&#x524D;&#x666F;&#x989C;&#x8272;</td>
    </tr>
    <tr>
      <td style="text-align:left">foregroundTintMode</td>
      <td style="text-align:left">enum</td>
      <td style="text-align:left">&#x524D;&#x666F;&#x56FE;&#x7247;&#x7684;&#x6DF7;&#x5408;&#x6A21;&#x5F0F;,
        &#x9ED8;&#x8BA4; SRC_IN</td>
    </tr>
    <tr>
      <td style="text-align:left">scrollIndicators</td>
      <td style="text-align:left">flag</td>
      <td style="text-align:left">&#x6ED1;&#x52A8;&#x6307;&#x793A;&#x5668;</td>
    </tr>
  </tbody>
</table>附： [android之View属性](http://www.jianshu.com/p/875a9adb4952) [Android View 组件](http://www.bozhiyue.com/anroid/wenzhang/2016/0516/103333.html) \[Android layout属性详细说明\] \([http://www.cnblogs.com/skywang12345/archive/2013/06/15/AndroidAttr.html](http://www.cnblogs.com/skywang12345/archive/2013/06/15/AndroidAttr.html)\) [\[教程\] 【也说Android开发】第三讲 Layout文件属性讲解](http://blog.chinaunix.net/uid-29134536-id-3982048.html)

## 常用方法

## 事件分发

