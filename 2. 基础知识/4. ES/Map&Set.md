# 介绍下 Set、Map、WeakSet 和 WeakMap 的区别？

## Set

 1. 成员不能重复
 2. 只有健值，没有健名，有点类似数组。
 3. 可以遍历，方法有add, delete,has
## weakSet

> 成员都是对象
> 成员都是弱引用，随时可以消失。 可以用来保存DOM节点，不容易造成内存泄漏
> 不能遍历，方法有add, delete,has

## Map
> 本质上是健值对的集合，类似集合
> 可以遍历，方法很多，可以干跟各种数据格式转换

## weakMap
> 直接受对象作为健名（null除外），不接受其他类型的值作为健名
> 健名所指向的对象，不计入垃圾回收机制
> 不能遍历，方法同get,set,has,delete
>


# Map&Set

以前使用集合，多数情况下会直接用 Object 代替，ES6 新增了两个特性，Map 和 Set，他们是对 JavaScript 关于集合概念的补充

## Map

### 前言

为什么会有 Map？像对象 Object，是由 key:value 集合组成的，但是**key 只能是字符串**。map 的作用就是可以用其他类型的数据做 key。

例如

```javascript
var map = new Map();
map.set(1, 2);
map.set({ name: 'johan' }, true);
// set(key, value)
```

### Map 是什么

`Map` 在其他语言中被翻译为字典，在 ES6 规范中引入了新的数据类型 `Map` 就是对字典这类数据结构的一种补充。

`Map` 是一组键值对的结构，具有极快的查找速度。数据结构是 hash-table（哈希表）

Map 是一个带键的数据项的集合，就像一个 Object 一样，但是它们最大的差别是 Map 允许任何类型的键（key）

### 方法与属性

-   new Map() —— 创建 map
-   map.set(key, value) —— 根据键存储值
-   map.get(key) —— 根据键来返回值，如果 map 中不存在对应的 key，则返回 undefined
-   map.has(key) —— 如果 key 存在则返回 true，否则返回 false
-   map.delete(key) —— 删除指定键的值
-   map.clear() —— 清空 map
-   map.size —— 返回当前元素个数

### 使用方法

```javascript
const m = new Map([
    ['Johan', 26],
    ['Elaine', 26],
    ['Bob', 12],
]);
m.get('Johan'); // 26
```

### 算法中是使用

最常见的是求两数之和和三数之和。无论是哪一种，本质都是目标数与循环数的差

例题：https://leetcode-cn.com/problems/two-sum/

> 给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **和为目标值** _`target`_ 的那 **两个** 整数，并返回它们的数组下标

示例 1：

```
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
```

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function (nums, target) {
    let len = nums.length;
    let map = new Map();
    for (let i = 0; i < len; i++) {
        const diff = target - nums[i];
        if (map.has(diff)) {
            return [map.get(diff), i];
        }
        map.set(num[i], i);
    }
};
```

### 窥视 Map

之前在将 Promise 时，我们已经自己手写了 Promise，那么 Map（字典）我们是否也能手写一个呢？

老规矩，先打印它具体有哪些参数

```javascript
console.dir(Map);
```

![Map构造函数结构](../public/images/ES6/Map构造函数结构.png)

肉眼分析可得，它是基于 Object 创建的对象实例（`__proto__`指向 Object，不懂的可以去 JavaScript 中的原型篇中了解一二），其次它的原型上有`clear`、`delete(key)`、`entries`、`forEach(callbackFn[, thisArg])`、`get(key)`、`set(key, valye)`、`has(key)`、`keys`、`values`、`[@@iterator]` 等十个方法，还有两个原型属性 `constructor` 和 `size`。各个方法和属性对应的解释不做说明，懂的人自然懂，不懂的可以去查

我们手写一个 Map

```javascript
function MyMap() {

}
MyMap.prototype = {
    constructor: MyMap;
    clear: function() {

    },
    delete: function(key) {

    },
    entries: function(key) {

    },
    forEach: function(callback) {

    },
    get: function(key) {

    },
    set: function(key, value) {

    },
    has: function(key) {

    },
    values: function(key) {

    }
}
var m = new Map([])
```

### WeakMap

与 Map 类似，但又几点区别：

-   WeakMap 只接受对象作为 key，如果设置其他类型的数据作为 key，会报错

Map 与 Object 的区别

-   Map 与 Object 都可以存取数据，Map 适用于存储需要**常需要变化（增减键值对）或遍历**的数据集，而 Object 适用于存储**静态（例如配置信息）**数据集
-   Object 的 key 必须是 String 或 Symbol 类型，而 Map 无此限制，可以是任何值
-   Map 可以很方面的取到键值对数量，而 Object 需要用额外途径

## Set

Set 作为最简单的集合，有着如下几个特点：

-   Set 可以存储任何类型的值，遍历顺序与 插入顺序相同
-   SET 内无重复的值

`Set` 和 `Map` 类似，也是一组 key 的集合，但不存储 value 。由于 key 不能重复，所以，在`Set`中，没有重复的 key

## WeakMap + WeakSet

主要特点是弱引用

相比于 Map 和 Set 的强引用，弱引用可以令对象在“适当”情况下正确被 GC 回收，减少内存资源浪费

但由于不是强引用，所以无法进行遍历或取得值数量，只能用于值的存取（WeakMap）或是否存在值的判断（WeakSet）

### 参考资料

-   [Map and Set（集合和映射）](https://zh.javascript.info/map-set)
-   [「 Map 最佳实践」什么时候适合使用 Map 而不是 Object](https://mp.weixin.qq.com/s/ax-Lec-wam0pptpRTH5Log)
-   [Map 和 Set](https://www.liaoxuefeng.com/wiki/1022910821149312/1023024181109440)


## map 的使用
```
map.set(key,value)添加键值对到映射中
map.get(key)获取映射中某一个键的对应值
map.delete(key)将某一键值对移除映射
map.clear()清空映射中所有键值对
map.entries()返回一个以二元数组（键值对）作为元素的数组
map.has(key)检查映射中是否包含某一键值对
map.keys()返回一个当前映射中所有键作为元素的可迭代对象
map.values()返回一个当前映射中所有值作为元素的可迭代对象
map.size映射中键值对的数量
```



垃圾回收机制
我们知道，程序运行中会有一些垃圾数据不再使用，需要及时释放出去，如果我们没有及时释放，这就是内存泄露

JS 中的垃圾数据都是由垃圾回收（Garbage Collection，缩写为 GC）器自动回收的，不需要手动释放，它是如何做的喃？

很简单，JS 引擎中有一个后台进程称为垃圾回收器，它监视所有对象，观察对象是否可被访问，然后按照固定的时间间隔周期性的删除掉那些不可访问的对象即可

现在各大浏览器通常用采用的垃圾回收有两种方法：
引用计数
标记清除


引用计数
最早最简单的垃圾回收机制，就是给一个占用物理空间的对象附加一个引用计数器，当有其它对象引用这个对象时，这个对象的引用计数加一，反之解除时就减一，当该对象引用计数为 0 时就会被回收。

该方式很简单，但会引起内存泄漏：

// 循环引用的问题
function temp(){
    var a={};
    var b={};
    a.o = b;
    b.o = a;
}
这种情况下每次调用 temp 函数，a 和 b 的引用计数都是 2 ，会使这部分内存永远不会被释放，即内存泄漏。现在已经很少使用了，只有低版本的 IE 使用这种方式。

标记清除
V8 中主垃圾回收器就采用标记清除法进行垃圾回收。主要流程如下：

标记：遍历调用栈，看老生代区域堆中的对象是否被引用，被引用的对象标记为活动对象，没有被引用的对象（待清理）标记为垃圾数据。
垃圾清理：将所有垃圾数据清理掉


在我们的开发过程中，如果我们想要让垃圾回收器回收某一对象，就将对象的引用直接设置为 null

var a = {}; // {} 可访问，a 是其引用

a = null; // 引用设置为 null
// {} 将会被从内存里清理出去


但如果一个对象被多次引用时，例如作为另一对象的键、值或子元素时，将该对象引用设置为 null 时，该对象是不会被回收的，依然存在

```
var a = {}; 
var arr = [a];

a = null; 
console.log(arr)
// [{}]
```

如果作为 Map 的键喃？

var a = {}; 
var map = new Map();
map.set(a, '三分钟学前端')

a = null; 
console.log(map.keys()) // MapIterator {{}}
console.log(map.values()) // MapIterator {"三分钟学前端"}
如果想让 a 置为 null 时，该对象被回收，该怎么做喃？

WeakMap vs Map
ES6 考虑到了这一点，推出了： WeakMap 。它对于值的引用都是不计入垃圾回收机制的，所以名字里面才会有一个"Weak"，表示这是弱引用（对对象的弱引用是指当该对象应该被GC回收时不会阻止GC的回收行为）。



### Map 相对于 WeakMap ：

Map 的键可以是任意类型，WeakMap 只接受对象作为键（null除外），而值可以是任意。
 2.WeakMap不能包含无引用的对象，否则会被自动清除出集合（垃圾回收机制）
Map 可以被遍历， WeakMap 不能被遍历



注意，只有对同一个对象的引用，Map 结构才将其视为同一个键。这一点要非常小心。
```
const map = new Map();

map.set(['a'], 555);
map.get(['a']) // undefined
```
上面代码的set和get方法，表面是针对同一个键，但实际上这是两个值，内存地址是不一样的，因此get方法无法读取该键，返回undefined。



任何具有 Iterator 接口、且每个成员都是一个双元素的数组的数据结构都可以当作Map构造函数的参数，例如：
```
const set = new Set([
  ['foo', 1],
  ['bar', 2]
]);
const m1 = new Map(set);
m1.get('foo') // 1

const m2 = new Map([['baz', 3]]);
const m3 = new Map(m2);
m3.get('baz') // 3
```


如果读取一个未知的键，则返回undefined。
```
new Map().get('asfddfsasadf')
// undefined

注意，只有对同一个对象的引用，Map 结构才将其视为同一个键。这一点要非常小心。
const map = new Map();

map.set(['a'], 555);
map.get(['a']) // undefined复制代码

上面代码的set和get方法，表面是针对同一个键，但实际上这是两个值，内存地址是不一样的，因此get方法无法读取该键，返回undefined。
由上可知，Map 的键实际上是跟内存地址绑定的，只要内存地址不一样，就视为两个键。这就解决了同名属性碰撞（clash）的问题，我们扩展别人的库的时候，如果使用对象作为键名，就不用担心自己的属性与原作者的属性同名。
如果 Map 的键是一个简单类型的值（数字、字符串、布尔值），则只要两个值严格相等，Map 将其视为一个键，比如0和-0就是一个键，布尔值true和字符串true则是两个不同的键。另外，undefined和null也是两个不同的键。虽然NaN不严格相等于自身，但 Map 将其视为同一个键。
let map = new Map();

map.set(-0, 123);
map.get(+0) // 123

map.set(true, 1);
map.set('true', 2);
map.get(true) // 1

map.set(undefined, 3);
map.set(null, 4);
map.get(undefined) // 3

map.set(NaN, 123);
map.get(NaN) // 123复制代码

Map 的属性及方法
属性：

constructor：构造函数
size：返回字典中所包含的元素个数



const map = new Map([
  ['name', 'An'],
  ['des', 'JS']
]);

map.size // 2复制代码

操作方法：

set(key, value)：向字典中添加新元素
get(key)：通过键查找特定的数值并返回
has(key)：判断字典中是否存在键key
delete(key)：通过键 key 从字典中移除对应的数据
clear()：将这个字典中的所有元素删除



遍历方法

Keys()：将字典中包含的所有键名以迭代器形式返回
values()：将字典中包含的所有数值以迭代器形式返回
entries()：返回所有成员的迭代器
forEach()：遍历字典的所有成员



const map = new Map([
        ['name', 'An'],
        ['des', 'JS']
]);
console.log(map.entries())    // MapIterator {"name" => "An", "des" => "JS"}
console.log(map.keys()) // MapIterator {"name", "des"}复制代码

Map 结构的默认遍历器接口（Symbol.iterator属性），就是entries方法。
map[Symbol.iterator] === map.entries
// true复制代码

Map 结构转为数组结构，比较快速的方法是使用扩展运算符（...）。
对于 forEach ，看一个例子
const reporter = {
  report: function(key, value) {
    console.log("Key: %s, Value: %s", key, value);
  }
};

let map = new Map([
    ['name', 'An'],
    ['des', 'JS']
])
map.forEach(function(value, key, map) {
  this.report(key, value);
}, reporter);
// Key: name, Value: An
// Key: des, Value: JS复制代码

在这个例子中， forEach 方法的回调函数的 this，就指向 reporter
与其他数据结构的相互转换
1.Map 转 Array
const map = new Map([[1, 1], [2, 2], [3, 3]])
console.log([...map])    // [[1, 1], [2, 2], [3, 3]]复制代码

2.Array 转 Map
const map = new Map([[1, 1], [2, 2], [3, 3]])
console.log(map)    // Map {1 => 1, 2 => 2, 3 => 3}复制代码

3.Map 转 Object
因为 Object 的键名都为字符串，而Map 的键名为对象，所以转换的时候会把非字符串键名转换为字符串键名。
function mapToObj(map) {
    let obj = Object.create(null)
    for (let [key, value] of map) {
        obj[key] = value
    }
    return obj
}
const map = new Map().set('name', 'An').set('des', 'JS')
mapToObj(map)  // {name: "An", des: "JS"}复制代码

4.Object 转 Map
function objToMap(obj) {
    let map = new Map()
    for (let key of Object.keys(obj)) {
        map.set(key, obj[key])
    }
    return map
}

objToMap({'name': 'An', 'des': 'JS'}) // Map {"name" => "An", "des" => "JS"}复制代码

5.Map 转 JSON
function mapToJson(map) {
    return JSON.stringify([...map])
}

let map = new Map().set('name', 'An').set('des', 'JS')
mapToJson(map)    // [["name","An"],["des","JS"]]复制代码

6.JSON 转 Map
function jsonToStrMap(jsonStr) {
  return objToMap(JSON.parse(jsonStr));
}

jsonToStrMap('{"name": "An", "des": "JS"}') // Map {"name" => "An", "des" => "JS"}

