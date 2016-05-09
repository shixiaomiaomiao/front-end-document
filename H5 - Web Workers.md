#使用Web Workers
> 英文原文：https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers

<code>Web Workers为web内容在背景线程上运行脚本提供了一种简单的方式。worker线程可以在不干扰用户接口的情况下执行任务。此外，他们可以利用
[XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Mozilla/Tech/XPCOM/Reference/Interface/nsIXMLHttpRequest)(尽管reponseXML和channel的属性值通常为null)。一旦创建，通过将信息传递给event handler，一个worker可以向创建它的Javascript代码发送信息；反之亦然。这篇文章详细讲述了使用web workers接口的细节信息。</code>

##Web Workers API
一个worker是由构造函数（eg. Worker()）创建的一个对象，他会运行一个命名好的Javascript文件，该文件中的代码将会运行在worker线程上。workers运行在另一个全局上下文（global contex）中，与运行在当前的[window](https://developer.mozilla.org/en-US/docs/Web/API/Window)不同。因此，在一个worker中想要使用[window](https://developer.mozilla.org/en-US/docs/Web/API/Window)来获取当前的全局作用域（正确的是用[self](https://developer.mozilla.org/en-US/docs/Web/API/Window/self)）将会返回错误。

在专用的workers中，worker的上下文是由[DedicateWorkerGlobalScope](https://developer.mozilla.org/en-US/docs/Web/API/DedicatedWorkerGlobalScope)对象表示的。标准workers是利用一个简单的脚本实现的，共享的wokers是使用[ShareWorkerGlobalScope](https://developer.mozilla.org/en-US/docs/Web/API/SharedWorkerGlobalScope).一个专用的worker只能从首次启用它的脚本中获得，然而共享的workers能够从多种脚本中获得。

<table><tr><td bgcolor=#FFF4CC>注意： 查看[The Web Workers API landing page](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API) 获取关于workers的参考资料和其他知道</td></tr></table>


你可以在worker线程中运行人格你喜欢的代码
