#Storage
> 原文地址：https://developer.mozilla.org/en-US/docs/Web/API/Storage

Web Storage API的Storage接口对于特殊的域来说可以获取session storage或者local storage,
允许你增加、修改和删除数据。

如果你想对一个域操作session storage，你可以使用[Window.sessionStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/sessionStorage)
方法；如果你想对一个域进行local storage操作，你可以使用[Window.localStorage](https://github.com/shixiaomiaomiao/front-end-document/blob/master/h5-localStorage.md).

###属性
- Storage.length (只读)

>  返回值为存储在Storage对象中的数据的个数的整数。

###方法
- Storage.key()
>传入一个数字n，该方法返回storage中的第n个key值的名字。

- Storage.getItem()
> 传入一个key值，返回对应的value值。

- Storage.setItem()
> 传入一个key值和相应的value值，将会在storage中新增该key值，
或者是跟新已经存在的key值对应的value值。

- Storage.removeItem()
> 传入一个key值，将会使得storage中的那个key值移除掉。

- Storage.clear()
> 当该方法被调用时，storage中的所有值都将被清空。

### 例子
在这里我们通过调用localStorage获得到了一个Storage对象。
我们首先使用!localStorage.getItem('bgcolor')来测试local storage中是否包含data对象。 -如果包含了，我们可以运行setStyles函数来使用localStorage.getItem()方法获取data的
各个值，并且用这些值来跟新页面的样式。
- 如果不包含，我们可以使用另一个函数:populateStorage(),这个函数是先用localStorage.setItem()方法
来设置item值，然后运行setStyles()函数。

        if(!localStorage.getItem('bgcolor')) {
          populateStorage();
        } else {
          setStyles();
        }
    
        function populateStorage() {
          localStorage.setItem('bgcolor', document.getElementById('bgcolor').value);
          localStorage.setItem('font', document.getElementById('font').value);
          localStorage.setItem('image', document.getElementById('image').value);
          
          setStyles();
        }
    
        function setStyles() {
          var currentColor = localStorage.getItem('bgcolor');
          var currentFont = localStorage.getItem('font');
          var currentImage = localStorage.getItem('image');
          
          document.getElementById('bgcolor').value = currentColor;
          document.getElementById('font').value = currentFont;
          document.getElementById('image').value = currentImage;
          
          htmlElem.style.backgroundColor = '#' + currentColor;
          pElem.style.fontFamily = currentFont;
          imgElem.setAttribute('src', currentImage);
        }
    
##### 注意：想看以上代码完整的工作例子，请见[Web Storage Demo](https://github.com/mdn/web-storage-demo);



