# front-end-document
records knowledge of front-end that I do know or know well 

> 今天接手打点广告业务，看代码时发现了document.compatMode方法，故此处对其用法做个记录

1.document.compatMode返回的是当前浏览器解析html文件所用的模式；这个方法主要用在浏览器兼容方面。

众所周知，IE的ie6,ie7,ie8在混杂模式（quriks mode）下的[盒模型与W3C的盒模型有所不同](http://www.cnblogs.com/shixiaomiao/p/5413438.html)。

2.document.compatMode的返回值有两种： 

1) BackCompat :代表的是混杂模式（Quriks Mode）

2) CSS<sub>1</sub>Compat:代表的是标准模式（Standards Mode）

> 建议在html的开头写清声明Doctype，使得解析模式在标准模式下；

> html5的声明方式<!Doctype html>，在ie11和Chrome49下的compatMode都是CSS<sub>1</sub>Compat。

#不同compatMode模式下的浏览器尺寸获取

- 当document.compatMode为BackCompat时，浏览器客户区宽度为： document.body.clientWidth;

- 当document.compatMode为CSS<sub>1</sub>Compat时，浏览器客户区宽度为： document.documentElement.clientWidth.
> 浏览器客户区高度clientHeight、可视区宽度clientWidth、滚动条高度scrollHeight、滚动条的scrollLeft、滚动条的scrollTop都是类似的


