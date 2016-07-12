# Window.localStorage
> 原文地址：https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage

localStorage属性允许你使用本地的[Storage](https://developer.mozilla.org/en-US/docs/Web/API/Storage).
localStorage跟[sessionStorage]()类似。

localStorage与sessionStorage唯一的区别在于：存储在localStorage中的数据没有过期时间；而存放在sessionStorage的数据将
在浏览器关闭的时候被清空。

###语法
    myStorage = localStorage;
    
###值
一个[Storage](https://developer.mozilla.org/en-US/docs/Web/API/Storage)对象。

###例子
> 以下的代码片段获取了当前域里的[Storage](https://developer.mozilla.org/en-US/docs/Web/API/Storage)对象，
并且使用[Storage.setItem()](https://developer.mozilla.org/en-US/docs/Web/API/Storage/setItem)方法将一个数据加入进去。
    
        localStorage.setItem('myCat', 'Tom');
    
#####注意：请参见[如何使用Web Storage API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API)来查看完整的例子。

