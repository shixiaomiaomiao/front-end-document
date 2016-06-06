## repaint && reflow 
> 翻译自：[Efficient Javascript](https://dev.opera.com/articles/efficient-javascript/#reflow)

>[reflow&repaints:css perfance making your Javascipt slow](http://www.stubbornella.org/content/2009/03/27/reflows-repaints-css-performance-making-your-javascript-slow/comment-page-1/)

repaint,或者说是redraw(重绘)，是在一些原先不可见的元素变得可见，并且不改变document的布局时发生的，反之亦然。
当在一个元素上加一个轮廓、改变背景颜色或者改变是否可见（visibility）样式时，将会发生重绘。
重绘在性能方面的开销是昂贵的，因为它需要引擎去搜索所有的元素来决定哪些是可见的,哪些应该被展示。

一次reflow（回流）是一个更加重大的改变。每当DOM树被计算，一个影响布局的样式改变了，或者当浏览器窗口大小改变了。
引擎必须回流相关元素来弄清楚哪些部分应该显示出来。发生变化元素的子元素，鉴于他们父元素的新布局，也会被回流。
在DOM结构中出现在变化元素之后的元素也会发生回流，一遍计算他们新的布局，因为他们可能被初始化的回流移动了位置。
为了适应他们子元素的尺寸变化，祖先元素也可能发生回流。最终，所有的元素都被重绘。

reflow(回流)在性能的开销是非常昂贵的。尤其是当设备的处理能力比较慢的时候，比如手机，它是拖慢DOM脚本的主要因素之一。
在许多情况下，他们等同于再次布局整个页面。


