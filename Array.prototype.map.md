# Array.prototype.map
> 原文： https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map

map的语法： arr.map( callback[ , thisArg] )
作用是：将原数组中的每个值都用 callback调用，将调用以后返回的结果值作为新数组。
callback接受三个参数：

- currentValue: 在数组中正在被处理的当前值
- index: 在数组中被处理的当前值的索引值
- array: 自从被调用起时的array.

thisArg: 可选值。但在执行callback函数时 被用作this. 默认值时Window对象。
