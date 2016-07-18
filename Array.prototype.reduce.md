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
                     .reduce(callback2, 0);  // 42
                     
### reduce怎样工作
> 试想一下以下的reduce的使用流程

        [0,1,2,3,4].reduce(function(previousValue,currentValue, currentIndex,arr){
        return previousValue + currentValue;
        })
        // 10
这个callback函数将会被执行4次，每次执行的参数和返回值如下所示：

你也可以提供一个[箭头函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
来代替完整的函数，以下的代码将会产生和上面代码一样的效果。

        [0,1,2,3,4].reduce((prev, curr) => prev + curr);
如果你提供一个初始值作为reduce函数的第二个参数，结果将会看起来如下所示：
        [0,1,2,3,4].reduce((previousValue, currentValue, currentIndex, array) => {
        return previousValue + currentValue;
        },10);
        // 20
        
### 例子
> 一个数组所有元素的和
        
        var total = [0,1,2,3].reduce(function(a,b) {
         return a+b;
        },0);
        // 6
用箭头函数写法如下：

        var total = [0,1,2,3].reduce((acc,cur)=>{return acc+cur;},0);
将一个数组扁平化处理：

        var flattened = [[0,1],[2,3],[4,5]].reduce(function(a,b) {
            return a.concat(b);
        },[]);
        // [0,1,2,3,4,5]
    
### Polyfill 
> Array.prototype.reduce在ECMA-262标准的第五版本中被加进；所以它不是在所有所准下都适用。
你可以在你的脚本中注入以下代码，来确保你能在不支持reduce的应用中使用reduce方法。

        // ECMA-262的生产步骤，第5版本， 15.4.4.21
        // 参考：http://es5.github.io/#x15.4.4.21
        if(!Array.prototype.reduce) {
            'use strict' 
            if(this == null) {
              throw new TypeError('Array.prototype.reduce called on null or undefined');
            }
            if(typeof callback !== 'function') {
                throw new TypeError(callback + ' is not a function');
            }
            var t = Object(this), len = t.length >>> 0, k = 0, value;
            if(arguments.length == 2) {
                value = arguments[1];
            } else {
                while(k < len && !(k in t)) {
                    k++;
                }
                if(k >= len) {
                    throw new TypeError('Reduce of empty array with no initial value');
                }
                value = t[k++];
            }
            for( ; k < len; k++) {
                if(k in t) {
                    value = callback(value, t[k], k, t);
                }
            }
            return value;
        }
        
####Q1: len = t.length >>> 0 ??
###A : 
> 参考：https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Unsigned_right_shift
>>> 符号表示0填充右移
