
## Set

Set 是一种数据结构，用于存储唯一值。

### 特点

- 唯一性
- 可迭代性：`for...of` 按照添加顺序
- 添加元素：`add`
- 删除元素：`delete`
- 检查元素是否存在：`has`
- 获取元素数量：`size`

### 应用场景

- 去重
- 事件监听的管理
- 集合运算
- 缓存管理
- 处理用户输入

```js
// 去重
const unique = [...new Set([1,1,1,1,1])]
// 事件监听管理
const eventHandlers = new Set()
// 集合
const set1 = [1,2,3],set2 = [3,4,5]
// 并集
const union = [...new Set([...set1],[...set2])]
// 交集
const intersection = set1.filter(item=>set2.has(item))
// 差集
const difference = set1.filter(item=>!set2.has(item))
// 缓存
const cache = new Set()
function addToCache(item){
	if(!cache.has(item)){
		cache.add(item)
	}
}
```

### `Set` 和 `WeakSet`

都是 JavaScript 中的集合类型，但它们有一些关键的区别：

1. **存储的值类型：**
    
    - `Set` 可以存储任意类型的值，包括原始数据类型和对象引用。
    - `WeakSet` 只能存储对象引用。它不接受原始数据类型，并且对存储的对象是弱引用，这意味着存储在 `WeakSet` 中的对象不会阻止垃圾回收。

2. **强引用 vs 弱引用：**
    
    - 对于 `Set`，它存储的是强引用。即使在 `Set` 中存在对某个对象的引用，该对象也不会被垃圾回收，直到从 `Set` 中删除对该对象的引用或清空整个 `Set`。
    - 对于 `WeakSet`，存储的是弱引用。这意味着存储在 `WeakSet` 中的对象如果在其他地方没有强引用，就可能被垃圾回收。`WeakSet` 不阻止存储的对象被垃圾回收，因此在许多情况下，它更适合临时性的关联。
    
3. **迭代和清空：**
    
    - 由于 `WeakSet` 中的对象是弱引用，`WeakSet` 不具备迭代方法和清空整个集合的方法。这是因为在迭代的过程中，集合中的对象可能已经被垃圾回收，因此不能准确遍历所有元素。

4. **API 方法的差异：**
    
    - `Set` 提供了丰富的方法，包括 `add`、`delete`、`has`、`clear` 等，还有迭代方法如 `forEach`。
    - `WeakSet` 的方法相对较少，它只提供了 `add`、`delete` 和 `has` 方法，没有清空整个集合的方法。

在选择使用 `Set` 还是 `WeakSet` 时，主要取决于你的需求。如果你需要存储任意类型的值，并且希望这些值在集合外部被引用时不被垃圾回收，那么使用 `Set`。如果你希望存储对象引用，且不希望阻止对象被垃圾回收，那么 `WeakSet` 可能更适合。

## Map

是一种集合类型，用于存储键值对，与 `Object` 相比，`Map` 的key更加灵活，可以是任意数据类型。

### 特点

- 灵活的键类型
- 保持添加顺序 - 按照添加的顺序
- 可迭代 - `for...of`
- 添加 - `set`
- 删除 - `delete`
- 键也是唯一的

### 应用场景

适用于许多需要灵活性、有序性和键唯一的场景；优势在于处理键值对的复杂数据结构。

### 最佳实践

```js
// 链式操作
const mapData = new Map().set('one',1)
						.set('two',2)
						.set('three',3)
// 解构赋值
for(const [key,value] of mapData){
	console.log(key,value)
}

// 数组转换
[...mapData]
// 对象转换
Object.fromEntries(mapData)

```