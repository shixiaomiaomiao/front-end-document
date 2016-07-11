#Array.prototype.reduce
> 原文地址：https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce

> reduce方法提供了带有累加器的函数，数组中的每个值（从左到右）被reduce为一个单一值。

### 语法

    arr.reduce(callback[,initialValue])

### 参数
- callback:处理数组中每个值的函数，需要四个参数
1)previousValue:这个值优先选取为上一次的callback的返回值，或者是initialValue(如果有提供的话)。
2)currentValue:数组中当前正在被处理的值。
3)currentIndex:数组中正在被处理的值的索引值。从0开始，如果initialValue被提供了，那么从1开始。
4)array:当前调用reduce的数组。

- initialValue: 可选值。被用来作为callback函数第一次调用时的第一个参数。

### 描述
reduce对于数组中的每个元素都执行callback 函数，包括空缺值，接受4个参数。
- previousValue
- currentValue
- currentIndex
- array

当callback首次被调用时，previousValue和currentValue可以是两个值。
如果initialValue被提供了，则previousValue的值将会等于initialValue，而currentValue将会等于数组中的第一个值。
如果initialValue没有被提供，previousValue将会等于数组中的第一个值，currentValue将会等于数组中的第二个值。

##### 注意：如果initialValue没有被提供，reduce函数将从索引值1（第二元素）开始执行callback函数，跳过第一个索引值；
如果initialValue被提供了，reduce函数将从索引值0开始。

如果数组是空的，并且initialValue没有被提供，则将会抛出[TypeError](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypeError)错误。
如果数组只有一个元素（不管元素的位置在哪）且没有initialValue值，或者有initialValue值，但是数组是空的，
那么这个单一的值将直接被返回，不经过callback处理。

相对来说提供initialValue值更加安全，因为如果没有initialValue值，将可能出现三种结果值。如下例子所示：

    var maxCallback = (pre, cur) => Math.max(pre.x, cur.x);
    var maxCallback2 = (max,cur) => Math.max(max, cur);
    
    // 没有initialValue值的reduce()函数
    [{x:22}, {x: 42}].reduce(maxCallback) ;  // 42
    [{x:22} ].reduce(maxCallback) ; //{x:22}
    [       ].reduce(maxCallback) ; //TypeError
    
    // map/reduce; 更好的解决方法，对于空数组也适用
    [{x:22}, {x: 42}].map(el => el.x)
                     .reduce(callback2, 0);  // ????
