
## 手写一个深度比较函数
```js
function isEqual(obj1, obj2) {
  if(!isObject(obj1) || !isObject(obj2)) {
    return obj1 === obj2
  }

  if (obj1 === obj2) {
    return true
  }

  const obj1Keys = Object.keys(obj1)
  const obj2Keys = Object.keys(obj2)

  if(obj1Keys.length != obj2Keys.length) {
    return false
  }

  for (let key in obj1) {
    const res = isEqual(obj1[key], obj2[key])
    if(!res) {
      return false
    }
  }

  return true
}


const obj1 = {a:1,b:{x:100,y:200}}
const obj2 = {a:1,b:{x:100,y:200}}

isEqual(obj1, obj2) === true

```


## 手写一个map方法
```js

//循环实现数组 map 方法
    const selfMap = function (fn, context) {
        let arr = Array.prototype.slice.call(this) //map方法不会改变原数组
        let mappedArr = Array(arr.length) //原答案这里是length - 1，我感觉应该是length才对，否则遇到稀疏数组，循环被跳出了，长度会不对
        for (let i = 0; i < arr.length; i++) {
            // 稀疏数组，跳出当前循环
            if (!arr.hasOwnProperty(i)) {
                continue
            }
            mappedArr[i] = fn.call(context, arr[i], i, this) //方法的三个参数，currentValue, 当前下标， 当前数组
        }
        return mappedArr
    }

    Array.prototype.selfMap = selfMap
    var arr1 = [1, 2, 3]
    arr1.length = 5

    let arrMap = arr1.selfMap(function (x) {
        return x * 2
    })
    // [2, 4, 6, empty × 2]

```

##  手写-new 操作符
```js
function myNew(fn, ...args) {
  let obj = Object.create(fn.prototype);
  let res = fn.call(obj, ...args);
  if (res && (typeof res === "object" || typeof res === "function")) {
    return res;
  }
  return obj;
}
```
用法如下：

// // function Person(name, age) {
// //   this.name = name;
// //   this.age = age;
// // }
// // Person.prototype.say = function() {
// //   console.log(this.age);
// // };
// // let p1 = myNew(Person, "yyy", 18);
// // console.log(p1.name);
// // console.log(p1);
// // p1.say();


## 手写一个Object.is

Object.is不会转换被比较的两个值的类型，这点和===更为相似，他们之间也存在一些区别。
    1. NaN在===中是不相等的，而在Object.is中是相等的
    2. +0和-0在===中是相等的，而在Object.is中是不相等的


```js
Object.is = function (x, y) {
  if (x === y) {
    // 当前情况下，只有一种情况是特殊的，即 +0 -0
    // 如果 x !== 0，则返回true
    // 如果 x === 0，则需要判断+0和-0，则可以直接使用 1/+0 === Infinity 和 1/-0 === -Infinity来进行判断
    return x !== 0 || 1 / x === 1 / y;
  }

  // x !== y 的情况下，只需要判断是否为NaN，如果x!==x，则说明x是NaN，同理y也一样
  // x和y同时为NaN时，返回true
  return x !== x && y !== y;
};
```

## S037-实现一个LRU缓存函数
```js
class LRUCache {
  constructor(size) {
    this.size = size
    this.cache = new Map()
  }

  get(key) {
    const hasKey = this.cache.has(key)
    if (hasKey) {
      const val = this.cache.get(key)
      this.cache.delete(key)
      this.cache.set(key, val)
      return val
    } else {
      return -1
    }
  }

  put(key, val) {
    const hasKey = this.cache.has(key)
    if (hasKey) {
      this.cache.delete(key)
    }
    this.cache.set(key, val)
    if (this.cache.size > this.size) {
      this.cache.delete(this.cache.keys().next().value)
    }
  }

}
```

## 手写const
```js
function __const(data, value) {
    window[data] = value // 把要定义的data挂载到window下，并赋值value
	let c=1
    Object.defineProperty(window, data, { 
        enumerable: true, // 可枚举
        configurable: false, // 可配置
        get: function () {
			return value
        },
        set: function (newVal) {
			if(c>=1) throw new TypeError('Assignment to constant variable')
           c++
		   value = newVal
        }
    })
}
__const('a', 10)
a = 10 // 报错
console.log(a)

```

## 一秒输出一个数

```js
for(let i=0;i<=10;i++){   //用var打印的都是11
 setTimeout(()=>{
    console.log(i);
 },1000*i)
}

```

## 手写instanceOf
```js
function myInstanceof(left, right) {
  while (true) {
    if (left === null) {
      return false;
    }
    if (left.__proto__ === right.prototype) {
      return true;
    }
    left = left.__proto__;
  }
}

```

## 实现JSON.parse

```js
function parse (json) {
    return eval("(" + json + ")");
}
```

## 给你一个对象，统计一下它的层数

const obj = {
    a: { b: [1] },
    c: { d: { e: { f: 1 } } }
}

console.log(loopGetLevel(obj)) // 4


实现如下:
```js
function loopGetLevel(obj) {
    var res = 1;

    function computedLevel(obj, level) {
        var level = level ? level : 0;
        if (typeof obj === 'object') {
            for (var key in obj) {
                if (typeof obj[key] === 'object') {
                    computedLevel(obj[key], level + 1);
                } else {
                    res = level + 1 > res ? level + 1 : res;
                }
            }
        } else {
            res = level > res ? level : res;
        }
    }
    computedLevel(obj)

    return res
}

```