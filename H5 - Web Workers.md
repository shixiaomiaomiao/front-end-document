#使用Web Workers
> 英文原文：https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers

<code>Web Workers为web内容在背景线程上运行脚本提供了一种简单的方式。worker线程可以在不干扰用户接口的情况下执行任务。此外，他们可以利用
[XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Mozilla/Tech/XPCOM/Reference/Interface/nsIXMLHttpRequest)(尽管reponseXML和channel的属性值一种为null)。一旦创建，一个worker
