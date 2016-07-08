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
  
  
### 常规性地使用map函数

>以下的例子显示了怎么使用map函数将一个字符串转变成一个字节数组，这些子节代表了各个字符的ASCII
编码值。

    var map = Array.prototype.map;
    var a = map.call('Hello World', function(x){ return x.charCodeAt(0);});
    // a now equals [72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100]
  
### 使用map函数 querySelectorAll

>以下的例子显示了怎么将一个由querySelectorAll选择出来的对象集合进行循环操作。
在这个例子中，我们在屏幕上得到所有已勾选的选项值和打印在console中的选项。

    var elems = document.querySelectorAll('select options:checked');
    var values = Array.prototye.map.call(elems, function(obj) {
      return obj.value;
    });
  
### 使用map函数来反转一个字符串

    var str = '12345';
    Array.prototype.map.call(str, function(x) {
      return x;
    }).reverse().join('');
    //输出：'54321'
    //额外的收获是：可以使用'==='来检测原始的字符串 是否是一个回文 
  
###map的妙用
> [参考的blog](http://www.wirfs-brock.com/allen/posts/166)

>通常使用callback都只有一个参数（这个元素被反复使用）。特定的函数也是通常只有一个参数，
即使他们带有额外的可选参数。这些习惯也许会导致令人疑惑的行为。

    //假设
    ['1','2','3'].map(parseInt);
    //也许有人会预期结果为［1，2，3］
    //但实际结果是：［1, NaN, NaN］
    
    //parseInt经常被传入一个参数来使用，但其他它有两个参数。
    //第一个参数是一个表达式，第二个是基数。
    //对于回调函数callback来说，Array.prototype.map传入3个参数：元素，索引值，数组
    //第三个参数将被parseInt忽略，但第二个参数不会被忽略。
    //因此也许有些疑惑，查看之前的blog获取更多的细节。
    
    function returnInt(element) {
      return parseInt(element, 10);
    }
    ['1', '2', '3'].map(returnInt); //[1,2,3]
    //实际的结果就是数字数组（正如预期的）
    
    //一个更加简单的方法获取以上结果，避免“获取错误”
    ['1', '2', '3'].map(Number); //[1, 2, 3]
  
### Polyfill
> map函数是在第5版的时候被加进ECMA-262标准的，所以它不是在所有的标准中都有。
你可以在你的脚本中的开始部分插入以下的代码，从而在不支持map函数的环境中实现map函数。
这个算法其实就是第5版的ECMA-262标准中实现的算法，假设Object，TypeError和Array有它们的
起始值，并且callback.call等价于起始值的Function.prototype.call方法。

    //ECMA-262的生产步骤，第5版，15.4.4.19
    //参考：http://es5.github.io/#x15.4.4.19
    if(!Array.prototype.map) {
      Array.prototype.map = function(callback,thisArg) ｛
        
      var T, A, K;
      if (this == null) {
        throw new TypeError(' this is null or not defined');
      }
      }
      
      //第一步:让O(大欧)作为调用Object函数的结果值，将this作为参数传入
      var O = Object(this);
      
      //第二步:让长度值作为调用0的内部Get方法的结果值，传入的参数为“length”
      //第三步:让长度值变成32位整型。
      var len = O.length >>> 0;
      
      //第四步:如果callback不可调用，则抛出一个类型错误。
      //具体参见:http://es5.github.com/#x9.11
      if (typeof callback !== 'function') {
      throw new TypeError(callback + 'is not a function');
      }
      
      //第五步:如果thisArg被提供了，就是T值等于thisArg,否则让T值等于undefined.
      if(arguments.length > 1) {
        T ＝ thisArg;
      }
      
      //第六步:由长度值通过内建函数Array方法构建一个长度为len的新数组，并将结果传给A.
      A = new Array(len);
      
      //第七步:将k值赋为0
      k = 0;
      
      //第八步:当k<len的时候，循环重复。
      while(k < len) {
        var kValue, mappedValue；
        
        
      }
      
    ｝




