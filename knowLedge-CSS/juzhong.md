# 水平垂直居中的7种方式
- 1 **absolute➕负margin**
```
  <div class="wp">
    <div class="box size"></div>
  </div>
```
**wp 是父元素的类名，box 是子元素的类名，因为有定宽和不定宽的区别，size 用来表示指定宽度，下面是所有效果都要用到的公共代码，主要是设置颜色和宽高。**
*公共代码*
```
.wp{
    width: 300px;
    height: 300px;
    border: 1px solid red;
  }
  .box.size{
    width: 100px;
    height: 100px;
  }
  .box{
    background: green;
    
  }
```
**绝对定位的百分比是相对于父元素的宽高，通过这个特性可以让子元素的居中显示，但绝对定位是基于子元素的左上角，期望的效果是子元素的中心居中显示。
为了修正这个问题，可以借助外边距的负值，负的外边距可以让元素向相反方向定位，通过指定子元素的外边距为子元素宽度一半的负值，就可以让子元素居中了，css 代码如下。**
```
/* 此处引用上面的公共代码 */
/* 此处引用上面的公共代码 */

/* 定位代码 */
.wp {
    position: relative;
}
.box {
    position: absolute;;
    top: 50%;
    left: 50%;
    margin-left: -50px;
    margin-top: -50px;
}
```
**这种方式比较好理解，兼容性也很好，缺点是需要知道子元素的宽高。**
- 2 **absolute + margin auto**
*这种方式也要求居中元素的宽高必须固定，这种方式通过设置各个方向的距离都是 0，此时再讲 margin 设为 auto，就可以在各个方向上居中了*
```
/* 此处引用上面的公共代码 */
/* 此处引用上面的公共代码 */

/* 定位代码 */
.wp {
    position: relative;
}
.box {
    position: absolute;;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    margin: auto;
}
```
- 3.**absolute + calc**
*这种方式也要求居中元素的宽高必须固定，感谢 css3 带来了计算属性，既然 top 的百分比是基于元素的左上角，那么在减去宽度的一半就好了，代码如下*
```	
/* 此处引用上面的公共代码 */
/* 此处引用上面的公共代码 */

/* 定位代码 */
.wp {
    position: relative;
}
.box {
    position: absolute;;
    top: calc(50% - 50px);
    left: calc(50% - 50px);
}
```

**以上是需要居中元素宽高的方法**
**======================================================================**

- 4.**absolute + transform**
*还是绝对定位，但这个方法不需要子元素固定宽高，所以不再需要 size 类了，HTML 代码如下*
```
<div class="wp">
    <div class="box">123123</div>
</div>
```
*修复绝对定位的问题，还可以使用 css3 新增的 transform，transform 的 translate 属性也可以设置百分比，其是相对于自身的宽和高，所以可以讲 translate 设置为 -50%，就可以做到居中了，代码如下：*
```
/* 此处引用上面的公共代码 */
/* 此处引用上**strong text**面的公共代码 */

/* 定位代码 */
.wp {
    position: relative;
}
.box {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
```
- 5**.lineheight**
*利用行内元素居中属性也可以做到水平垂直居中，HTML 代码如下：
```
<div class="wp">
    <div class="box">123123</div>
</div>
```
把 box 设置为行内元素，通过 text-align 就可以做到水平居中，但很多同学可能不知道通过通过 vertical-align 也可以在垂直方向做到居中，代码如下：*
```
/* 此处引用上面的公共代码 */
/* 此处引用上面的公共代码 */

/* 定位代码 */
.wp {
    line-height: 300px;
    text-align: center;
    font-size: 0px;
}
.box {
    font-size: 16px;
    display: inline-block;
    vertical-align: middle;
    line-height: initial;
    text-align: left; /* 修正文字 */
}
```
- 6**css-table**
css 新增的 table 属性，可以让我们把普通元素，变为 table 元素的现实效果，通过这个特性也可以实现水平垂直居中。
```
<div class="wp">
    <div class="box">123123</div>
</div>
```
下面通过 css 属性，可以让 div 显示的和 table 一样：
```
.wp {
    display: table-cell;
    text-align: center;
    vertical-align: middle;
}
.box {
    display: inline-block;
}
```
这种方法和 table 一样的原理，但却没有那么多冗余代码，兼容性也还不错。
- 7 **.flex**
flex 作为现代的布局方案，颠覆了过去的经验，只需几行代码就可以优雅的做到水平垂直居中。
```
<div class="wp">
    <div class="box">123123</div>
</div>

.wp {
    display: flex;
    justify-content: center;
    align-items: center;
}
```
目前在移动端已经完全可以使用 flex 了，PC 端需要看自己业务的兼容性情况。


