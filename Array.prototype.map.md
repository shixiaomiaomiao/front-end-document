# Array.prototype.map
> 原文： https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map


map的语法： arr.map( callback[ , thisArg] )
作用是：将原数组中的每个值都用 callback调用，将调用以后返回的结果值作为新数组。
callback接受三个参数：

- currentValue: 在数组中正在被处理的当前值
- index: 在数组中被处理的当前值的索引值
- array: 自从被调用起时的array.


thisArg: 可选值。但在执行callback函数时 被用作this. 默认值为Window对象。

## 描述
map方法将数组中的每个元素都调用一次callback函数，以至于从返回的结果值中构建了一个新的数组。
callback函数只会呗数组中已经分配值的索引值所调用，包括undefined；它将不会被那些数组中缺失的元素调用。
即，索引值从未被设置过，或者已经被删除的，或者从未被赋值过。

callback函数被调用时含有三个参数：元素的值，元素的索引值，和数组对象。
如果一个thisArg参数被传入map函数中，它将会在callback被调用时传给callback函数，作为callback函数的
this值来使用。否则，值undefined就会被传入作为this值。此时，this的值最终由callback函数根据
[一个函数中的this值的取值规则](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)决定。

map函数的调用并不改变数组。（尽管如果调用callback,也许会改变数组）

- 被map函数处理的元素的范围狮子啊callback首次调用之前就已经设定好了的。
- 在map函数已经开始执行以后，被添加进数组的元素将不再被callback访问。
- 如果数组中存在的元素被改变了，或者被删除了，他们传入callback函数中的值将会是map访问他们时的值；
当然元素被删除了，将不再被访问。

##例子

#### 将一个数字数组map成一个平方根数组

>以下的代码将选取了一个数字数组，并且创建了一个包含第一个数组中的平方根的新数组。
  
  var numbers  = [1,4,9];
  var roots = numbers.map(Math.sqrt);
  //roots=> [1,2,3] ; number => [1,4,9]




