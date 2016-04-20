> 今天boss通知我以后接手广告业务的展示和打点，项目中有个document.compatMode方法，故在此处对其方法在这里进行记录。

1.document.compatMode返回的是当前浏览器解析html文件所用的模式；这个方法主要用在浏览器兼容方面。

众所周知，IE的ie6,ie7,ie8在混杂模式（quriks mode）下的[盒模型与W3C的盒模型有所不同](http://www.cnblogs.com/shixiaomiao/p/5413438.html)。

2.document.compatMode的返回值有两种： 

1) BackCompat :代表的是混杂模式（Quriks Mode）

2) CSS<sub>1</sub>Compat:代表的是标准模式（Standards Mode）

-  建议在html的开头写清声明Doctype，使得解析模式在标准模式下；

- html5的声明方式<!Doctype html>，在ie11和Chrome49下的compatMode都是CSS<sub>1</sub>Compat。

#不同compatMode模式下的浏览器尺寸获取

- 当document.compatMode为BackCompat时，浏览器客户区宽度为： document.body.clientWidth;

- 当document.compatMode为CSS<sub>1</sub>Compat时，浏览器客户区宽度为： document.documentElement.clientWidth.

 >浏览器客户区高度clientHeight、可视区宽度clientWidth、滚动条高度scrollHeight、滚动条的scrollLeft、滚动条的scrollTop都是类似的

    if (document.compatMode == \"BackCompat\") {
      	cWidth = document.body.clientWidth;
        cHeight = document.body.clientHeight;
        sWidth = document.body.scrollWidth;
        sHeight = document.body.scrollHeight;
        sLeft = document.body.scrollLeft;
        sTop = document.body.scrollTop;
      }
      else { 
        //document.compatMode == \"CSS1Compat\"
        cWidth = document.documentElement.clientWidth;
        cHeight = document.documentElement.clientHeight;
        sWidth = document.documentElement.scrollWidth;
        sHeight = document.documentElement.scrollHeight;
        sLeft = document.documentElement.scrollLeft == 0 ? document.body.scrollLeft : document.documentElement.scrollLeft;
        sTop = document.documentElement.scrollTop == 0 ? document.body.scrollTop : document.documentElement.scrollTop;
      }
