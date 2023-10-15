# Array 常用方法

- Array 常见 API(opens new window)
  - `Array.from()`, `Array.of()`, `Array.isArray()`, `.fill()`
  - `.sort()`, `.reverse()`, `.flat()`, `.flatMap()`
  - `.pop()`, `.push()`, `.shift()`, `.unshift()`
  - `.map()`, `.filter()`, `.reduce()`, `.reduceRight()`, `.forEach()`, `.every()`, `.some()`
  - `.find()`, `.findIndex()`, `.includes()`, `.indexOf()`, `.lastIndexOf()`
  - `.concat()`, `.join()`, `.slice()`, `.splice()`
  - `.keys()`, `.values()`, `.entries()`

下表列出了会修改原始数组的方法，以及相应的非修改方法：

| 修改方法                                                     | 相应的非修改方法                                             |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [`copyWithin()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/copyWithin) | 没有相应的非修改方法                                         |
| [`fill()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/fill) | 没有相应的非修改方法                                         |
| [`pop()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/pop) | [`slice(0, -1)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/slice) |
| [`push(v1, v2)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/push) | [`concat([v1, v2\])`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) |
| [`reverse()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse) | [`toReversed()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/toReversed) |
| [`shift()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/shift) | [`slice(1)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/slice) |
| [`sort()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) | [`toSorted()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/toSorted) |
| [`splice()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/splice) | [`toSpliced()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/toSpliced) |
| [`unshift(v1, v2)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift) | [`toSpliced(0, 0, v1, v2)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/toSpliced) |

[`Array.prototype.at()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/at)

返回给定索引处的数组元素。接受从最后一项往回计算的负整数。

[`Array.prototype.copyWithin()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/copyWithin)

在数组内复制数组元素序列。

[`Array.prototype.entries()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/entries)

返回一个新的[*数组迭代器*](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Iterators_and_generators)对象，其中包含数组中每个索引的键/值对。

[`Array.prototype.fill()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/fill)

用静态值填充数组中从开始索引到结束索引的所有元素。

[`Array.prototype.flat()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flat)

返回一个新数组，所有子数组元素递归地连接到其中，直到指定的深度。

[`Array.prototype.flatMap()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flatMap)

对调用数组的每个元素调用给定的回调函数，然后将结果展平一层，返回一个新数组。

[`Array.prototype.reverse()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse)

*就地*反转数组中元素的顺序。（前面变成后面，后面变成前面。）

[`Array.prototype.reduce()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)

对数组的每个元素（从左到右）执行用户提供的“reducer”回调函数，将其简化为单个值。

[`Array.prototype.shift()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/shift)

从数组中移除第一个元素并返回该元素。

[`Array.prototype.slice()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)

提取调用数组的一部分并返回一个新数组。

[`Array.prototype.splice()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

从数组中添加和/或删除元素。

[`Array.prototype.unshift()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift)

在数组的前面添加一个或多个元素，并返回数组新的 `length`。

[`Array.prototype.with()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/with)

返回一个新数组，其中给定索引处的元素替换为给定值，而不改变原始数组。